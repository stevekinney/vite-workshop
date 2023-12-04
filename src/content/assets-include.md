---
title: assetsInclude
---

# `assetsInclude`

The `assetsInclude` option in Vite's configuration allows you to specify additional file types that should be treated as assets. By default, Vite treats certain types of files like images and fonts as assets, meaning they will be copied as-is into the final build directory without being bundled as JavaScript. However, you may have other custom file types that you want to be treated in the same way. That's where `assetsInclude` comes in handy.

### How to Use

You can use this option to extend the default behavior by specifying a string, a RegExp pattern, or an array of both. Here's how you could use it in your Vite configuration:

```jsx
export default {
	assetsInclude: ['*.pdf', '*.ico']
};
```

In this example, all `.pdf` and `.ico` files imported in your code will be treated as assets, in addition to the default asset types that Vite already handles.

### RegExp Pattern

You can also use RegExp patterns for more complex scenarios:

```jsx
export default {
	assetsInclude: /^\.\/some-special-dir\/.*\.special-extension$/
};
```

### Array of Patterns

An array can be used to include multiple patterns:

```jsx
export default {
	assetsInclude: ['*.pdf', /^\.\/some-special-dir\/.*\.special-extension$/]
};
```

### Handling Custom Asset Types

Once a file type is marked as an asset, you can import it in your JavaScript like you would import, say, an image:

```jsx
import pdfPath from 'src/assets/some-document.pdf';
```

`pdfPath` will contain the resolved URL for the PDF asset.

### Use Cases

The `assetsInclude` option is especially useful in projects that have custom assets that are not covered by Vite's default asset handling. For example:

- Multimedia projects that use custom audio formats.
- Applications that need to serve raw data files.
- PDFs or other document types that should be treated as static assets.
