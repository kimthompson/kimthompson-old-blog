<script>
import Nav from '../components/Nav.svelte'

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
}

.sidebar {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 300px;
  text-align: center;
  background-color: #757780;
}

@media(max-width: 1020px) {
  img {
    padding: 0;
  }

  .sidebar {
    flex-direction: row;
    width: 100%;
    border: none;
    padding: 10px;
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
  }

  h1 {
    margin: 0;
  }

  p {
    margin: 0;
  }
}
</style>

<aside class="sidebar">
  <figure>
    <img alt='Me, being grumpy and getting caffeine' src='grump.png'>
    <figcaption>Art by <a href="https://www.instagram.com/lady_red_art/" target="_blank">@lady_red_art</a> on Instagram</figcaption>
  </figure>

  <div class="title">
    <h1>Kim Thompson</h1>
    <p>Web Developer</p>
  </div>

  <div class="nav">
    <Nav {segment}/>
  </div>
</aside>
