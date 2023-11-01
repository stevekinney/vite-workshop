---
title: preserveModules
---

# `preserveModules`

The `preserveModules` option in Rollup is used to preserve the individual modules in the output, keeping the original file and folder structure of the input modules. When you set `preserveModules: true`, Rollup doesn't bundle all the modules into a single file but instead emits each module as a separate file in the output directory.

Here are some important points to note:

### Directory Structure

The option keeps the relative directory structure of the input files. So if you have an `src/input.js` and `src/utils/helper.js`, you might end up with `dist/input.js` and `dist/utils/helper.js`.

### Code Splitting

This option is particularly useful when code-splitting because it allows you to maintain each dynamically-imported module as a separate chunk.

### Tree Shaking

Tree shaking still works as expected. Only the used parts of each module will end up in the final output, but they will remain as individual files.

### Side Effects

You don't get the typical bundling benefits like scope hoisting, which can result in smaller output sizes for a typical single-file bundle. Each file will have its own scope as if it were a standalone module.

### Use Case

It's useful for libraries and other projects where maintaining the original file structure is more beneficial than bundling everything into a single file.

### Example Configuration

Here is a simple example of how to use `preserveModules` in a Rollup configuration:

```js
// vite.config.js
export default {
	build: {
		rollupOptions: {
			output: {
				preserveModules: true
			}
		}
	}
};
```
