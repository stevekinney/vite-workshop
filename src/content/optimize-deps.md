---
title: Optimizing Dependencies
---

# Optimizing Dependencies

The `optimizeDeps` configuration option in Vite controls the optimization behavior of dependencies (i.e., modules installed from `node_modules`). This is particularly important for improving the development server startup time and ensuring compatibility with various npm packages.

When you run Vite for the first time or when you install new dependencies, Vite pre-bundles these dependencies using esbuild by default (or Rollup if you specify it). Pre-bundling is the process of converting the dependencies into ESM (ECMAScript Modules) format and bundling them together into smaller chunks. This is done to improve both the startup time of the development server and the performance of handling these dependencies during development and production builds.

### Configuration Options

You can specify options under `optimizeDeps` in your `vite.config.js` file. Some common properties include:

- `include`: An array of package names or globs to forcibly include in the optimization step, even if they are not imported in your code.

  ```javascript
  optimizeDeps: {
  	include: ['lodash'];
  }
  ```

- `exclude`: An array of package names to exclude from the optimization process.

  ```javascript
  optimizeDeps: {
  	exclude: ['optional-package'];
  }
  ```

- `esbuild`: Allows you to pass options directly to esbuild for dependency optimization.

  ```javascript
  optimizeDeps: {
  	esbuild: {
  		// esbuild options
  	}
  }
  ```

### Why is `optimizeDeps` Needed?

Some packages that are not written as native ESM modules might include dynamic imports, global variables, or other features that are difficult to optimize out-of-the-box. The `optimizeDeps` option gives you more control over the optimization process so you can fine-tune it according to your needs.

### How it Relates to Development and Production

- **Development:** Pre-bundling is primarily a development optimization. It significantly speeds up the dev server's module resolution time by reducing the number of separate files it has to fetch.
- **Production:** In production, the normal bundling step, which also uses Rollup under the hood, will include all imported modules regardless of the `optimizeDeps` setting. Therefore, it is mainly a dev-time optimization, although it can affect production if dependencies are not correctly pre-bundled.

## Tasting Notes

The `optimizeDeps` feature in Vite is important for dependency management, but its configuration is usually straightforward with just the `include` and `exclude` options. However, there are some nuanced aspects that might be worth exploring:

1. **[Link and Force Optimization](./link-and-force-optimization)**: Understanding how to link dependencies in a monorepo or in a workspace setup could be important.
2. **[Esbuild Options](./esbuild-options)**: The `esbuild` option allows you to fine-tune the behavior of the dependency optimizer itself, but it's advanced and often not needed for standard use-cases.
3. **Debugging**: Learning how to debug issues with dependency optimization can be crucial. Vite will throw errors if it encounters packages that it can't pre-optimize, so knowing how to troubleshoot these issues can save a lot of time.
4. **Implications on Caching**: How does `optimizeDeps` affect the caching strategy? Can you invalidate the cache manually?
5. **Optimizing CSS and Other Assets**: Even though `optimizeDeps` primarily targets JavaScript dependencies, it might be worthwhile to understand how it interacts (or doesn't interact) with CSS imports and other assets.
6. **Compatibility with Various Frameworks**: Some frameworks and libraries may have specific needs or incompatibilities that require special configuration in `optimizeDeps`.
7. **Custom Plugins and `optimizeDeps`**: If you are using or writing custom Vite plugins, understanding how they can interact with dependency optimization could be beneficial.
8. **Server vs Client Optimization**: In an SSR context, are there cases where `optimizeDeps` needs to be configured differently for client-side and server-side code?
