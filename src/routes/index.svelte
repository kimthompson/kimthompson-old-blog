<script context="module">
export function preload({ params, query }) {
  return this.fetch(`blog.json`).then(r => r.json()).then(posts => {
    return { posts };
  });
}
</script>

<script>
export let posts;
</script>

<style>
h1 {
  margin: 1em 0;
}

h2,
.post-item-footer {
  font-family: var(--main-header-font);
  font-weight: 700;
}

.container {
  padding-left: 25px;
}

.post-item-date {
  color: var(--main-theme-color);
  text-align: left;
  text-transform: uppercase;
  margin-right: 16px;
}

hr {
  margin: 60px auto;
}

.container {
  padding-bottom: 1em;
}
</style>

<svelte:head>
  <title>Kim Thompson</title>
</svelte:head>

<div class="container">
  <h1>Blog</h1>
  {#each posts as post, index}
    {#if index}
      <hr />
    {/if}
    <div class="post-item">
      <h2>
        <a rel='prefetch' href='blog/{post.slug}'>{post.title}</a>
      </h2>
      <p>{post.excerpt}</p>
      <div class="post-item-footer">
        <span class="post-item-date">— {post.printDate}</span>
      </div>
    </div>
  {/each}
</div>
