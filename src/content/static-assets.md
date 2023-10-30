---
title: Static Assets
---

# Static Assets

Static file serving is an essential feature in many web development environments, and Vite is no exception. Serving static files means that the server handles requests for static assets (like images, CSS, and JavaScript files) without any additional processing, and returns them directly to the client. Here's an in-depth look at how static file serving works in Vite.

## Default Behavior

By default, Vite serves static files from the `public` directory in the root of your project. Files in this directory are served as-is at the root level.

For example, if you have an image at `public/my-image.jpg`, it will be available at `http://localhost:3000/my-image.jpg`.

## Advantages

1. **Efficient**: Vite caches these files and serves them efficiently, enabling faster load times during development.
2. **No Rebuild**: Unlike files in `src` or other source code directories, changes to files in `public` don't trigger a rebuild.
3. **Absolute Paths**: Files are served at the root level, which means you can reference them using absolute paths.

## Limitations

1. **No Import Support**: Files in the `public` directory cannot be imported in your source code as modules.
2. **No Pre-processing**: These files are not processed or optimized by Vite or any of its plugins.

## Customizing the Public Directory

Although the default directory for static files is `public`, you can configure this using the `publicDir` option in `vite.config.js`:

```javascript
// vite.config.js
export default {
	publicDir: 'my-public-folder'
};
```

## Serving from Source Code

You can also import and serve static files directly from your source code. This allows them to go through the build process, which can include optimizations like minification or file hashing.

For instance, you can import an image in a JavaScript file:

```javascript
import myImage from 'src/images/my-image.jpg';

// myImage now contains the resolved URL of the image.
```

## Cache Behavior

Vite's development server utilizes the browser's native caching features to cache static assets. This ensures that unchanged files are not reloaded, leading to faster development experiences.

## Environment Variables

Vite allows you to use environment variables, which you can also utilize when dealing with static assets. However, remember that only variables prefixed with `VITE_` are exposed to your Vite application.

## Debugging

If you're having issues with static files not showing up, you can run Vite in debug mode to get detailed logs that might help you diagnose the problem:

```bash
DEBUG=vite:* vite
```

## Other Notes

## Importing Asset as URL

### Basic Usage

In Vite, you can import an asset directly as a URL. This is similar to how Webpack’s `file-loader` functions, except you have the freedom to use either absolute or relative paths for the asset.

```js
import imgUrl from './img.png';
document.getElementById('hero-img').src = imgUrl;
```

### What Happens Under the Hood

In development, the asset URL will point to its direct path like `/img.png`. However, during the production build, it changes to a hashed version, say `/assets/img.2d8efhg.png`.

### CSS and Vue Special Cases

If you're using CSS, `url()` references are handled in the same manner as JavaScript imports. For Vue developers, asset references in Single File Components (SFC) are automatically converted into imports.

### Extendable Asset Types

Vite automatically identifies common image, media, and font filetypes as assets. You can further extend this list using the `assetsInclude` option.

### Asset Inlining

If an asset is smaller than the limit specified in `assetsInlineLimit`, it will be inlined as a base64 data URL, thereby reducing HTTP requests.

### Handling Git LFS Placeholders

Git Large File Storage (LFS) placeholders are automatically excluded from inlining. You must download the actual file content via Git LFS before building for it to be inlined.

### TypeScript Compatibility

For TypeScript users who may face issues with static asset imports, Vite includes client types to fix these problems.

### Explicit URL Imports

If you need to import assets that are not part of Vite’s internal list, you can use the `?url` suffix to explicitly treat them as URLs. This is especially useful for specialized use-cases, like importing Houdini Paint Worklets.

### Importing Asset as String

You can import assets directly as strings by appending a `?raw` suffix. This is often useful for shader files, configuration files, or other textual data that you need as a string inside your JavaScript.

### Importing Script as Web Worker

Vite supports importing scripts as Web Workers through the use of special query suffixes `?worker` and `?sharedworker`. You can also inline workers as base64 strings using the `?worker&inline` option.

### The `public` Directory

#### Characteristics

If an asset doesn't need to go through any build steps and must retain its filename, you can place it in a special `public` directory. These assets are served at the root level during development and are copied as-is during production builds.

#### Limitations

The `public` directory has some limitations. These assets can't be imported in your JavaScript files, and you should always reference them using root absolute paths.

### `new URL(url, import.meta.url)`

This feature leverages native ESM capabilities to obtain a full, resolved URL of a static asset. The code for this works natively in modern browsers and doesn't need any special handling by Vite during development. It's a powerful feature but comes with its own set of limitations, such as not working in a server-side rendering (SSR) context and requiring static URL strings for correct asset resolution during production builds.
