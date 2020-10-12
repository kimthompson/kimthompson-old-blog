<script>
import Nav from '../components/Nav.svelte'
import Icon from 'svelte-awesome';
import { github, twitter, youtube, twitch, linkedin } from 'svelte-awesome/icons';

export let segment
</script>

<style>
img {
  height: 200px;
  padding-top: 10px;
}

img:hover {
  -webkit-animation: wobble .25s linear;
  -moz-animation: wobble .25s linear;
  animation: wobble .25s linear;
}

@-moz-keyframes wobble {
  0% { -moz-transform: rotate(3deg); }
  25% { -moz-transform: rotate(-3deg); }
  50% { -moz-transform: rotate(3deg); }
  75% { -moz-transform: rotate(-3deg); }
  100% { -moz-transform: rotate(3deg); }
}

@-webkit-keyframes wobble {
  0% { -webkit-transform: rotate(3deg); }
  25% { -webkit-transform: rotate(-3deg); }
  50% { -webkit-transform: rotate(3deg); }
  75% { -webkit-transform: rotate(-3deg); }
  100% { -webkit-transform: rotate(3deg); }
}

@keyframes wobble {
  0% {
    -webkit-transform: rotate(3deg);
    transform: rotate(3);
  }
  25% {
    -webkit-transform: rotate(-3deg);
    transform: rotate(-3);
  }
  50% {
    -webkit-transform: rotate(3deg);
    transform: rotate(3);
  }
  75% {
    -webkit-transform: rotate(-3deg);
    transform: rotate(-3);
  }
  100% {
    -webkit-transform: rotate(3deg);
    transform: rotate(3);
  }
}

figcaption {
  font-size: 10px;
  height: 10px;
}

h1 {
  font-size: 48px;
  min-height: 70px;
  margin: 0;
}

p {
  margin: 0;
}

.sidebar {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 300px;
  text-align: center;
  background-color: var(--sidebar-color);
  z-index: 1000;
}

.nav {
  margin-top: 30px;
  margin-bottom: 100px;
}

.center {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.social {
  margin-top: 10px;
  display: flex;
}

.icon {
  padding: 0 5px;
}

@media(max-width: 1020px) {
  img {
    padding: 0;
  }

  .sidebar {
    flex-direction: row;
    width: 100%;
    border: none;
    padding: 10px 10px 10px 25px;
    margin-bottom: 15px;
  }

  .title {
    flex: 4;
  }

  figure {
    flex: 2;
    order: 5;
  }

  .nav {
    order: -1;
    flex: 2;
    margin: 0;
  }
}
</style>

<aside class="sidebar shadow">
    <figure>
      <a href="/">
        <img alt='Me, being grumpy and getting caffeine' src='grump.png'>
      </a>
      <figcaption>Art by <a href="https://www.instagram.com/lady_red_art/" target="_blank">@lady_red_art</a></figcaption>
    </figure>

  <div class="center">
    <div class="title">
      <h1>Kim Thompson</h1>
      <p>Web Developer</p>
    </div>

    <div class="social">
      <a href="https://github.com/kimthompson" class="icon"><Icon data={github} scale="1.5" /></a>
      <a href="https://www.linkedin.com/in/kimberlyannthompson/" class="icon"><Icon data={linkedin} scale="1.5" /></a>
      <a href="https://www.youtube.com/channel/UCfXT3usekugleJdBo2LIjig" class="icon"><Icon data={youtube} scale="1.5" /></a>
      <a href="https://www.twitch.tv/kimicalburn" class="icon"><Icon data={twitch} scale="1.5" /></a>
      <a href="https://twitter.com/byKimThompson" class="icon"><Icon data={twitter} scale="1.5" /></a>
    </div>
  </div>

  <div class="nav">
    <Nav {segment}/>
  </div>
</aside>
