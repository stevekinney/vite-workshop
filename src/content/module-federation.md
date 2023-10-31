---
title: Module Federation
---

# Module Federation

[Module Federation](https://github.com/module-federation) (which I am pretty sure [a term that the Webpack team made up](https://webpack.js.org/concepts/module-federation/)) allows you to dynamically run code from multiple different bundles at runtime, essentially letting different JavaScript applications share code without the need for package installations or versioning conflicts.

It's a feature mainly associated with Webpack 5, but you can also achieve similar functionality with Vite, a build tool that aims to provide a faster and leaner development experience.

### Why Vite?

Vite offers fast development, lean builds, and has a simple config API. It also comes with features like Hot Module Replacement (HMR) out of the box. Though Vite doesn't natively support Module Federation like Webpack 5, plugins are available to enable this functionality.

### Adding Module Federation Plugin to Vite

You'll need to add a Vite plugin to enable Module Federation. One such plugin is `vite-plugin-module-federation`. Install it as a dependency:

```bash
npm install vite-plugin-module-federation --save-dev
```

Now, add it to your Vite config. Create or modify `vite.config.js` as follows:

```javascript
import { defineConfig } from 'vite';
import ModuleFederation from 'vite-plugin-module-federation';

export default defineConfig({
	plugins: [
		ModuleFederation({
			name: 'fancy-design-system',
			filename: 'remoteEntry.js',
			exposes: {
				'./button': './src/components/button.tsx'
			}
		})
	]
});
```

### Consuming a Federated Module

Now that we've exposed some modules, let's see how to consume them in another Vite project. Create another Vite project as outlined earlier.

Next, update its `vite.config.js` to consume the federated module:

```javascript
import { defineConfig } from 'vite';
import ModuleFederation from 'vite-plugin-module-federation';

export default defineConfig({
	plugins: [
		ModuleFederation({
			remotes: {
				['fancy-design-system']: 'fancy-design-system@http://localhost:3000/remoteEntry.js'
			}
		})
	]
});
```

### Importing the Federated Module

In your application code, you can now dynamically import the federated module:

```javascript
const Button = import('fancy-design-system/button');
```

### Running the Projects

Start both projects with `npm run dev` and navigate to their respective URLs to see Module Federation in action.

### Caveats and Considerations

- Ensure both projects are running during development to properly fetch the federated modules.
- Keep track of versioning; though Module Federation aims to resolve versioning issues, it's not foolproof.
