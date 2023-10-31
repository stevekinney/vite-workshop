---
title: Typed CSS Modules
---

# Typed CSS Modules

If you're using TypeScript and CSS modules, you may want type support for your CSS classes. You can use a package like `tcm`, `typed-css-modules` or scripts that generate `.d.ts` files for your CSS modules.

Here's how you might use `typed-css-modules`:

```
npm install -D typed-css-modules
```

Generate types:

```
tcm src -w
```

Include this in your `build` script to ensure the CSS types are always up-to-date.

After all these steps, your `package.json` scripts section may look something like:

```json
{
	"scripts": {
		"build": "vite build && tsc --declaration --emitDeclarationOnly --outDir dist/types && tcm src -w"
	}
}
```
