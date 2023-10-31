---
title: ESBuild Options
---

# ESBuild Options

The `esbuild` option within Vite's `optimizeDeps` configuration allows you to pass custom options directly to esbuild, the tool Vite uses for fast dependency pre-bundling. This can be useful for advanced scenarios where you need fine-grained control over the optimization process.

Here's a simple example:

```js
// vite.config.js
export default {
	optimizeDeps: {
		esbuild: {
			// esbuild options
			target: 'es2020' // specify the target environment
		}
	}
};
```

## Commonly Used Esbuild Options

Here are some esbuild options that might be useful in the context of `optimizeDeps`:

1. **`target`**: Specifies the ECMAScript version to target. This could be a string like 'es2015', 'es2020', or an array of multiple targets. The default is usually 'esnext'.
2. **`jsxFactory` and `jsxFragment`**: Useful if you are optimizing a React library or component and you want to specify a custom JSX factory or fragment.
3. **`define`**: Allows replacing global variables with fixed values. This is often used for feature flags or environment-specific variables.
4. **`external`**: Specifies external modules that should not be bundled.
5. **`plugins`**: Specifies custom esbuild plugins to use during the bundling process.
6. **`keepNames`**: Preserves names during minification, useful for debugging.
7. **`charset`**: Specifies the charset to use for output files. Usually 'utf8', but you can specify 'ascii' if needed.

Here's how you could use the `define` option for example:

```js
// vite.config.js
export default {
	optimizeDeps: {
		esbuild: {
			define: {
				'process.env.NODE_ENV': '"production"'
			}
		}
	}
};
```

## Limitations and Caveats

1. **Compatibility**: Since Vite is using esbuild for optimization, the options you pass must be compatible with esbuild's API.
2. **Conflict Resolution**: Be cautious when setting esbuild options as they can potentially conflict with other Vite options or plugins you may be using.
3. **Documentation**: Always consult the [esbuild documentation](https://esbuild.github.io/api/) for the most accurate and detailed information about these options.

Understanding the `esbuild` options within `optimizeDeps` can offer greater flexibility and control over the build and optimization process. This is particularly useful for developers who have specific optimization requirements that are not handled out-of-the-box by Vite.
