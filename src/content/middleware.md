### Types of Middleware Mode

Vite has two types of middleware modes:

1. **HTML Mode**: Designed for SPA (Single Page Application) where the server needs to fall back to the `index.html` file for routes. This is the default behavior.
2. **Proxy Mode**: Useful when using Vite as a middleware in a larger application, such as an Express app. This mode doesn't handle HTML fallbacks and leaves that to the surrounding server environment.

Here's how to specify the middleware mode in your `vite.config.js`:

```js
// vite.config.js
export default {
	server: {
		middlewareMode: 'html' // or 'proxy'
	}
};
```

### Adding Custom Middleware

You can add your custom middleware via the `configureServer` hook in your `vite.config.js`. The `configureServer` function will be called with a `ViteDevServer` object, and you can use its `app` property, an instance of `koa`, to add middleware.

```js
// vite.config.js
export default {
	server: {
		configureServer(app) {
			app.use(async (ctx, next) => {
				if (ctx.path === '/hello') {
					ctx.body = 'Hello, world!';
				} else {
					await next();
				}
			});
		}
	}
};
```

In the above example, if you navigate to `http://localhost:<PORT>/hello`, you will see "Hello, world!" displayed.

### Combining with Existing Servers

You can also combine Vite with existing backend servers or frameworks like Express:

```js
// server.js
const express = require('express');
const { createServer } = require('vite');

async function start() {
	const vite = await createServer({
		server: { middlewareMode: 'html' }
	});

	const app = express();

	// Use Vite's middleware
	app.use(vite.middlewares);

	// Your custom routes here
	app.get('/api/hello', (req, res) => res.json({ message: 'Hello' }));

	// Start the server
	app.listen(3000, () => {
		console.log('Server running at http://localhost:3000');
	});
}

start();
```

### Debugging Middleware

For debugging, you can run Vite in debug mode to see detailed logs:

```
DEBUG=vite:* vite
```
