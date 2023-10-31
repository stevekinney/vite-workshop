---
title: CSS and TypeScript
---

# Using TypeScript with CSS Modules

With a few minor changes, `add-banner.ts` works as expected. But, TypeScript is annoyed by the CSS module and the fact that it doesn't know it's type.

We're going to solve for this by using a little library called `typed-css-modules`.

```sh
npm install -D typed-css-modules
```

Next, we can run `tcm src` and it will generate a `.d.ts` file for each CSS file.

If you want to keep this running, you can do something like this in your `package.json`.

```json
{
	"scripts": {
		"watch": "vite & tcm --watch src",
		"check:css": "tcm --listDifferent src"
	}
}
```

Or, if you use husky, you can automate this whenever you commit a change to a CSS file. In `.husky/pre-commit`:

```sh
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npm run check:css
```
