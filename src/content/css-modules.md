---
title: CSS Modules
---

# CSS Modules

Vite offers native support for CSS Modules, which is a way to locally scope CSS class names to avoid global style conflicts.

- When you create a CSS file with the `.module.css` extension, Vite automatically treats it as a CSS Module.
- You can import and use CSS Modules in your JavaScript, and the class names are scoped to the component.

```vue
<template>
	<div :class="$style.myComponent">This is my component</div>
</template>

<script>
import styles from './my-component.module.css';

export default {
	name: 'MyComponent'
};
</script>
```
