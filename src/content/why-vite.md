---
title: Why Vite?
---

# Why Vite?

1. **Problems with Traditional Tools**: Older build tools require bundling, which becomes increasingly inefficient as the scale of a project grows. This leads to slow server start times and updates.
2. **Slow Server Start**: Vite improves development server start time by categorizing modules into "dependencies" and "source code". Dependencies are pre-bundled using esbuild, which is faster than JavaScript-based bundlers, while source code is served over native ESM, optimizing loading times.
3. **Slow Updates**: Vite makes Hot Module Replacement (HMR) faster and more efficient by only invalidating the necessary chain of modules when a file is edited.
4. **Why Bundle for Production**: Despite the advancements, bundling is still necessary for optimal performance in production. Vite offers a pre-configured build command that includes performance optimizations.
5. **Bundler Choice**: Vite uses Rollup for its flexibility, although esbuild offers speed. The possibility of incorporating esbuild in the future isn't ruled out.
6. **Comparison**: Vite distinguishes itself from other tools in various aspects, which can be further explored in the "Comparisons" section.
