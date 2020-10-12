<script>
  export let project;
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
    margin: 0;
    width: 100%;
    border: 0;
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

  .hidden {
    display: none;
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

<div class="file">
  <button class="file_tab" on:click={handleExpand}>
    <h2>
      {project.name}<Icon data={faCaretDown} scale="2" />
    </h2>
  </button>
  <p class="file_description">{@html marked(project.description)}</p>
  <div class="file_me hidden">
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
