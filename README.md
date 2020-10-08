# kimthompson.me

The website and blog for Kim Thompson, React developer by day and Svelte afficionado by night.

## Installation

Once you pull down this repo and install the packages with `npm i`, about the only command you should need is

`npm run dev`

This will run a development version of the site with HMR at http://localhost:3000. If you're curious about other commands or the rollup settings used here, you can check out the `package.json` and `rollup.config.js` files.

## How I Deploy

First, create an account with [https://vercel.com](Vercel) and install the Vercel package globally.

`npm i -g vercel`

Then use this nice little tool to automatically generate the `vercel.json` configuration you'll need for Sapper.

`npx vercel-sapper`

Finally, run the command `vercel` and follow the prompts. Log in and verify your email if it asks you to. You can then also set up this site to build and deploy automatically in Vercel every time you push to the master branch.

## Credits

I got this blog template from [Maxi Ferreira](https://www.twitter.com/Charca), and you can find it [here](https://github.com/Charca/sapper-blog-template)

## 🏗 Structure

The base structure of this template is the same as Sapper's [default template](https://github.com/sveltejs/sapper-template/). These are some of the new things you'll find here:

### src/routes/blog

This is the home of your blog. The most important files in here are:

- `_posts.js`: this module contains the logic for loading and parsing your markdown posts.
- `[slug].svelte`: this is the template of your blog post page.
- `index.svelte`: this is the template of your article list page.

### src/routes/blog/posts

This is where your markdown posts live in. All `.md` files in this directory are treated as blog posts and parsed automatically by the `_posts.js` module.

- The markdown file name becomes the post slug. For example `hello-world.md` becomes `http://localhost:3000/blog/hello-world`.
- Everything between the start of the post and the `<!-- more -->` tag becomes the article's "excerpt".
- Frontmatter properties supported are `title` and `date`.

## 🐛 Bugs and feedback

Sapper is in early development, and may have the odd rough edge here and there. Please be vocal over on the [Sapper issue tracker](https://github.com/sveltejs/sapper/issues).

