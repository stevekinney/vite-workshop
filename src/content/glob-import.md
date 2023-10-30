---
title: Glob Import
---

# Glob Import

- Support for importing multiple modules via `import.meta.glob`
- Default behavior transforms to dynamic imports
- Example code for basic usage

## Basic Usage

- How to declare a constant for glob imports
- Transformed code by Vite
- Iterating over modules object to access each module

## Lazy Loading and Chunks

- Default lazy-loaded via dynamic imports
- Split into separate chunks during build process

## Eager Importing

- Usage of `{ eager: true }` as the second argument
- Transformed code when using eager loading
- When to use eager importing

## Advanced Features

### Importing as Strings

- Utilizing Import Reflection syntax with `{ as: 'raw', eager: true }`
- Transformed code and its behavior
- Support for `{ as: 'url' }` for loading assets as URLs

### Multiple Patterns

- Accepts an array of globs as the first argument
- Example code for using multiple patterns

### Negative Patterns

- Prefixed with `!` to exclude files
- Transformed code when using negative patterns

## Named Imports

- Using the `import` options to selectively import parts of the modules
- Example code when using named imports
- Tree-shaking support when combined with `eager`

### Custom Queries

- Using `query` option to provide custom queries
- How other plugins can consume these queries

## Caveats and Limitations

- Vite-only feature, not a web or ES standard
- Rules for glob patterns (relative, absolute, or alias paths)
- Reliance on fast-glob for matching
- Restrictions on literals; variables or expressions not allowed

This outline provides a structured overview of the Glob Import feature in Vite, from basic usage to advanced functionalities, as well as its limitations. It should help you gain a deep understanding of how to leverage this feature effectively.
