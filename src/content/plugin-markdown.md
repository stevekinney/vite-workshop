---
title: Creating a Plugin to Render Markdown
---

# Transforming Markdown

Consider this function to render markdown to HTML.

```jsx
import Markdown from 'markdown-it';
import { readFile } from 'fs/promises';

const md = new Markdown();

const renderMarkdown = async (file) => {
	const content = await readFile(file, 'utf-8');
	const rendered = md.render(content);

	return rendered;
};
```

What would it look like to create a plugin that supported Markdown?

```jsx
function markdownToHtml() {
	return {
		name: 'markdown-to-html',
		resolvedId(id) {
			if (id.endsWith('.md')) {
				return id;
			}
		},
		async load(id) {
			if (id.endsWith('.md')) {
				const rendered = await renderMarkdown(id);
				return `export default ${JSON.stringify(rendered)}`;
			}
		}
	};
}
```
