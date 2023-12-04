---
title: Vite Configuration
---

# Vite Configuration

Configuring Vite involves tweaking settings in a `vite.config.js` file at the root of your project. This configuration file allows you to control various aspects of your development and production build processes.

## Basic Structure

Here's a basic `vite.config.js` to start:

```jsx
import VitePlugin from 'some-vite-plugin';

export default {
	plugins: [VitePlugin()],
	server: {
		port: 8080
	},
	build: {
		outDir: 'dist'
	}
};
```

## Important Fields

### `plugins`

An array of Vite plugins to be used. Plugins can affect how Vite bundles your code, handles assets, or even injects new features.

```jsx
import ViteReact from '@vitejs/plugin-react';
import ViteVue from '@vitejs/plugin-vue';

export default {
	plugins: [ViteReact(), ViteVue()]
};
```

### `root`

Specifies the root directory for a project. It defaults to the location of the `vite.config.js` file.

```jsx
export default {
	root: './src'
};
```

### `resolve`

Customize how Vite resolves modules. For example, to add custom aliasing:

```jsx
export default {
	resolve: {
		alias: {
			'@': '/src'
		}
	}
};
```

### `publicDir`

Specifies the directory for static assets. The default is the `public` directory.

```jsx
export default {
	publicDir: 'static-assets'
};
```

### `server`

Configuration related to the development server.

```jsx
export default {
	server: {
		port: 8080,
		proxy: {
			'/api': 'http://localhost:3001'
		}
	}
};
```

### `build`

Controls how your project is built for production.

```jsx
export default {
	build: {
		outDir: 'dist',
		rollupOptions: {}
	}
};
```

### `optimizeDeps`

Used for handling dependencies that need special treatment for optimization. For instance, to pre-bundle certain dependencies:

```jsx
export default {
	optimizeDeps: {
		include: ['lodash']
	}
};
```

### `define`

Used to replace variables in code during bundling. For example, to replace `process.env.NODE_ENV`:

```jsx
export default {
	define: {
		'process.env.NODE_ENV': '"production"'
	}
};
```

### `css`

CSS-related options, such as PostCSS plugins, can be configured here.

```jsx
export default {
	css: {
		postcss: {
			plugins: [require('autoprefixer')]
		}
	}
};
```

### Modes and Environment Variables

Vite supports environment variables and different modes (`development`, `production`, etc.). You can also create `.env` files that Vite will load depending on the mode.

### Extend with Plugins

Vite's ecosystem allows extending its functionality by using plugins, which can be essential for handling specific tasks like image optimization, linting, or even integrating with other build tools.

### TypeScript Support

Vite has first-class TypeScript support, and you can even write your `vite.config.js` as a TypeScript file (`vite.config.ts`).

### API Configurations

Vite also exposes a JavaScript API for more advanced configurations. This allows you to, for example, programmatically start the Vite development server with custom settings.

```jsx
import { createServer } from 'vite';

async function startServer() {
	const vite = await createServer({});
	await vite.listen();
}
```

### `base`

Defines the base public path when served in development or production. Useful for deploying to subdirectories.

```jsx
export default {
	base: '/subdirectory/'
};
```

### `publicDir`

Specifies the folder to serve as the root for the dev server and to be copied to the root of the `dist` directory during the build.

```jsx
export default {
	publicDir: 'public'
};
```

### `build`

Contains options for the build process, such as `rollupOptions`, `target`, `outDir`, and more. For example, you can control how CSS code-splitting works:

```jsx
export default {
	build: {
		cssCodeSplit: true
	}
};
```

### `server`

Configuration options for the development server, such as `host`, `port`, `strictPort`, and `proxy`.

```jsx
export default {
	server: {
		port: 3000,
		proxy: {
			'/api': 'http://localhost:4000'
		}
	}
};
```

### `resolve`

Controls how module requests are resolved. You can define custom aliasing, extensions, and other options here.

```jsx
export default {
	resolve: {
		alias: {
			'@': '/src'
		}
	}
};
```

### `plugins`

Allows you to add an array of plugins to extend Vite's functionality. Vite plugins are based on Rollup plugins but with additional hooks and properties that are Vite-specific.

```jsx
import Vue from '@vitejs/plugin-vue';

export default {
	plugins: [Vue()]
};
```

### `css`

CSS-related options, such as modules and preprocessor options.

```jsx
export default {
	css: {
		preprocessorOptions: {
			scss: {
				additionalData: '@import "src/variables.scss";'
			}
		}
	}
};
```

### `jsx`

Controls JSX transformation, allowing you to specify the JSX factory, JSX fragment, or even disable JSX transformation.

```jsx
export default {
	jsx: {
		factory: 'h',
		fragment: 'Fragment'
	}
};
```

### `ssr`

Controls Server-Side Rendering (SSR) options, letting you specify an external file as the entry point for your server code and other settings.

```jsx
export default {
	ssr: {
		external: ['some-external-package'],
		noExternal: ['some-local-package']
	}
};
```
