---
title: Sass
---

# Using SCSS or Sass

Using SCSS (or Sass) is relatively straight-forward. Consider this change to our CSS.

```scss
.button {
	padding: 0.5rem 1rem;
	background-color: transparent;
	border: none;
	font-size: 20px;
	cursor: pointer;
	&:hover {
		background-color: rgba(255, 255, 255, 0.5);
	}
}
```

We _could_ change the import to `./banner.module.scss`, but you'll see we get a _very_ easy to resolve error.

> Preprocessor dependency "sass" not found. Did you install it? Try `npm install -D sass`.

Well, I guess we can handle this. That's it. Everything works as expected.

## Aliases and URL Rebasing in Pre-processors

- Also available for Sass and Less
- Not supported for Stylus due to API constraints
