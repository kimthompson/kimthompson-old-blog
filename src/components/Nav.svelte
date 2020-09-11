<script>
  export let segment;
</script>

<style>
  nav {
    display: flex;
    flex-direction: column;
    flex: 1;
    text-transform: uppercase;
  }

  a {
    color: inherit;
    text-decoration: none;
    padding: 4px;
    display: block;
    position: relative;
    max-width: 8em;
  }

  a:not(.selected) {
    opacity: 0.7;
  }

  a::before {
    content: '';
    position: absolute;
    transition: transform .3s ease;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 2px;
    background: #aaa;
    transform: scaleX(0);
  }

  a:hover::before,
  .selected::before {
    transform: scaleX(1);
  }

  .selected::before {
    background: #fd6378;
  }
</style>

<nav>
  <a rel=prefetch class='{segment === undefined ? "selected" : ""}' href='.'>home</a>
  <a class='{segment === "about" ? "selected" : ""}' href='about'>about</a>
  <a class='{segment === "portfolio" ? "selected" : ""}' href='portfolio'>portfolio</a>
</nav>
