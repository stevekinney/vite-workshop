---
title: PostCSS
---

# Usage with PostCSS

Vite supports [PostCSS](https://postcss.org/) out of the box. There is basically nothing that you need to do on your end.

Here is a list of a bunch of [PostCSS plugins](https://postcss.org/docs/postcss-plugins) that you can use.

All you need to do is create a `postcss.config.cjs` file and Vite will pick it up automatically.

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
