---
title: Vite Plugins
---

# Vite Plugins

Writing a Vite plugin can be a powerful way to extend Vite's functionality or integrate it with other tools and workflows. Below is a comprehensive guide that covers everything you need to know to get started with writing a Vite plugin:

## Understanding Vite Plugins

- Vite plugins are objects or factory functions that adhere to the Rollup Plugin Interface, with some additional Vite-specific hooks.
- Plugins in Vite can perform tasks like modifying initial configuration, transforming imports, adding custom assets, and more.

## Setting Up a Vite Project

1. Install Vite if you haven't already:

```
npm install -g create-vite
```

2. Create a new Vite project:

```
npm init vite@latest my-vite-project --template react
```

3. Navigate to the project directory:

```
cd my-vite-project
```

# Initial Plugin Structure

A basic Vite plugin can be an object with properties that define its functionality. It can also be a factory function returning such an object, allowing for configuration options.

Example:

```js
// my-plugin.js
export default function myPlugin(options = {}) {
	return {
		name: 'my-plugin',
		transform(code, id) {
			// Your transformation logic
		}
	};
}
```

# Adding Your Plugin to the Vite Configuration

Add your plugin in `vite.config.js`:

```js
// vite.config.js
import myPlugin from './my-plugin.js';

export default {
	plugins: [
		myPlugin({
			/* options */
		})
	]
};
```

# Vite Lifecycle Hooks

- **Universal Hooks**: Common Rollup hooks that work in Vite too, like `transform`, `resolveId`, `load`, etc.
- **Vite Specific Hooks**: Unique to Vite like `configResolved`, `configureServer`, etc.

## Example of Universal Hook

```js
{
  name: 'universal-hook-example',
  load(id) {
    // Hook logic
  }
}
```

## Example of Vite Specific Hook

```js
{
  name: 'vite-specific-hook-example',
  configResolved(config) {
    // Hook logic
  }
}
```
