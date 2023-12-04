---
title: JSON Named Exports
---

# JSON Named Exports

## Default Import

In many bundlers, importing a JSON file generally brings in the whole object. In Vite, this is also true:

```json
{
	"name": "Alice",
	"age": 30
}
```

In `main.js`:

```jsx
import data from './data.json';

console.log(data.name);
```

**Output**: Alice

## Named Exports

Vite also allows named exports directly from JSON files. This feature enables you to import only the fields you need:

```jsx
import { name, age } from './data.json';

console.log(name);
```

**Output**: Alice

This is different from how Node.js or Webpack handle JSON imports, where you typically have to import the whole object and then destructure it.

## Usage with TypeScript

If you're using TypeScript, you might need to declare the JSON module to make TypeScript aware of the named exports:

```ts
declare module '*.json' {
	const value: any;
	export default value;
	export const name: string;
	export const age: number;
}
```

## Caveats and Considerations

1. **Tree Shaking**: Because you can use named exports, tree shaking is more effective as you only import what you actually use.
2. **Type Safety**: Although it's convenient, remember that there's no type safety when importing JSON files. If the JSON file changes, your code might break.
3. **Dynamic Imports**: If you need to import JSON files dynamically, you'll have to use dynamic `import()` syntax, which returns a Promise.

```ts
import('./data.json').then(function ({ name }) {
	console.log(name);
});
```

**Output**: Alice
