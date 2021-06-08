---
title: Mdsvex Setup
abstract: 
keywords: 
categories: '[ Development ]'
weblogName: Weblog WP
postId: 5149
postDate: 2021-05-04T13:31:44.1945412+02:00
postStatus: publish
dontInferFeaturedImage: false
dontStripH1Header: false
author: Max
date: April 13, 2021 - 22:35
tags: '[ JS, Nwp-Components ]'
---

## Mdsvex

### Markdown for Svelte

**Config** `mdsvex.config.cjs`



<!-- pagebreak -->

<!--wp-->
<!--more-->





```javascript
/* ---------------------------- mdsvex.config.cjs --------------------------- */

const { join } = require("path");
const path_to_layout = join(__dirname, "./src/lib/Layout.svelte");

module.exports = {
	layout: path_to_layout,
	extensions: [".svx", ".md"],
	smartypants: {
		dashes: "oldschool",
	},
	remarkPlugins: [
		[require("remark-github"), {
			// Use your own repository
			repository: "https://github.com/svelte-add/mdsvex.git",
		}],
		require("remark-abbr"),
	],
	rehypePlugins: [
		require("rehype-slug"),
		[require("rehype-autolink-headings"), {
			behavior: "wrap",
		}],
	],
};
```

#### Layout (Tailwind)

```html
<script>
    export let title;
    export let author;
    export let date;
</script>

<style>
    /* your styles go here */
</style>

<div class="flex flex-col h-full px-4">
    <header class="p-4 mt-2 border rounded-lg text-center text-gray-600">
        <nav class="flex justify-between">
            <span>{title ? title : ''}</span><span class="text-lg text-gray-600">nwp-cgn </span>
        </nav>
    </header>
    <article class="flex-grow border rounded-lg mt-2 mb-4 px-4 py-2">
        <slot></slot>
    </article>
</div>
```