---
title: Globbing Entries in Library Mode
---

```ts
  build: {
    lib: {
      entry: glob.sync(path.resolve(__dirname, 'lib/**/*.ts')),
      name: '',
    },
    rollupOptions: {
      output: {
        preserveModules: true,
      },
    },
  },
```
