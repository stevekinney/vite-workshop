---
title: Create Vite Server
---

# `createViteServer`

The `createViteServer` function is part of Vite's Node.js API, allowing you to programmatically create a Vite development server. This can be particularly useful for integrating Vite into larger setups, for running Vite as part of tests, or for more advanced scenarios where you want to customize the development environment programmatically.

### Basic Usage

To get started, you first need to install Vite as a dependency:

```
npm install vite
```

Then you can import the `createViteServer` function and use it in your Node.js script:

```jsx
import { createServer as createViteServer } from 'vite';

async function start() {
	const vite = await createViteServer({
		/* Vite options here. */
	});
	const url = vite.config.server.https;
	console.log(`Vite server started at ${url}`);
}

start();
```

### Options

The `createViteServer` function takes an optional configuration object that allows you to specify Vite's behavior. These options are the same as what you can provide in a `vite.config.js` file:

```jsx
const vite = await createViteServer({
	plugins: [
		/* your plugins */
	],
	root: './src',
	server: {
		port: 8080,
		strictPort: true
	}
});
```

### API Methods

The returned `vite` object exposes several API methods that you can use to interact with the server:

- `vite.close()`: Closes the Vite development server.
- `vite.pluginContainer`: Access the underlying Vite plugins.
- `vite.moduleGraph`: Access Vite's internal module graph.
- `vite.ssrLoadModule`: Dynamically import a module with Vite's SSR logic applied.

And several more, allowing you to control and interact with the server programmatically.

### Use Cases

- **Testing**: You can write tests that spin up a Vite server, run some operations, and then shut it down.
- **Custom Development Environments**: Integrate Vite into larger, custom development setups.
- **Programmatic Builds**: Run build operations on-demand, based on certain events or triggers.
