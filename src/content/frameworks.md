---
title: Usage with Frameworks
---

# Usage with Frameworks

Using a framework like React is super simple.

```ts
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';

// https://vitejs.dev/config/
export default defineConfig({
	plugins: [react()]
});
```

- You can see the list of offical plugins [here](https://vitejs.dev/plugins/#official-plugins).
- There are also [a bunch of community plugins](https://github.com/vitejs/awesome-vite#plugins).
