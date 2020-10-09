<script>
  import marked from 'marked';
  import Icon from 'svelte-awesome';
  import { faNpm } from '@fortawesome/free-brands-svg-icons';
  import {
    faMobileAlt,
    faBaby,
    faMicrophoneAlt,
    faPodcast,
    faVial,
    faCubes,
    faDatabase,
    faVoteYea,
    faBroadcastTower,
    faGuitar,
    faCaretDown
  } from '@fortawesome/free-solid-svg-icons';
  import { faFileImage, faComment } from '@fortawesome/free-regular-svg-icons';

  let projects = [
    {
      name: 'Two React Native Apps',
      description: 'Our next two projects will be developed for Next.js, iOS and Android at the same time using React Native. These are the first projects at MPR to use TypeScript, which has made our code more rigorous.',
      myRole: 'I created the proof of concept, showing that apps created in React Native with Expo could do all of the things we would need an audio-heavy web app to do. I got everyone on board and excited about it.', 
      icon: faMobileAlt,
      link: null,
      isWip: true
    },
    {
      name: '@apmg/amat-native',
      description: 'Basically a copy of @amat/react that output React Native markup instead of normal React markup.',
      myRole: 'I copied @amat/react, gutted the project and started to rebuild from the ground up. I completed the basic scaffolding and most of the easier features, then published an alpha version on NPM. Now my coworkers and I are building out the rest, ticket by ticket.', 
      icon: faNpm,
      link: 'https://npmjs.com/package/@apmg/amat-native',
      isWip: true
    },
    {
      name: "Kids' Podcasts Site Engine",
      description: 'Podcast websites for children had very different layout and content requirements, to the point where it made sense to split them off into their own ecosystem with their own configuration file template.',
      myRole: "I did the initial clone and reorganization of the Podcasts Site Engine, using Julie's Library as the model.",
      icon: faBaby,
      link: 'https://julieslibraryshow.org',
      isWip: false
    },
    {
      name: 'Podcasts Site Engine',
      description: "A single engine upon which infinite podcast websites can be created, built with Next.js. Spinning up a website for a new podcast is as simple as buying the domain and filling out a configuration file with the needed commponents and assets. Uses React's Context API to figure out which config to use and, therefore, which site to show.",
      myRole: 'After proving that Next.js was the most reliable way for us to render React on the server, I ported this whole site over to Next.js from a custom webpack system. I also devised the Context API configuration system.',
      icon: faPodcast,
      link: 'https://ttfa.org',
      isWip: false
    },
    {
      name: "MPR's Testing Standards",
      description: "We had taken one course on testing together, and some of us had taken extra. There still ended up being a lot of confusion and disagreement over what constituted a 'good' test or 'enough' testing, and some of our projects recieved no testing at all.",
      myRole: "I didn't have strong opinions on how/what to test myself, but I at least wanted to get rid of the ambiguity. I retook Kent Dodd's testing course on Front End Masters once it got an update, taking detailed notes this time. I then pored over all of his blog posts and managed to condense my interpretation of his teachings into a single word doc, which I then walked my teammates through and pointed to from time to time during code review.",
      icon: faVial,
      link: '/blog/mpr-testing-standards',
      isWip: false
    },
    {
      name: "Titan — Library of React Components",
      description: 'For various things MPR uses over all their sites &mdash; teasers, hero banners, and so on &mdash; we decided to build them once and provide a number of customization options.',
      myRole: 'I was pretty involved in the initial organization of Titan, which was reverse engineered from a number of components we made for Live From Here that we thought would be more generally useful. About 18 months later, I successfully lobbied for time to write and/or reorganize tests and documentation for these components so that v1.0.0 could published.',
      icon: faCubes,
      link: 'https://npmjs.com/package/@apmg/titan',
      isWip: false
    },
    {
      name: 'Mimas — Easy Image Processing',
      description: "A React component that takes image data from our CMS and figures out which aspect ratio(s) and size(s) to deliver in a given situation. This libary, like Titan, is open source, though I don't see it having much utility outside of our CMS.",
      myRole: 'I created the first version of Mimas. About 18 months later, I successfully lobbied for time to write/reorganize tests and documentation for this library so that v1.0.0 could be published.',
      icon: faFileImage,
      link: 'https://npmjs.com/package/@apmg/mimas',
      isWip: false
    },
    {
      name: 'MPR.org → GraphQL API',
      description: "MPR.org, as well as a few of our other Rails sites that don't get a huge amount of traffic, were still relying on the old API that is on its way out. They also were a few versions of Rails behind.",
      myRole: 'I upgraded MPR.org to the latest version of Ruby and replaced their Presenter and Roar models with a lightweight system that used GraphQLi. I then showed my team how I did it, and my teammates then went off to do that to our other Rails sites.',
      icon: faDatabase,
      link: 'https://mpr.org',
      isWip: false
    },
    {
      name: 'Elections',
      description: 'A React website (not SSR for once!) that displays information about each election in Minnesota since November 2016.',
      myRole: "When 2018 rolled around, the site wasn't quite ready to handle all of the new races that cropped up, and the router was out of date enough that it was difficult hard to add the ability to switch years and impossible to upgrade React to 16.x and take advantage of features like Context and Hooks. So I rebootstrapped this site with CRA and migrated all the components, cleaning up and generalizing as I went.\n I then created our state legislature Balance of Power charts and, as the Leaflet plugin started to fail us, ported all of our election maps over to D3.js.",
      icon: faVoteYea,
      link: 'https://elections.mpr.org/2018-11-06/us/senate',
      isWip: false
    },
    {
      name: 'MPR News',
      description: 'A complete redesign and rebuild of MPR News, creating it in Next.js and React instead of Ruby on Rails.',
      myRole: "This was my second large project at MPR, and I hopped onto it sort of late after finishing up a number of followup bugs from Live From Here. Geoff had set up an SSR system with Webpack based on Razzle, and many parts of it weren't working. He spent a couple of weeks troubleshooting it, his questions on Stack Overflow remaining unanswered. I only had a couple of days of patience for that in me and asked if I could recreate the project thus far in Next.js as a proof-of-concept. My approach eventually won out and ended up being used in quite a few other places.",
      icon: faBroadcastTower,
      link: 'https://mprnews.org',
      isWip: false
    },
    {
      name: 'Live From Here',
      description: 'A site launch for _Live From Here_, the program that replaced _A Prairie Home Companion_. One of the last sites we built with a Rails back end and a React front end.',
      myRole: 'This was my first large project at MPR and my first eveer project with React. I found it pretty easy to pick up and ended up enjoying it more than Vue by the end of this project (though that was hard to admit). I was primarily to work with Node.js, React and Rails, but this project ended up having way more styling work than anticipated. My manager was immensely relieved to discover that I already knew SCSS and immediately able to jump in and help with those tickets instead.', 
      icon: faGuitar,
      link: 'https://livefromhere.org',
      isWip: false
    },
    {
      name: 'Classical 24',
      description: 'A lightweight relaunch of our simple Classical 24 website, done in Rails and Vue.',
      myRole: "This was a tutorial project where my manager didn't even care if I used React: he just wanted me to get used to bootstrapping a Rails project and using our APIs. I had limited capacity to change up the logo or design since MPR is not the sole owner of this property. I opted to use Vue to reduce the learning curve for this project and get it done in a week. I turned a four page website into one updating page, and my revamp was of a high enough quality that it got published. The backend team was able to shut down one more ancient site. 🎉",
      icon: faMicrophoneAlt,
      link: 'https://classical24.org',
      isWip: false
    },
    {
      name: "😭 NDAs 😭",
      description: "Amn't allowed to speak of anything I did for Design Center or Ameriprise Financial except in the vaguest and most general of ways. I get it though.",
      myRole: 'Various projects with Swift, Objective-C, C#, Xamarin 🤢, Backbone.js, HTML and CSS.',
      icon: null,
      link: 'https://en.wikipedia.org/wiki/Non-disclosure-agreement',
      isWip: false
    }
  ]
