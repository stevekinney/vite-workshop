---
title: Conditional Imports and Dynamic Imports
---

# Conditional Imports and Dynamic Imports

Conditional imports allow you to dynamically load different modules based on certain conditions, such as the current environment (development, production, etc.), the platform (browser, Node.js), or even custom conditions that you define.

Vite leverages JavaScript's dynamic `import()` syntax and some additional configuration options to make conditional imports possible.

### Basic Conditional Import Example

Here's a simple example of using a dynamic import based on a condition:

```ts
let module;

if (process.env.NODE_ENV === 'development') {
	module = import('./dev-module.js');
} else {
	module = import('./prod-module.js');
}

module.then(function (m) {
	console.log('Do something with the loaded module');
});
```

In this example, the module that gets loaded depends on the current environment.

### Environment-Based Conditional Imports

Vite exposes certain environment variables that can be used for conditional imports. For example, you can use `import.meta.env.MODE` to determine the current mode (`'development'`, `'production'`, etc.).

```ts
if (import.meta.env.MODE === 'development') {
	console.log('Import development-only module');
}
```

You can also define your own environment variables in a `.env` file and use them for conditional imports.

### Vite-Specific Conditional Import Features

Vite offers more advanced features like the `define` option, which lets you replace global variables at compile time:

```ts
export default {
	define: {
		__MY_CONDITION__: 'some value'
	}
};
```

Then, you can use this in your code to conditionally import modules:

```ts
if (__MY_CONDITION__ === 'some value') {
	console.log('Conditionally import something');
}
```

### Using Dynamic Import with `vite-plugin-dynamic-import`

While Vite doesn't offer built-in direct support for conditional imports in `import` statements, there's a third-party plugin called [`vite-plugin-dynamic-import`](https://www.npmjs.com/package/vite-plugin-dynamic-import) that provides such a feature.

```
npm install vite-plugin-dynamic-import
```

Then, add it to your `vite.config.js`:

```jsx
import dynamicImport from 'vite-plugin-dynamic-import';

export default {
	plugins: [dynamicImport()]
};
```

This plugin allows you to write conditional imports directly in the `import` statements based on conditions you define.

```jsx
import(`./content/${variable}.js`);
```
