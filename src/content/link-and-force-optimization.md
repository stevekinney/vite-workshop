---
title: Link and Force Optimization
---

# Link and Force Optimization

The concepts of "linking" and "force optimization" primarily come into play in complex project structures like monorepos or projects that use yarn workspaces, lerna, or similar setups. These scenarios can present challenges for dependency optimization, and Vite's `optimizeDeps` settings can help navigate them.

## Linking in Monorepos

In a monorepo, multiple packages live together, often sharing common dependencies. Sometimes you might want to "link" one package to another so that changes in one package are instantly reflected in another without needing a publish-and-install cycle. In a monorepo setup, the packages are usually symlinked, which can sometimes confuse dependency resolution and optimization processes.

## Force Optimization

Force optimization means explicitly telling Vite to include certain packages in its pre-bundling process. This is where the `optimizeDeps.include` configuration option can be beneficial. If a package is being symlinked or locally linked in a monorepo, it might be excluded from optimization. By explicitly adding it to the `include` array, you force Vite to optimize it.

Here's how you can use `include` to force optimization:

```js
// vite.config.js
export default {
	optimizeDeps: {
		include: ['some-linked-package']
	}
};
```

## Common Issues and Solutions

1. **SymLinked Dependencies**: These can cause problems because Vite might not correctly resolve them to their actual location. Manually including them can help.

2. **Peer Dependencies**: In monorepos or workspaces, peer dependencies can sometimes get hoisted to the root `node_modules`, which might cause issues. Specifying these dependencies in `optimizeDeps.include` can often solve the problem.
3. **Version Mismatches**: Monorepos can sometimes have multiple versions of the same package for different sub-projects. Handling this correctly might require manual configuration and possibly the use of package aliasing to ensure that the right versions are being used.
4. **Native Modules**: Some dependencies might rely on native Node.js modules. Vite and esbuild have specific ways of dealing with these that might require tweaking `optimizeDeps`.
