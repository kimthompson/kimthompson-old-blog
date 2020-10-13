---
title: Testing @ MPR
date: 2020-10-12T22:00:00.000Z
---

I wrote this for my team earlier this year to ensure that we were all on the same page regarding testing. Nobody on my team (myself included) really had strong opinions other than 1) we should be doing more of it and 2) these tests should be written in the same way everywhere. In light of that, I watched Kent Dodd's two FEM courses, read all his testing blog posts and synthesized what I learned into this lightweight guide.

<!-- more -->

## A Distillation and Bastardization of the Scattered Teachings of Kent Dodds

I wrote this for my team earlier this year to ensure that we were all on the same page regarding testing. Nobody on my team (myself included) really had strong opinions other than 1) we should be doing more of it and 2) these tests should be written in the same way everywhere. In light of that, I watched Kent Dodd's two FEM courses, read all his testing blog posts and synthesized what I learned into this lightweight guide.

The goal of this rulebook is to set out in writing what it means for one of MPR's libraries to be well tested. This is what we have decided we need to feel confident that our code works and we won't push out any breaking changes.

### The Testing Trophy

#### Terminology & Definitions

Dodds' "testing trophy" diagram lays out the confidence gained in each stage of testing, with cost and difficulty increasing the higher you go. My thought was that we should keep doing what we're doing for static testing, ensure that our unit tests follow all the rules I'll outline later, and try to expand on integration testing where we can, since that is where the most confidence can be gained for the least work.

![Testing Trophy](blog/testing-trophy.jpg)

Here is what we are doing/can implement soon for each of these stages:

#### Static

We use ESLint, Sasslint, PropTypes, and Prettier. Dodds recommends Flow or TypeScript to force JavaScript, but Flow is basically dead and TypeScript is more of an intense lift for our apps that we likely want to spring for right now. (Note from the future: We started doing new development in TypeScript in August)

#### Unit

This comprises most of the tests we've written so far. Here's an example how to unit test a bit of UI, from one of Dodd's blog posts:

``` javascript
import '@testing-library/jest-dom/extend-expect'
import React from 'react'
import { render } from '@testing-library/react'
import ItemList from '../item-list'

// Some people don't call these a unit test because we're rendering to the DOM with React.
// They'd tell you to use shallow rendering instead.
// When they tell you this, send them to https://kcd.im/shallow

test('renders "no items" when the item list is empty', () => {
  const { getByText } = render(<ItemList items={[]} />)
  expect(getByText(/no items/i)).toBeInTheDocument()
})

test('renders the items in a list', () => {
  const { getByText, queryByText } = render(
    <ItemList items={['apple', 'orange', 'pear']} />,
  )

  // note: with something so simple I might consider using a snapshot instead, but only if:
  // 1. the snapshot is small
  // 2. we use toMatchInlineSnapshot()

  expect(getByText(/apple/i)).toBeInTheDocument()
  expect(getByText(/orange/i)).toBeInTheDocument()
  expect(getByText(/pear/i)).toBeInTheDocument()
  expect(queryByText(/no items/i)).not.toBeInTheDocument()
})
```

Here's an example of unit testing a function.

``` javascript
import cases from 'jest-in-case'
import fizzbuzz from '../fizzbuzz'

cases(
  'fizzbuzz',
  ({input, output}) => expect(fizzbuzz(input)).toBe(output),
  [
    [1, '1'],
    [2, '2'],
    [3, 'Fizz'],
    [5, 'Buzz'],
    [9, 'Fizz'],
    [15, 'FizzBuzz'],
    [16, '16'],
  ].map(([input, output]) => ({title: `${input} => ${output}`, input, output})),
)
```

#### <a name="integration-example">Integration</a>

Integration tests will render a good chunk of your app — all of the providers, etc. — mocking as little as possible to see if it all works together. If your app is small enough, this test may even render the whole thing, but that will not be the case for most of our stuff. The line between this and E2E testing is a bit wobbly.

