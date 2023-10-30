---
title: Import Meta
---

# Import Meta

The `import.meta` object is a meta-property that provides metadata about the module in which it appears. It's a feature of JavaScript modules that is particularly useful in the context of Vite.

In Vite, `import.meta` serves multiple purposes and allows you to write more dynamic and context-aware code. Here are some ways `import.meta` is commonly used:

### Environment Variables

You can access environment variables in your Vite project through `import.meta.env`. Variables prefixed with `VITE_` in your `.env` files are exposed to your code via `import.meta.env`.

```javascript
console.log(import.meta.env.VITE_API_URL); // Outputs: "https://myapi.com"
```

### Hot Module Replacement (HMR)

Vite uses `import.meta.hot` for Hot Module Replacement, allowing you to replace modules without reloading the entire page. This is essential for a fast development experience.

```javascript
if (import.meta.hot) {
	import.meta.hot.accept(['./module.js'], (modules) => {
		// Handle the updated modules here
	});
}
```

### Module URL

`import.meta.url` provides the URL of the current module, which can be useful for dynamic imports or working with assets.

```javascript
const moduleUrl = new URL('some-asset.png', import.meta.url);
```

### Glob Import

Vite extends `import.meta` to add a globbing feature, which allows you to import multiple modules with a single statement.

```javascript
import.meta.glob('./dir/*.js'); // Returns an object mapping paths to import() functions
```

### Plugins and Custom Properties

Some Vite plugins extend `import.meta` with custom properties. For example, a plugin might inject a version number:

```javascript
console.log(import.meta.VERSION); // Outputs: "1.0.0", if the plugin sets this property
```

### Production vs Development

Keep in mind that while `import.meta` provides a great development experience, not all its properties may be directly usable in production. Vite handles this by replacing or polyfilling some of the `import.meta` features during the production build, where it uses Rollup.

For example, `import.meta.env` variables are statically replaced during the production build, and `import.meta.hot` is removed since it's not needed in production.

Given your interest in both teaching and technology, understanding `import.meta` in the context of Vite could provide a rich topic to cover in a teaching module. It's a feature that embodies many aspects of modern JavaScript development, from environment configuration to module loading strategies.

Would you like to go deeper into any of these aspects?