</script>

<style>
  .title {
    display: flex;
    justify-content: center;
  }

  .file {
    background-color: var(--sage-color);
  }

  .file_tab {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 1.3em;
    background-color: var(--main-theme-color);
    padding: 25px 10px 20px;
    margin: 0;
  }

  .file_description {
    margin: 0 10px;
  }

  .file_me {
    padding: 0 5px;
    display: flex;
    align-items: center;
  }

  .file_me p {
    font-style: italic;
    flex-grow: 5;
    margin: 0 50px 0 25px;
  }

  .file_icon {
    flex-grow: 3;
    min-width: 100px;
  }

  @media(max-width: 500px) {
    .file_icon {
      display: none;
    }

    .file_me p {
      margin: 0 25px;
    }
  }
</style>

<svelte:head>
  <title>Projects</title>
</svelte:head>

<div>
  <h1 class="title">Projects</h1>

  {#each projects as project, index}
    <div class="file">
        <h2 class="file_tab">
          {project.name}
          <Icon data={faCaretDown} scale="2" />
        </h2>
        <p class="file_description">{@html marked(project.description)}</p>
        <div class="file_me">
          <p>{@html marked(project.myRole)}</p>
          <a href={project.link !== null ? project.link : ''}>
            {#if project.icon !== null}
              <div class="file_icon">
                <Icon data={project.icon} scale="3" />
              </div>
            {/if}
          </a>
        </div>
    </div>
  {/each}
</div>