The only things that should consistently be mocked are network requests and components responsible for animation. For more detail, check out the dedicated section on [Mocking](#mocking).

``` javascript
import React from 'react'
// this module is mocked via jest's __mocks__ directory feature
import axiosMock from 'axios'
import { render, generate, fireEvent } from 'til-client-test-utils'
import { init as initAPI } from '../utils/api'
import App from '../app'

beforeEach(() => {
  window.localStorage.removeItem('token')
  axiosMock.__mock.reset()
  initAPI()
})

test('login as an existing user', async () => {
  const {
    getByTestId,
    container,
    getByText,
    getByLabelText,
    finishLoading
  } = render(<App />)

  // wait for the app to finish loading the mocked requests
  await finishLoading()
  fireEvent.click(getByText(/login/i))
  expect(window.location.href).toContain('login')

  // fill out form
  const fakeUser = generate.loginForm()
  const usernameNode = getByLabelText(/username/i)
  const passwordNode = getByLabelText(/password/i)

  usernameNode.value = fakeUser.username
  passwordNode.value = fakeUser.password

  // submit form
  const { post } = axiosMock.__mock.instance
  const token = generate.token(fakeUser)

  post.mockImplementationOnce(() =>
    Promise.resolve({
      data: {user: {...fakeUser, token}}
    }),
  )

  fireEvent.click(getByText(/submit/i))

  // wait for the mocked requests to finish
  await finishLoading()

  // assert calls
  expect(axiosMock.__mock.instance.post).toHaveBeenCalledTimes(1)
  expect(axiosMock.__mock.instance.post).toHaveBeenCalledWith(
    '/auth/login',
    fakeUser
  )

  // assert the state of the world
  expect(window.localStorage.getItem('token')).toBe(token)
  expect(window.location.href).not.toContain('login')
  expect(getByTestId('username-display').textContent).toEqual(fakeUser.username)
  expect(getByText(/logout/i)).toBeTruthy()
})
```

#### E2E

This is where you use a tool like Cypress to click through your site just like a user would. It doesn’t even apply to things like our libraries, and would be overkill for most of our sites. Maybe we should try it with a big site like MPR News if we ever get the time (which we won’t).

### <a name="mocking">Mocking</a>

Mocks are, at their core, functions that keep track of how they’re called and what called them. Dodds prefers to avoid mocking wherever possible, but sometimes it is not just feasible or desirable to import and run an actual function as many times as you need to test the features that use it. Mock where it makes sense -- where things are slow, where you have to wait for data from an API, where you have to wait for animations, where JSDOM can’t figure out what an SVG is, and so on.

For the purposes of this illustration, we’re going to pretend that the following component is making a call to some third party machine learning service that has a testing environment we don’t control and is unreliable. Instead of basically reimplementing that so that we can “test” it, we’re going to mock it out and test what we’ve built off using it.

``` javascript
import { getWinner } from './utils'

function thumbWar(player1, player2) {
  const numberToWin = 2
  let player1Wins = 0
  let player2Wins = 0

  while (player1Wins < numberToWin && player2Wins < numberToWin) {
    const winner = getWinner(player1, player2)
    if (winner === player1) {
      player1Wins++
    } else if (winner === player2) {
      player2Wins++
    }
  }

  return player1Wins > player2Wins ? player1 : player2
}

export default thumbWar
```

We don’t want to re-implement the workings of `getWinner` in our tests, so it’s fine to keep it simple and just hardcode a winner. There are tons of ways to mock something, from monkey patching to Jest’s own `spyOn`, but the best and easiest of these is to just use `jest.mock`.

``` javascript
import thumbWar from './thumbWar'
import * as utilsMock from '../utils'

jest.mock('../utils', () => {
  return {
    getWinner: jest.fn((p1, p2) => p2)
  }
})

test('returns winner', () => {
  const winner = thumbWar('Ken Wheeler', 'Kent C. Dodds')
  expect(winner).toBe('Kent C. Dodds')
  expect(utilsMock.getWinner).toHaveBeenCalledTimes(2)
  utilsMock.getWinner.mock.calls.forEach(args => {
    expect(args).toEqual(['Ken Wheeler', 'Kent C. Dodds'])
  })
})
```

Fun fact: I watched his first testing course and didn’t know this existed until Philip told me about it like two months ago, and I was skeptical that it would just magically replace the imported function with my new one.

![I am boo boo the fool](https://i.kym-cdn.com/entries/icons/facebook/000/022/477/5ebacf52cd3221a7487b805d0954b422.jpg)

If you want something to be mocked in a lot of tests, you can even create a `__mocks__` directory right next to your `__tests__` directory for that area and import it from there. In this case, in `__mocks__/utils.js`:

``` javascript
export const getWinner = jest.fn((p1, p2) => p2)
```

It is then called in the tests instead of the normal `getWinner`:

``` javascript
import thumbWar from '../thumbWar'
import * as utilsMock from '../utils'

jest.mock('../utils')

test('returns winner', () => {
  const winner = thumbWar('Ken Wheeler', 'Kent C. Dodds')
  expect(winner).toBe('Kent C. Dodds')
  expect(utilsMock.getWinner).toHaveBeenCalledTimes(2)
  utilsMock.getWinner.mock.calls.forEach(args => {
    expect(args).toEqual(['Ken Wheeler', 'Kent C. Dodds'])
  })
})
```

### File Structure

Our apps currently have kind of a mix of organization schemes. Some have a `__tests__` folder at the root level, while others have a `__tests__` folder in each component folder, while some skip that entirely and pair the `*.test.js` file right next to what it’s testing. I favored the latter for its terseness, but if we organize the way Dodds recommends, more options are open to us.

Most tests should be contained right next to their component, in a `__tests__` folder. This makes it a little harder to forget that tests exist when you update a component. If you need to, you can also have a `__mocks__` folder in that directory for your nearby tests to access.

If you need to run more of a sitewide test or mock something for all tests, you can put a `__tests__` and a `__mocks__` directory at the root level of the app, which is wherever you declared in your <a name="#configuration">Jest config</a>. For data that your tests all need to access, keep it all in a `__data__` folder within your root `__tests__` folder.

To summarize, the most common file structure in our tested applications, assuming we need component-specific mocks at all, will look a lot like this:

```
Component/
├── index.js
├── Subcomponent.js
├── __data__/
│   └── data.json
├── __mocks__/
│   └── utils.js
└── __tests__/
    ├── Component.test.js
    └── Subcomponent.test.js
```

### Code Coverage

Lots of people (often management) make the mistake of instituting a 100% code coverage rule. This is a misguided impulse and will often lead to bad or superficial tests.

What does code coverage tell you? All it says is “this code was run when your tests were run”. It cannot confirm that:

1. This code will work according to business requirements
2. This code works with all other code in the application

There is no one size fits all solution for a good code coverage number to shoot for. The only wiggly metric that matters is how confident you are that the important parts of your application are covered.

In that light, I would propose that our average websites aim for 80% code coverage. This was inspired by a heuristic I like outside of coding, where 80% ofthe effort in any given space generally nets you 99% of the results, and any more effort after that has diminished returns.

More important than what I’ve decided might be a good number, after our initial refactor of tests, we should set up coverage thresholds in our projects so that our coverage cannot sink any lower when we add new features (see the section on <a name="#configuration">configuration</a> for how to do this).

### Snapshots

Snapshots don’t often end up being all that useful. More often than not, any change will break the snapshot, and you’ll just hit the `u` button to update, assuming that it’s nothing, almost always correctly. 

Some authorities on testing say it should never be used, but Dodds is a bit softer on the issue. He thinks they are great for detecting changes in the UI on very small bits of code, and that your snapshots should be very small. For example, if a component relies on some CSS for functionality and you want to be sure you don’t change it or knock it out without some sort of alarm going off.

So yeah, we’re going to purge most of our snapshots and likely not use them much in the future.

### Simulating Events

When you create a container for testing, it’s isolated. You’re not actually attaching it to the DOM, so you need to use Jest functions like `fireEvent()` to interact with your page, and you ought to use `renderIntoDocument()` instead of the normal `render()` function as well. See the <a name="#integration-example">Integration Test example</a> for an idea of what this looks like.

### <a name="configuration">Configuration</a>

Here's an example of one of our `jest.config.js` files:

``` javascript
module.exports = {
  coverageDirectory: './coverage',
  collectCoverageFrom: [
    '**/src/**/*.js',
    '!**/__tests__/**',
    '!**/node_modules/**'
  ],
  setupFilesAfterEnv: ['./src/setupTests.js'],
  coverageThreshold: {
    global: {
      statements: 85,
      branches: 80,
      functions: 100,
      lines: 85
    }
  }
}
```

As you can see, we also have a `setupTests.js` file that takes care of a few important things our tests will need to run properly.

``` javascript
import '@testing-library/jest-dom'
import 'jest-prop-type-error'
import 'babel-polyfill'
```

You can add more here as necessary and as you discover new tools that help your tests run better. These are just the tools I use and the things I installed to make the confusing runtime errors go away.

### Best Practices

#### Arrange, Act, Assert

The generic pattern you’ll follow when setting up tests: render or run the function you want, do something with it (if applicable) and then see if everything turned out like you expected.

#### Object & Test Factories

An object factory is basically a function that will create your object and provide you an opportunity to overwrite it. Here’s an example:

``` javascript
import * as blogPostController from '../blog-post'

jest.mock('../../lib/db')

function setup(overrides = {}) {
  const req = {
    locale: {
      source: 'default',
      language: 'en',
      region: 'GB',
    },
    user: {
      guid: '0336397b-e29d-4b63-b94d-7e68a6fa3747',
      isActive: false,
      picture: 'http://placehold.it/32x32',
      age: 30,
      name: {
        first: 'Francine',
        last: 'Oconnor',
      },
      company: 'ACME',
      email: 'francine.oconnor@ac.me',
      latitude: 51.507351,
      longitude: -0.127758,
      favoriteFruit: 'banana',
    },
    body: {},
    cookies: {},
    query: {},
    params: {
      bucket: 'photography',
    },
    header(name) {
      return {
        Authorization: 'Bearer TEST_TOKN',
      }[name]
    },
  }

  const res = {
    clearCookie: jest.fn(),
    cookie: jest.fn(),
    end: jest.fn(),
    locals: {
      content: {},
    },
    json: jest.fn(),
    send: jest.fn(),
    sendStatus: jest.fn(),
    set: jest.fn(),
  }
  const next = jest.fn()

  return {req, res, next}
}

test('lists blog posts for the logged in user', async () => {
  const {req, res, next} = setup()

  await blogPostController.loadBlogPosts(req, res, next)

  expect(res.json).toHaveBeenCalledTimes(1)
  expect(res.json).toHaveBeenCalledWith({
    posts: expect.arrayContaining([
      expect.objectContaining({
        title: 'Test Post 1',
        subtitle: 'This is the subtitle of Test Post 1',
        body: 'The is the body of Test Post 1',
      }),
    ]),
  })
})

test('returns an empty list when there are no blog posts', async () => {
  const {req, res, next} = setup()
  req.user.latitude = 31.230416
  req.user.longitude = 121.473701

  await blogPostController.loadBlogPosts(req, res, next)

  expect(res.json).toHaveBeenCalledTimes(1)
  expect(res.json).toHaveBeenCalledWith({
    posts: [],
  })
})
```

Throwing that object generation into a setup function really helped clarity here, since it makes it crystal clear that, for example, the final test is testing latitude and longitude. If you had set up a new object in every single test, it would have been difficult to spot that.

Try to follow the AHA (Avoid Hasty Abstraction) principle for testing, which falls somewhere in the middle of ANA (Absolutely No Abstraction) and DRY (Don’t Repeat Yourself). Basically, what he means by this is that you should only split things out into object or test factories if your tests will become clearer.

Sometimes doing clever little things to avoid repeating yourself actually makes your tests harder to read, because someone has to scroll around to see what you’re refrring to. Then again, if you never abstract anything, some of your tests with a lot of setup can become so long that you forget which one you’re looking at. Abstract, but not *too* much. What that means is kind of up to you and whoever’s reviewing your code.

Why would you not just use beforeEach()? That brings us to our second practice:

#### Avoid Nesting

The following code works fine and isn’t bad. But according to Dodds, it is harder to read than it ought to be.

``` javascript

import React from 'react'
import {render, fireEvent} from '@testing-library/react'
import Login from '../login'

describe('Login', () => {
  let utils,
    handleSubmit,
    user,
    changeUsernameInput,
    changePasswordInput,
    clickSubmit

  beforeEach(() => {
    handleSubmit = jest.fn()
    user = {username: 'michelle', password: 'smith'}
    utils = render(<Login onSubmit={handleSubmit} />)
    changeUsernameInput = value =>
      fireEvent.change(utils.getByLabelText(/username/i), {target: {value}})
    changePasswordInput = value =>
      fireEvent.change(utils.getByLabelText(/password/i), {target: {value}})
    clickSubmit = () => fireEvent.click(utils.getByText(/submit/i))
  })

  describe('when username and password is provided', () =>{
    beforeEach(() => {
      changeUsernameInput(user.username)
      changePasswordInput(user.password)
    })

    describe('when the submit button is clicked', () => {
      beforeEach(() => {
        clickSubmit()
      })

      it('should call onSubmit with the username and password', () => {
        expect(handleSubmit).toHaveBeenCalledTimes(1)
        expect(handleSubmit).toHaveBeenCalledWith(user)
      })
    })
  })

  describe('when the password is not provided', () => {
    beforeEach(() => {
      changeUsernameInput(user.username)
    })

    describe('when the submit button is clicked', () => {
      let errorMessage
      beforeEach(() => {
        clickSubmit()
        errorMessage = utils.getByRole('alert')
      })

      it('should show an error message', () => {
        expect(errorMessage).toHaveTextContent(/password is required/i)
      })
    })
  })

  describe('when the username is not provided', () => {
    beforeEach(() => {
      changePasswordInput(user.password)
    })

    describe('when the submit button is clicked', () => {
      let errorMessage
      beforeEach(() => {
        clickSubmit()
        errorMessage = utils.getByRole('alert')
      })

      it('should show an error message', () => {
        expect(errorMessage).toHaveTextContent(/username is required/i)
      })
    })
  })
})
```

For an example of why he thinks this, try to read this test in isolation.

``` javascript
it('should call onSubmit with the username and password', () => {
  expect(handleSubmit).toHaveBeenCalledTimes(1)
  expect(handleSubmit).toHaveBeenCalledWith(user)
})
```

What is `handleSubmit`? What is its value? Where is `user` cominf from? What it do? You can look all this stuff up, but your test isn't as easy to interpret as it seems. For the three tests it was used in, did you really save any space?

As a side node, we prefer to use the `test` function instead of the `it` function most of the time, but on the rare occasion we group with `describe`, we'll then use `it`. They're functionally interchangeable.

#### jest-in-case is good

``` javascript
import cases from 'jest-in-case'
import add from '../add'
cases(
 'add',
 ({first, second, result}) => {
   expect(add(first, second)).toBe(result)
 },
 [
   {first: 1, second: 2, result: 3},
   {first: 3, second: 4, result: 7},
   {first: 100, second: 2, result: 102},
 ],
)
```

### Documentation

Each component will have a corresponding page in GitHub’s Wiki. You can edit markdown files these using GitHub’s interface, or by cloning down the wiki repo with `git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.wiki.git` (this is created automatically when you first create a wiki page).

Please try to keep them up to date. At a minimum, the main page should involve installation and basic usage instructions, while each component page should outline props and functionality.

### Conclusion

Check out [@apmg/mimas v1.0.0](https://github.com/APMG/apm-mimas/wiki) or later for an idea of what this looks like in practice, keeping in mind that Mimas is tiny and there’s not much integration testing that can be done.

#### Blog Selections

* https://kentcdodds.com/blog/aha-testing
* https://kentcdodds.com/blog/testing-implementation-details
* https://kentcdodds.com/blog/avoid-nesting-when-youre-testing
* https://kentcdodds.com/blog/common-testing-mistakes
* https://kentcdodds.com/blog/demystifying-testing
* https://kentcdodds.com/blog/effective-snapshot-testing
* https://kentcdodds.com/blog/unit-vs-integration-vs-e2e-tests
* https://kentcdodds.com/blog/make-your-test-fail
* https://kentcdodds.com/blog/write-fewer-longer-tests
* https://kentcdodds.com/blog/write-tests
