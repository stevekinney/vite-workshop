---
title: Environment Variables
---

# Environment Variables

Environment variables in Vite provide a way to inject runtime values into your application, making it possible to customize the behavior of your app depending on the environment it's running in. These variables are often used for storing API keys, environment-specific URLs, feature flags, and other configuration settings.

### Basic Usage

To define environment variables, you can create a `.env` file at the root of your Vite project. The variables in this file can then be accessed in your application code.

```env
# .env file
VITE_API_URL=https://myapi.com
```

In your application, you can access this variable as follows:

```javascript
console.log(import.meta.env.VITE_API_URL); // Outputs: "https://myapi.com"
```

### Prefixing

It's important to note that only variables prefixed with `VITE_` are exposed in the client-side code. This is a security measure to prevent accidental exposure of sensitive server-side variables.

### Multiple Environment Files

Vite supports multiple `.env` files for different modes:

- `.env` : Default.
- `.env.local` : Local overrides for the default environment.
- `.env.[mode]` : For a specific mode (e.g., `.env.production` for production mode).
- `.env.[mode].local` : Local overrides for a specific mode.

Files are loaded in that order, and variables from later files will overwrite variables declared in earlier files.

### Accessing Environment Variables in `vite.config.js`

In the `vite.config.js` file, you can also access the environment variables via the `process.env` object, but you don't need the `VITE_` prefix there.

```javascript
// vite.config.js
export default {
	plugins: [
		myPlugin({
			apiKey: process.env.VITE_API_URL
		})
	]
};
```

### In Shell Commands

You can also set environment variables directly in your package.json scripts:

```json
{
	"scripts": {
		"dev": "VITE_API_URL=https://dev.myapi.com vite",
		"build": "VITE_API_URL=https://prod.myapi.com vite build"
	}
}
```

### Type Declarations

Since environment variables are strings, you may want to declare their types if you're using TypeScript. Create a `env.d.ts` file for type declarations:

```typescript
interface ImportMetaEnv {
	VITE_API_URL: string;
	// define other variables here
}
```

### Cautions

1. **Security**: Remember that all client-accessible environment variables will be exposed in the browser, so don't store sensitive information there.
2. **Server-side Variables**: Server-side environment variables are accessible in the `vite.config.js` but should not be prefixed with `VITE_` if you want to keep them server-side.

Given your interest in technology and teaching, understanding environment variables could add a layer of depth to your curriculum, allowing you to teach students about best practices for configuration management, security considerations, and environment-specific adjustments.

Would you like to know more about any particular aspect of environment variables in Vite?
