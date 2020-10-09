<script>
  export let segment;
</script>

<style>
  nav {
    display: flex;
    flex-direction: column;
    flex: 1;
    text-transform: uppercase;
    font-family: 'Special Elite', serif;
  }

  a {
    color: inherit;
    text-decoration: none;
    padding: 9px 0 0 0;
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
    background: var(--grey-color);
    transform: scaleX(0);
  }

  a:hover::before,
  .selected::before {
    transform: scaleX(1);
  }

  .selected::before {
    background: var(--main-theme-color);
  }
</style>

<nav>
  <a rel=prefetch class='{segment === undefined ? "selected" : ""}' href='.'>home</a>
  <a class='{segment === "projects" ? "selected" : ""}' href='projects'>projects</a>
  <a class='{segment === "resume" ? "selected" : ""}' href='resume'>resume</a>
</nav>
