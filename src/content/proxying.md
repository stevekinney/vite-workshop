---
title: Proxying
---

# Proxying

Proxying in Vite allows you to forward certain HTTP requests to another server, usually for the purpose of avoiding CORS (Cross-Origin Resource Sharing) issues during development or routing API requests through the development server. This is extremely useful when you have a separate backend API and you want to develop both the frontend and backend concurrently.

### Basic Configuration

To set up a proxy, you can modify your `vite.config.js` to include a `proxy` object inside the `server` configuration.

Here's an example:

```jsx
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react-swc';

export default defineConfig({
	plugins: [react()],
	server: {
		proxy: {
			'/todos': {
				target: 'http://localhost:3000',
				changeOrigin: true
			}
		}
	}
});
```

In this configuration, any request that starts with `/api` on your development server will be forwarded to `http://localhost:3001`.

### Advanced Configuration

For more advanced use-cases, you can use an object for detailed configuration:

```jsx
export default {
	server: {
		proxy: {
			'/api': {
				target: 'http://localhost:3001',
				changeOrigin: true,
				rewrite: (path) => path.replace(/^\/api/, '')
			}
		}
	}
};
```

In this configuration:

- `target` specifies the server to which the request should be proxied.
- `changeOrigin` changes the origin of the host header to the target URL.
- `rewrite` allows you to modify the path of the request URL.

### WebSockets

You can also proxy WebSocket requests:

```jsx
export default {
	server: {
		proxy: {
			'/socket': {
				target: 'http://localhost:3001',
				ws: true
			}
		}
	}
};
```

In this example, WebSocket requests to `/socket` will be proxied to `http://localhost:3001`.

### Multiple Proxy Targets

If you have multiple different APIs or services running on different ports, you can set multiple proxy rules:

```jsx
export default {
	server: {
		proxy: {
			'/api': 'http://localhost:3001',
			'/auth': 'http://localhost:3002'
		}
	}
};
```

### Secure Proxying

To handle secure HTTPS proxying, you can include additional options:

```jsx
export default {
	server: {
		proxy: {
			'/api': {
				target: 'https://secure.api.com',
				secure: false
			}
		}
	}
};
```
