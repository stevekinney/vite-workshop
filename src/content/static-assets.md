---
title: Static Assets
---

# Static Assets

Static file serving is an essential feature in many web development environments, and Vite is no exception. Serving static files means that the server handles requests for static assets (like images, CSS, and JavaScript files) without any additional processing, and returns them directly to the client.

The thing about static asset optimization is that we know it's something we _should_ do, but we know we don't often do it, because it's often time **harder than it ought to be**.

To no one's surpise, that's not true with Vite. It's easy with Vite.

## Default Behavior

By default, Vite serves static files from the `public` directory in the root of your project. Files in this directory are served as-is at the root level.

For example, if you have an image at `public/my-image.jpg`, it will be available at `http://localhost:3000/my-image.jpg`.

We saw this in the [Basic Setup](./basic-setup.md) section.

## Advantages

1. **Efficient**: Vite caches these files and serves them efficiently, enabling faster load times during development.
2. **No Rebuild**: Unlike files in `src` or other source code directories, changes to files in `public` don't trigger a rebuild.
3. **Absolute Paths**: Files are served at the root level, which means you can reference them using absolute paths.

## Limitations

1. **No Import Support**: Files in the `public` directory cannot be imported in your source code as modules.
2. **No Pre-Processing**: These files are not processed or optimized by Vite or any of its plugins.

You can't add a hash to them to bust the HTTP cache.

## Serving from Source Code

You can also import and serve static files directly from your source code. This allows them to go through the build process, which can include optimizations like minification or file hashing.

For instance, you can import an image in a JavaScript file:

```js
import myImage from 'src/images/my-image.jpg';

// myImage now contains the resolved URL of the image.
```

Vite's development server utilizes the browser's native caching features to cache static assets. This ensures that unchanged files are not reloaded, leading to faster development experiences.

<div class="exercise">

### Exercise: Try It Out

We have this image in `public/images/steve-after-a-workshop.jpg`. You can try loading just using a regular `img` tag, but that's not the point of this exercise.

- Build the application and look where it is and what it's called.
- Move it into the `src` directory and then try to import it.
- Ignore the fact that it's absolutely huge. We'll deal with that later.
- Build the application again. What do you notice?
- Now grab `public/favicon-16x16.png` and do the same thing with that image. What do you notice?

</div>

<details><summary>Give me some code for adding an image to the DOM.</summary>

Okay, here you go.

```js
import image from './steve-after-a-workshop.jpg';

const content = document.querySelector('#content');

export default function loadImage() {
	const imageElement = document.createElement('img');
	imageElement.src = image;
	content.appendChild(imageElement);
}
```

</details>

### What Happens Under the Hood

In development, the asset URL will point to its direct path like `/img.png`. However, during the production build, it changes to a hashed version, say `/assets/img.2d8efhg.png`.

## Asset Inlining

If an asset is smaller than the limit specified in `assetsInlineLimit`, it will be inlined as a base64 data URL, thereby reducing HTTP requests.

## TypeScript Compatibility

For TypeScript users who may face issues with static asset imports, Vite includes client types to fix these problems.

If you don't already have it. You can create a `vite.d.ts` file with a reference to [Vite's client types](https://vitejs.dev/guide/features.html#client-types).

```ts
/// <reference types="vite/client" />
```

## Esoteria

Here are some quick hits that you _probably_ don't need, but I'm including at the bottom here in case I get a question.

### Customizing the Public Directory

Although the default directory for static files is `public`, you can configure this using the `publicDir` option in `vite.config.js`:

```js
export default defineConfig({
	publicDir: 'my-public-folder'
});
```

### Debugging

If you're having issues with static files not showing up, you can run Vite in debug mode to get detailed logs that might help you diagnose the problem.

```
DEBUG=vite:* vite
```
