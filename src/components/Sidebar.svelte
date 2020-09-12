<script>
import Nav from '../components/Nav.svelte'
import Icon from 'svelte-awesome';
import { github, twitter, youtube, twitch, linkedin } from 'svelte-awesome/icons';

export let segment
</script>

<style>
img {
  height: 200px;
  -webkit-animation: wobble 3s linear infinite;
  -moz-animation: wobble 3s linear infinite;
  animation: wobble 3s linear infinite;
  padding-top: 10px;
}

@-moz-keyframes wobble {
  0% { -moz-transform: rotate(20deg); }
  50% { -moz-transform: rotate(-10deg); }
  100% { -moz-transform: rotate(20deg); }
}

@-webkit-keyframes wobble {
  0% { -webkit-transform: rotate(20deg); }
  50% { -webkit-transform: rotate(-10deg); }
  100% { -webkit-transform: rotate(20deg); }
}

@keyframes wobble {
  0% {
    -webkit-transform: rotate(20deg);
    transform: rotate(20);
  }
  50% {
    -webkit-transform: rotate(-10deg);
    transform: rotate(-10);
  }
  100% {
    -webkit-transform: rotate(20deg);
    transform: rotate(20);
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
  background-color: #D2CCA1;
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

<aside class="sidebar">
  <figure>
    <img alt='Me, being grumpy and getting caffeine' src='grump.png'>
    <figcaption>Art by <a href="https://www.instagram.com/lady_red_art/" target="_blank">@lady_red_art</a> on Instagram</figcaption>
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
