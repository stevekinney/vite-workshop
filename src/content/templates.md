---
title: Using Templates
---

<script lang="ts">
  import { Callout } from '$components';
</script>

# Using Templates

You can quickly scaffold out a new Vite project using `npm create`.

```
npm create vite@latest
```

Alternatively, if you prefer `pnpm` or `yarn`, that's easy too.

```
yarn create vite
```

```
pnpm create vite
```

You will be taken through a bunch of steps. Follow the prompts.

```
✔ Select a framework: › React
✔ Select a variant: › TypeScript + SWC
```

<Callout title="A Guided Tour">
I'm going to generate a template and take you on a quick your. You're welcome to follow along with me or pick a totally different framework if there is something that you're more interested in.
</Callout>

## Community Templates

I made two templates that I use all the time.

- [template-typescript](https://github.com/stevekinney/template-typescript)
- [template-react](https://github.com/stevekinney/template-react)

The easiest way to use either one is to use `degit`.

```
npx degit stevekinney/template-typescript
```

There are also [a bunch of templates made by the community](https://github.com/vitejs/awesome-vite#templates).
