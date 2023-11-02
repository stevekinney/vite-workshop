---
title: Library Mode with Components
---

# Creating a Component Library

Okay, we saw how to do this with some basic code. Let's look what it would take to do it with some React components.

We're going to start with the [vite-components](https://github.com/stevekinney/vite-components) repository.

## Creating an Entry File

We need to give Vite an entry point for our library. I just want to export the components, so I'm going to create `src/components/index.ts`.

It's going to look something like this:

```js
export * from './button';
export * from './input';
```

## Add the Configuration

Let's start with something simple, like this:

```js
import { resolve } from 'node:path';
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react-swc';

const __dirname = new URL('.', import.meta.url).pathname;

export default defineConfig({
	plugins: [react()],
	build: {
		lib: {
			entry: resolve(__dirname, 'src/components/index.ts'),
			name: 'VeryFancyComponents',
			fileName: 'very-fancy-components'
		}
	}
});
```

And then we can run `npm run build`. And we _should_ see the following output (or something close to it).

```
dist/style.css                       0.59 kB │ gzip:  0.31 kB
dist/very-fancy-components.js       77.17 kB │ gzip: 19.25 kB
dist/style.css                       0.59 kB │ gzip:  0.31 kB
dist/very-fancy-components.umd.cjs  47.61 kB │ gzip: 14.54 kB
```

**Whoa**, 77.17kb is… a lot. That's because we managed to include all of React. Ideally, whoever is consuming this component has React, right?

So, let's call that out as an external dependency.

### Externalizing Dependencies

Rollup has an option for us. I'm going to tell it not to include all of the React stuff. If you use a different framework, this obviously be a little different, but the basic idea still applies.

```js
export default defineConfig({
	plugins: [react()],
	build: {
		lib: {
			entry: resolve(__dirname, 'src/components/index.ts'),
			name: 'VeryFancyComponents',
			fileName: 'very-fancy-components'
		},
		rollupOptions: {
			external: ['react', 'react-dom', 'react/jsx-runtime'],
			output: {
				globals: {
					react: 'React',
					'react-dom': 'ReactDOM'
				}
			}
		}
	}
});
```

```
dist/style.css                      0.59 kB │ gzip: 0.31 kB
dist/very-fancy-components.js       0.03 kB │ gzip: 0.05 kB
dist/style.css                      0.59 kB │ gzip: 0.31 kB
dist/very-fancy-components.umd.cjs  0.19 kB │ gzip: 0.16 kB
```

Much better.

## Include CSS Modules

You can directly import CSS modules in your TypeScript/JavaScript files. They will be bundled into your library.

## Generate TypeScript Types

Vite does not generate TypeScript types by default. You will have to include a TypeScript compilation step for type generation.

My first thought would be to try to use TypeScript's build-in compiler.

```
// package.json
{
	"scripts": {
		"build": "vite build && npm run build:types",
		"build:types": "tsc ./src/components/index.ts --jsx react --declaration --emitDeclarationOnly --noEmit false --outFile dist/index.d.ts"
	},
	"types": "dist/types/index.d.ts"
}
```

This is a recipe for sadness. Could I figure out how to fight with it? Sure. But, I'd rather use a plugin.

```
npm install -D vite-plugin-dts
```

And now we'll install the plugin in `vite.config.ts`:

```ts
import { resolve } from 'node:path';
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react-swc';
import dts from 'vite-plugin-dts';

const __dirname = new URL('.', import.meta.url).pathname;

export default defineConfig({
	plugins: [react(), dts()]
	// … more stuff
});
```

It works, but it creates a lot of files and directories.

Let's tweak that.

```ts
dts({
	include: ['src/components']
});
```

## A Special TypeScript Configuration

```
{
	"extends": "./tsconfig.json",
	"compilerOptions": {
		"outDir": "./dist/",
		"declaration": true,
		"declarationDir": "./dist"
	},
	"include": ["src/components/**/*.ts", "src/components/**/*.tsx"]
}
```

And now… it blows up. 😭 You'll likely see something like this:

```
src/components/button.tsx:4:20 - error TS2307: Cannot find module './button.module.css' or its corresponding type declarations.

4 import styles from './button.module.css';
                     ~~~~~~~~~~~~~~~~~~~~~

src/components/input.tsx:4:20 - error TS2307: Cannot find module './input.module.css' or its corresponding type declarations.

4 import styles from './input.module.css';
                     ~~~~~~~~~~~~~~~~~~~~
```

That's fine. Let's just tell TypeScript that it's okay.

In any `d.ts` file that makes you happy.

```ts
declare module '*.css';
```

### Injecting the CSS

Another day, another plugin.

```
npm install -D vite-plugin-lib-inject-css
```

```ts
export default defineConfig({
	plugins: [
		react(),
		libInjectCss(), // 👀
		dts({
			include: ['src/components']
		})
	],
	build: {
		copyPublicDir: false,
		cssCodeSplit: true, // 👀
		lib: {
			entry: resolve(__dirname, 'src/components/index.ts'),
			name: 'VeryFancyComponents',
			fileName: 'very-fancy-components',
			formats: ['es', 'umd']
		},
		rollupOptions: {
			external: ['react', 'react-dom', 'react/jsx-runtime'],
			output: {
				globals: {
					react: 'React',
					'react-dom': 'ReactDOM'
				}
			}
		}
	}
});
```

## Not Including the Public Directory

Just add the following configuration:

```
copyPublicDir: false,
```

## Adding Your Library to Your `package.json`

```
{
	"main": "./dist/very-fancy-components.umd.cjs",
	"module": "./dist/very-fancy-components.js",
	"types": "./dist/index.d.ts",
	"exports": {
		".": {
			"import": "./dist/very-fancy-components.js",
			"require": "./dist/very-fancy-components.umd.cjs",
			"types": "./dist/index.d.ts"
		}
	}
}
```
