---
title: Working with CSS
---

# Working with CSS

## CSS Importing

- Injection of `.css` files into a page via `<style>` tags
- Support for Hot Module Replacement (HMR)
- Retrieval of processed CSS as a string as the module's default export

## @import Handling

### Inlining and Rebasing

- Support for CSS `@import` inlining via postcss-import
- Vite aliases are respected for `@import`
- `url()` references are rebased automatically, ensuring correctness across different directories

### Aliases and URL Rebasing in Pre-processors

- Also available for Sass and Less
- Not supported for Stylus due to API constraints

## PostCSS

- Auto-detection of valid PostCSS configurations
- All imported CSS will be processed by PostCSS
- Minification runs after PostCSS, uses `build.cssTarget` option

## CSS Modules

- Files with `.module.css` are treated as CSS modules
- Returns a module object for classes
- Configuration via `css.modules` option
- Support for camelCase locals (`localsConvention: 'camelCaseOnly'`)

## CSS Pre-processors

### General

- Built-in support for `.scss`, `.sass`, `.less`, `.styl`, `.stylus`
- Must install the corresponding pre-processor
- Vue single-file components also supported

### @import Resolving

- Improved `@import` resolving for Sass and Less
- Vite aliases respected
- Relative `url()` references are rebased

### Modules with Pre-processors

- Support for `.module` prepended to file extension (e.g., `style.module.scss`)

## Disabling CSS Injection

- Control via `?inline` query parameter
- CSS string is returned but not injected into the page

## Experimental Features

### Lightning CSS

- Available starting Vite 4.4
- Enabled by adding `css.transformer: 'lightningcss'` to config
- Requires installation of `lightningcss` dependency

### Configuration

- `css.lightningcss` config option
- `css.lightningcss.cssModules` for CSS Modules
- `build.cssMinify: 'lightningcss'` for minification

### Limitations

- Doesn't support CSS Pre-processors

## Security and Deprecated Features

- Default and named imports from CSS files are deprecated, use `?inline` instead

## Further Research

By studying this comprehensive outline, you can gain a clear understanding of how Vite handles CSS, from basic imports to advanced configurations and experimental features.

CSS handling in Vite is quite flexible and caters to a wide range of CSS-related needs. Here's an overview of how Vite handles CSS, including support for CSS Modules, PostCSS, and preprocessors like SCSS:

1. **CSS Modules**: Vite offers native support for CSS Modules, which is a way to locally scope CSS class names to avoid global style conflicts.
   - When you create a CSS file with the `.module.css` extension, Vite automatically treats it as a CSS Module.
   - You can import and use CSS Modules in your JavaScript or Vue components, and the class names are scoped to the component.

```vue
<template>
	<div :class="$style.myComponent">This is my component</div>
</template>

<script>
import styles from './my-component.module.css';

export default {
	name: 'MyComponent'
	// ...
};
</script>
```

2. **PostCSS**: Vite supports PostCSS, a CSS preprocessor and post-processor, out of the box.
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

3. **SCSS and Other Preprocessors**: Vite also supports popular CSS preprocessors like SCSS, Less, and Stylus.
   - To use SCSS, for example, you can simply install the `sass` package and start writing `.scss` files in your project.
   - There's no need for additional configuration; Vite will process these files automatically.

```vue
<template>
	<div class="my-component">This is my component</div>
</template>

<style scoped lang="scss">
// You can use SCSS here
.my-component {
	background-color: #f0f0f0;
	padding: 20px;
}
</style>
```

In summary, Vite provides a versatile CSS handling system that includes support for CSS Modules, PostCSS for advanced transformations, and various CSS preprocessors like SCSS for enhanced styling capabilities. This flexibility allows developers to choose the CSS approach that best fits their project's requirements while benefiting from Vite's fast development and hot module replacement features.
