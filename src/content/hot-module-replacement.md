---
title: Hot Module Replacement
---

# Hot Module Replacement

Out of the box, Vite supports hot module replacement. This means that if you edit a file. Only that file will be replaced and the rest of the application will continue remain. This allows Vite to refresh the page quickly and maintain the state between reloads.

Most of the time, when we're using a framework, we don't have to think about it and we'll get this for free. But, if we're doing something that has side effects, we may want to clean up after ourselves.

`initializeCounter()` returns a function that removes its event listeners. In the code below, we're going to:

1. Dynamically load `src/counter.js`
2. Call `initialzeCounter()` and store its `cleanup` function.
3. If the module is replaced using hot module reloading, we'll clean up the event listeners from the old one and then reinitialize the counter.

```js
import('./counter.js').then(({ initializeCounter }) => {
	const cleanup = initializeCounter();

	if (import.meta.hot) {
		import.meta.hot.accept(({ module }) => {
			cleanup();
			cleanup = module.initializeCounter();
		});
	}
});
```

If this code seems like a lot, keep in mind two things:

1. This will be stripped out of the final build.
2. Most frameworks will do this for you under the hood. This might be the most that you ever have to think about it.
