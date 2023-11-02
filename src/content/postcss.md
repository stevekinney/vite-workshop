---
title: PostCSS
---

# Usage with PostCSS

Vite supports [PostCSS](https://postcss.org/) out of the box. There is basically nothing that you need to do on your end.

Here is a list of a bunch of [PostCSS plugins](https://postcss.org/docs/postcss-plugins) that you can use.

All you need to do is create a `postcss.config.cjs` file and Vite will pick it up automatically.

Let's take it for a spin. First, let's grab a plugin.

```
npm install -D postcss-nested
```

Then let's configure `postcss.config.cjs`.

```js
module.exports = {
	plugins: {
		['postcss-nested']: {}
	}
};
```

## Configuring Vite and Supporting Source Maps

I was going to wait a little bit to talk about configuring Vite, but let's dip our toes in for a quick minute.

So far, we haven't confiugured Vite at all—and it hasn't really complained. But maybe I want some source maps with my PostCSS and I want to configure that.

I can add a file called `vite.config.js` (or, `vite.config.ts` and any of the various other extensions).

```js
import { defineConfig } from 'vite';

export default defineConfig({
	css: {
		postcss: {
			map: true
		}
	}
});
```

I use `defineConfig` to have TypeScript help me out under the hood. But I _could_ just return the object as well.

## Tasting Notes

- Auto-detection of valid PostCSS configurations
- All imported CSS will be processed by PostCSS
- Minification runs after PostCSS, uses `build.cssTarget` option

Vite supports PostCSS, a CSS preprocessor and post-processor, out of the box.

- You can configure PostCSS and add plugins to your project by modifying the `postcss.config.js` file in your project directory.
- This allows you to apply transformations to your CSS, such as autoprefixing, nesting, and custom property handling.

```js
// postcss.config.js
module.exports = {
	plugins: {
		'postcss-preset-env': {}
		// Add other PostCSS plugins here
	}
};
```

Finally, let's write a style using the nested syntax.

```css
button {
	background-color: #4caf50;
	color: white;
	&:hover {
		background-color: #3e8e41;
	}
}
```

If we look in our browser, we'll see that PostCSS has transpiled our code into regular 'ol CSS.
