---
title: Dependency Pre-Bundling
---

# Dependency Pre-Bundling

The "Dependency Pre-Bundling" feature in Vite serves a dual purpose:

1. **Compatibility**: Vite operates in a development environment where it serves all code as native ECMAScript Modules (ESM). But not all dependencies in a project are ESM-ready; some could be in CommonJS or UMD formats. To maintain compatibility, Vite converts these dependencies into ESM. This includes smart import analysis to handle dynamic assignments in CommonJS modules. For example, it allows named imports from React’s CommonJS package to work seamlessly in a Vite project.
2. **Performance**: When you use dependencies that have a high number of internal modules (like `lodash-es` with over 600 internal modules), serving each module separately would result in numerous HTTP requests. This can congest the network and slow down page load times. Vite improves this by pre-bundling these dependencies into single ESM modules, thus reducing the number of HTTP requests needed.

## Automatic Dependency Discovery

When Vite is run for the first time, it automatically scans your source code for imports that are expected to be resolved from `node_modules` (known as "bare imports"). It then uses these found imports as entry points for the pre-bundling process. This is done using esbuild, which is known for its speed.

## Handling New Dependencies

If a new dependency import is discovered while the server is running, Vite will automatically re-run the pre-bundling process and reload the page if needed.

## Monorepo and Linked Dependencies

In a monorepo setup, some dependencies might not come from `node_modules` but might be linked packages within the same repository. Vite is smart enough to recognize this and treat the linked dependencies as source code rather than as dependencies that need to be bundled. However, these linked dependencies must be in ESM format.

## Customization

Vite offers options to customize dependency pre-bundling through the `optimizeDeps` configuration. You can explicitly include or exclude certain dependencies from the pre-bundle. This is useful if, for example, an import is created dynamically by a plugin and therefore isn’t discovered during Vite’s initial scan.

## Caching Mechanisms

- **File System Cache**: Vite caches pre-bundled dependencies in the `node_modules/.vite` directory. It checks several factors to determine if re-bundling is necessary, such as changes in your package lock files or in the Vite config file.
- **Browser Cache**: Once a dependency is cached in the browser, it won't hit the dev server again due to strong caching via HTTP headers.
