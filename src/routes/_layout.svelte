<script>
import Sidebar from '../components/Sidebar.svelte'

export let segment;
</script>

<style>
.layout {
  display: flex;
  flex-direction: column;
  min-height: 100%;
  min-height: 100vh;
}

.layout_main {
  display: flex;
}

main {
  flex: 1;
  position: relative;
  margin: 0 auto;
  background-color: white;
  padding: 1em 2em;
  box-sizing: border-box;
  width: 100%;
  display: flex;
  flex-direction: column;
}

footer {
  color: #aaa;
  background-color: #090809;
  font-size: 1em;
  font-family: 'Cabin Sketch', sans-serif;
  padding: 1em 2em;
  text-align: center;
  width: 100%;
}

@media(max-width: 1020px) {
  .layout_main {
    flex-direction: column;
  }
}
</style>

<div class="layout">
  <div class="layout_main">
    <Sidebar {segment}/>

    <main>
      <slot></slot>
    </main>
  </div>
  <footer>
    <span>
      &copy; {new Date().getFullYear()} Kim Thompson.
      Powered by <a href="https://sapper.svelte.dev" target="_blank">Sapper</a>.
      Template by <a href="https://www.twitter.com/Charca" target="_blank">Maxi Ferreira</a>.
    </span>
  </footer>
</div>
