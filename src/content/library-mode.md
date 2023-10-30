---
title: Library Mode
---

# Library Mode

Outline:

- Basic usage
- Exporting types
- Exporting `.d.ts`
- Usage with a framework (Exercise where they do the basics)
- Show how to use `glob` to split up the CSS.
- Tweaks for publishing
  - Add `types` entry to `package.json`.
  - Set up the `peerDependencies`.
  - Set up `sideEffects` entry in `package.json`.
  - Set up a `prepublish` step.
- Multiple entries.
- Research: [`build.cssCodeSplit`](https://vitejs.dev/config/build-options.html#build-csscodesplit)

Library mode in Vite allows you to build your code as a reusable library. This is particularly useful when you want to create a package that can be shared across multiple projects, be it open source or for internal usage. In library mode, Vite will produce a bundle optimized to be used as an npm package or via a CDN as a global variable in the browser.

The biggest difference that you're going to notice is that because most libraries or other packages that you install via npm don't include—much less start from—an `index.html` file, you're going to need to provide Vite an entry point.

### Example Use Cases

- **Component Libraries**: Create reusable UI components.
- **Utility Libraries**: Offer a set of utility functions or classes.
- **Plugin Systems**: Create plugins for larger libraries or frameworks.

### Benefits of Using Library Mode

1. **Optimized Code**: Vite ensures the output is tree-shakeable and as minimal as possible.
2. **Multiple Formats**: Easily target different environments with various module formats.
3. **Customization**: Extensive customization possibilities through Rollup options.

## How to Use Library Mode

Let's start with a super simple example.

```ts
import { resolve } from 'path';
import { defineConfig } from 'vite';

export default defineConfig({
	build: {
		lib: {
			entry: resolve(__dirname, 'src/main.ts'),
			name: 'SuperCoolLibrary',
			fileName: 'super-cool-library'
		}
	}
});
```

If we run `npx vite build`, we'll see the following output:

```
dist/super-cool-library.mjs
dist/super-cool-library.umd.js
```

Some things to take note of:

1. Vite used the `fileName` setting to name the files.
2. Vite created two versions: a `.mjs` and a `.umd.js`.

The reason that we create two different files is because the JavaScript ecosystem is hard and we want to support both ES Modules as well as CommonJS modules.

**Quick experiment**: Go into your `package.json` and switch the type of the package to support ES Modules (e.g. add `"type": "module"` to your `package.json`). Run `npx vite build` again. What did you notice about the output?

Our `package.json` will do the heavy-lifting of helping to determine which of the two should be used depending on how the module is consumed. We might set up a simple `package.json` to look something like this:

```json
{
	"name": "super-cool-library",
	"type": "module",
	"files": ["dist"],
	"main": "./dist/super-cool-library.umd.cjs",
	"module": "./dist/super-cool-library.js",
	"exports": {
		".": {
			"import": "./dist/super-cool-library.js",
			"require": "./dist/super-cool-library.umd.cjs"
		}
	}
}
```

This is not-Vite-specific, but let's cover some quick terminology:

- `main`: The main field is a module ID that is the primary entry point to your program.
- `module`: An ECMAScript module ID that is the primary entry point to your program.
- `exports`: The module path that is resolved when this specifier is imported. Set to `null` to disallow importing this module.

## Supported Formats

We didn't specify what formats we wanted, so Vite used Rollup's defaults of `es` and `umd`. But, it will support any of the following:

```ts
export declare type LibraryFormats = 'es' | 'cjs' | 'umd' | 'iife';
```

That `name` field is only required if you're using the `umd` or `iife` formats. It's basically the name of the variable to be referenced in the output.

**Quick Experiment**: Get rid of the `umd` format and add in `cjs`. You can get rid of the `name` field while you're at it. Update your `package.json` accordingly.

## Building the Types

To make this a bit easier, we're going to pull in the [`vite-plugin-dts`](http://npm.im/vite-plugin-dts) plugin from npm.

```
npm i -D vite-plugin-dts
```

And we'll update our `vite.config.ts` accordingly.

```ts
export default defineConfig({
	plugins: [dts()],
	build: {
		lib: {
			entry: resolve(__dirname, 'src/main.ts'),
			fileName: 'super-cool-library',
			formats: ['es', 'cjs']
		}
	}
});
```

We can explore some more of [the options for `vite-dts-plugins`](https://github.com/qmhc/vite-plugin-dts#options).

Some notable options:

- `include` takes an array of directories that you want to include.
- `rollupTypes` rolls up all of the type declaration files after emitting them.
- `copyDtsFiles` copies any and all `.d.ts` files.

## External Dependencies

You don't necessarily want to include Svelte or React or Vue with your library as the consuming application has likely specified its own version of these dependencies.

We can define what _not_ to include using `rollupOptions.external`:

```ts
export default defineConfig({
	plugins: [dts()],
	build: {
		lib: {
			entry: resolve(__dirname, 'src/main.ts'),
			fileName: 'super-cool-library',
			formats: ['es', 'cjs']
		},
		rollupOptions: {
			external: ['react', 'react-dom']
		}
	}
});
```

## Including Styles

Now, if we have these React (or whatever) components, Vite is going to try to roll them all up—pun _unintended_—into one `style.css` file, which is sub-optimal for all of the code-splitting goodness that we've been after when another Vite application consumes it. Bummer.

We _could_ use [a plugin](https://www.npmjs.com/package/vite-plugin-lib-inject-css), I suppose.

```
npm i -D vite-plugin-lib-inject-css
```

## Next Steps

- Show how to use `glob` to split up the CSS.
- Add `types` entry to `package.json`.
- Set up the `peerDependencies`.
- Set up `sideEffects` entry in `package.json`.
- Set up a `prepublish` step.
- Multiple entries.
