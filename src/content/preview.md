---
title: Preview Server
---

# The Preview Server

**The Short Version**: You can preview your compiled assets using `vite preview`. This will spin up a server that looks suspiciously like development—except you'll be looking at the built-for-production version of your application as opposed to the development server. This can be super useful if you're tweaking your build process.

## The Longer Version

The preview server in Vite serves as a means to preview the production build of your application. It's basically a local server environment that _mimics_ the behavior of an actual production server, so you can test your application as it would run in The Real World™ setting.

This is super important for debugging issues that only appear in production due to differences like minification, tree-shaking, or lazy-loading.

### How to Use the Preview Server

After you've created a production build of your project by running `vite build`, you can start the preview server by running:

```bash
vite preview
```

This command will start a local HTTP server that serves the files in the `dist` directory (or whatever you've configured as the output directory). You can then navigate to the local server URL displayed in your terminal to view your application.

### Configuration

While the preview server aims to mimic a production environment, you can still specify some options to adjust its behavior. These options are typically placed in the `vite.config.js` file under the `server` field but are limited compared to the dev server. For example:

```js
export default {
	server: {
		preview: {
			port: 5000, // specify a port
			strictPort: true // fail if the port is occupied
		}
	}
};
```

### Why You Might Want to Use it

1. **Production Debugging**: It enables you to catch issues that only manifest in a production-like environment but do so locally where you can more easily debug.
2. **Speed**: It's faster to preview changes locally than to deploy your application to a production server continually.
3. **Isolated Testing**: The preview server allows you to test production behavior without deploying, making it easier to test features or fixes in isolation.

### Limitations

- The preview server is not intended to replace a full-featured production server with features like HTTPS, reverse proxying, or load balancing.
- Custom server middleware you may have defined for the development server won't apply to the preview server.
