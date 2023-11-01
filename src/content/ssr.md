---
title: Server-Side Rendering
---

# Server-Side Rendering

Server-Side Rendering (SSR) does what it says on the tin. It let's us pre-render a client-side application on the server, sending the fully rendered page to the client. This can improve initial page load performance and enhance SEO. Vite offers first-class support for server-side rendering, providing a more streamlined development experience.

Vite aims to simplify the SSR setup process. You don't need to maintain separate build configurations for the server and client; Vite handles this automatically.

## Hydration

Vite supports "hydration," which is the process of binding event listeners and executing other client-side logic on the pre-rendered HTML content received from the server.

## Configuring SSR in Vite

In Vite, you can specify separate entry points for the server and client using the `vite.config.js` file:

```js
// vite.config.js
export default {
	build: {
		rollupOptions: {
			input: {
				client: './src/client-entry.js',
				server: './src/server-entry.js'
			}
		}
	}
};
```

Inside these entry points, you can use special SSR flags provided by `import.meta` to conditionally run code:

```js
if (import.meta.env.SSR) {
	// Server-only code
} else {
	// Client-only code
}
```

## Vite SSR Plugins and Frameworks

Vite offers plugins that make it easier to work with SSR in popular frameworks like React and Vue. For instance, `@vitejs/plugin-vue` and `@vitejs/plugin-react` come with SSR capabilities out-of-the-box.

## Loading Data

In an SSR context, you often need to fetch data on the server before rendering the page. Vite doesn't dictate how you should do this, giving you the flexibility to use any data-fetching or state-management library.

## Deployment

Vite's SSR output is not tied to a specific Node.js server framework. You can integrate it into an Express application, a Fastify server, or even deploy it on serverless platforms.

## Advantages of Using Vite for SSR

1. **Fast Development:** Vite's HMR capabilities are available in SSR mode, making for a speedy development experience.
2. **Optimized Builds:** Since Vite uses Rollup for production builds, the output is highly optimized.
3. **Flexible:** You're not locked into a specific framework or server environment.
4. **Plugin Ecosystem:** Easily extendable to support various tools and libraries commonly used in SSR contexts.

Implementing Server-Side Rendering (SSR) with Vite involves a few key steps, from modifying your Vite configuration to adapting your application code for both server-side and client-side execution. Below is a step-by-step guide to help you set up SSR in a Vite project:

## Update Vite Configuration

In your `vite.config.js`, specify SSR-specific configurations:

```js
// vite.config.js
export default {
	ssr: {
		// Your SSR-specific configurations here
	}
};
```

## Create Server Entry Point

Create a `server.js` file (or `server.ts` if you're using TypeScript) where you'll implement the server logic. Here's an example using Express:

```js
const express = require('express');
const { createServer: createViteServer } = require('vite');

async function createServer() {
	const app = express();

	// Create Vite server in middleware mode.
	const vite = await createViteServer({
		server: { middlewareMode: 'ssr' }
	});

	app.use(vite.middlewares);

	app.use('*', async (req, res) => {
		// SSR logic here
	});

	app.listen(3000, () => {
		console.log('Server running at http://localhost:3000');
	});
}

createServer();
```

## Implement SSR Logic

You'll need to render your app on the server and send the HTML to the client. Here's an example using Vue:

```js
// Inside your server.js
app.use('*', async (req, res) => {
	const url = req.originalUrl;

	// Use the `ssrRender` function exported from your Vue app
	const { ssrRender } = require('./dist/server/ssr.js');
	let appHtml = await ssrRender(url);

	const html = `
    <!DOCTYPE html>
    <html lang="en">
    <head>
      <title>SSR with Vite</title>
    </head>
    <body>
      <div id="app">${appHtml}</div>
      <script type="module" src="/src/main.js"></script>
    </body>
    </html>
  `;

	res.status(200).set({ 'Content-Type': 'text/html' }).end(html);
});
```

## Client Hydration

In your client entry (usually `main.js` or `main.ts`), add logic to hydrate the application:

```js
import React from 'react';
import { hydrate } from 'react-dom';
import App from './App';

hydrate(<App />, document.getElementById('app'));
```

## Running the Server

Run the server by executing:

```
node server.js
```

Your application should now be running with SSR on `http://localhost:3000`.
