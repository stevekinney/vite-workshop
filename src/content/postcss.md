---
title: PostCSS
---

# Usage with PostCSS

- Auto-detection of valid PostCSS configurations
- All imported CSS will be processed by PostCSS
- Minification runs after PostCSS, uses `build.cssTarget` option

Vite supports PostCSS, a CSS preprocessor and post-processor, out of the box.

- You can configure PostCSS and add plugins to your project by modifying the `postcss.config.js` file in your project directory.
- This allows you to apply transformations to your CSS, such as autoprefixing, nesting, and custom property handling.

```javascript
// postcss.config.js
module.exports = {
	plugins: {
		'postcss-preset-env': {}
		// Add other PostCSS plugins here
	}
};
```
