---
title: Testing @ MPR
date: 2020-10-12T21:00:00.000Z
---

I wrote this for my team earlier this year to ensure that we were all on the same page regarding testing. Nobody on my team really had strong opinions other than 1) we should be doing more and 2) they should all follow a similar approach. In light of that, I watched Kent Dodd's two FEM courses, read all his testing blog posts and synthesized what I learned into this lightweight guide.

<!-- more -->

# Testing @ MPR

## A Distillation and Bastardization of the Scattered Teachings of Kent Dodds

The goal of this rulebook is to set out in writing what it means for one of our libraries to be well tested. This is what we have decided we need to feel confident that our code works and we won't push out any breaking changes.

### The Testing Trophy

#### Terminology & Definitions

Dodds' "testing trophy" diagram lays out the confidence gained in each stage of testing, with cost and difficulty increasing the higher you go. My thought was that we should keep doing what we're doing for static testing, ensure that our unit tests follow all the rules I'll outline later, and try to expand on integration testing where we can, since that is where the most confidence can be gained for the least work.

![Testing Trophy](blog/testing-trophy.jpg)

Here is what we are doing/can implement soon for each of these stages:

#### Static

We use ESLint, Sasslint, PropTypes, and Prettier. Dodds recommends Flow or TypeScript to force JavaScript, but Flow is basically dead and TypeScript is more of an intense lift for our apps that we likely want to spring for right now. (Note from the future: We started doing new development in TypeScript in August)

#### Unit

This comprises most of the tests we've written so far. Here's an example how to unit test a bit of UI, from one of Dodd's blog posts:

```js
import '@testing-library/jest-dom/extend-expect';
import React from 'react';
import { render } from '@testing-library/react';
import ItemList from '../item-list';

// Some people don't call these a unit test because we're rendering to the DOM with React.
// They'd tell you to use shallow rendering instead.
// When they tell you this, send them to https://kcd.im/shallow

test('renders "no items" when the item list is empty', () => {

})
```
