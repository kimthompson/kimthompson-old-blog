<script>
  import marked from 'marked';
  import { slide } from 'svelte/transition';
  import Icon from 'svelte-awesome';
  import projects from '../data/projects';
  import { faCaretDown, faCaretUp } from '@fortawesome/free-solid-svg-icons';
</script>

<style>
  h2 {
    margin: 1em 1em .6em;
  }

  input[type="checkbox"] {
    display: none;
  }

  .title {
    margin: 0;
    padding: 1em;
    display: flex;
    justify-content: center;
  }

  .file {
    padding: 1em 1.5em;
    background-color: var(--sage-color);
    display: flex;
    align-items: center;
    justify-content: space-around;
  }

  .file_text {
    max-width: 850px;
  }

  .file_tab {
    display: flex;
    width: 100%;
    border: 0;
    align-items: center;
    justify-content: space-between;
    font-size: 1.3em;
    margin: 0;
    background-color: var(--main-theme-color);
  }

  .file_icon {
    color: var(--sage-color);
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: var(--main-theme-color);
    width: 150px;
    height: 150px;
    border-radius: 10px;
    flex-grow: 3;
    transition: 0.3s;
    padding-left: 15px;
  }

  .file_icon:hover {
    background-color: var(--rich-black-color);
  }

  @media(max-width: 850px) {
    .file {
      flex-direction: column;
    }
  }
</style>

<svelte:head>
  <title>Projects - Kim Thompson</title>
</svelte:head>

<div>
  <h1 class="title">Projects</h1>

  {#each projects as project, index}
    <div class="shadow">
      <label style={`background-color: var(${project.color})`} class="file_tab shadow">
        <input type="checkbox" bind:checked={project.isSelected}>
        <h2>
          {project.name}
          <Icon data={project.isSelected ? faCaretUp : faCaretDown} scale="2" />
        </h2>
      </label>
      {#if project.isSelected}
        <div transition:slide class="file">
          <div class="file_text">
            {@html marked(project.description)}
            <div class="file_me">{@html marked(project.myRole)}</div>
          </div>
          <a href={project.link !== null ? project.link : ''}>
            {#if project.icon !== null}
              <div style={`background-color: var(${project.color})`} class="file_icon">
                <Icon data={project.icon} scale="7" />
              </div>
            {/if}
          </a>
        </div>
      {/if}
    </div>
  {/each}
</div>
