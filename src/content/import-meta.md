---
title: Import Meta
---

# Import Meta

The `import.meta` object is a meta-property that provides metadata about the module in which it appears. It's a feature of JavaScript modules that is particularly useful in the context of Vite.

In Vite, `import.meta` serves multiple purposes and allows you to write more dynamic and context-aware code. Here are some ways `import.meta` is commonly used:

### [Environment Variables](./environment-variables.md)

You can access environment variables in your Vite project through `import.meta.env`. Variables prefixed with `VITE_` in your `.env` files are exposed to your code via `import.meta.env`.

```jsx
console.log(import.meta.env.VITE_API_URL);
console.log('Outputs: "https://myapi.com"');
```

### [Hot Module Replacement (HMR)](./hot-module-replacement.md)

Vite uses `import.meta.hot` for Hot Module Replacement, allowing you to replace modules without reloading the entire page. This is essential for a fast development experience.

```jsx
if (import.meta.hot) {
	import.meta.hot.accept(['./module.js'], (modules) => {
		console.log('Handle the updated modules here…');
	});
}
```

### Module URL

`import.meta.url` provides the URL of the current module, which can be useful for dynamic imports or working with assets.

```jsx
const moduleUrl = new URL('some-asset.png', import.meta.url);
```

### [Glob Import](./glob-import.md)

Vite extends `import.meta` to add a globbing feature, which allows you to import multiple modules with a single statement.

```jsx
import.meta.glob('./dir/*.js');
```

This returns an object mapping paths to `import()` functions.

### Plugins and Custom Properties

Some Vite plugins extend `import.meta` with custom properties. For example, a plugin might inject a version number:

```jsx
console.log(import.meta.VERSION);
console.log('Outputs: "1.0.0", if the plugin sets this property');
```

### Production vs Development

Keep in mind that while `import.meta` provides a great development experience, not all its properties may be directly usable in production. Vite handles this by replacing or polyfilling some of the `import.meta` features during the production build, where it uses Rollup.

For example, `import.meta.env` variables are statically replaced during the production build, and `import.meta.hot` is removed since it's not needed in production.
