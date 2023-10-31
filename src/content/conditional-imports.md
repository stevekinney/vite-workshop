---
title: Conditional Imports
---

# Conditional Imports

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
	// Do something with the loaded module
});
```

In this example, the module that gets loaded depends on the current environment.

### Environment-Based Conditional Imports

Vite exposes certain environment variables that can be used for conditional imports. For example, you can use `import.meta.env.MODE` to determine the current mode (`'development'`, `'production'`, etc.).

```ts
if (import.meta.env.MODE === 'development') {
	// Import development-only module
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
	// Conditionally import something
}
```

### Using Dynamic Import with `vite-plugin-conditional-import`

While Vite doesn't offer built-in direct support for conditional imports in `import` statements, there's a third-party plugin called `vite-plugin-conditional-import` that provides such a feature.

```
npm install vite-plugin-conditional-import
```

Then, add it to your `vite.config.js`:

```ts
import ConditionalImport from 'vite-plugin-conditional-import';

export default {
	plugins: [ConditionalImport()]
};
```

This plugin allows you to write conditional imports directly in the `import` statements based on conditions you define.

### Why They're Cool

Conditional imports can be good for:

- Code splitting: Only load the code you need, when you need it.
- Environment-specific behavior: Use different modules for development and production.
- Platform-specific code: Use different modules for different platforms (browser, Node.js, etc.).
