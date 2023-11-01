---
title: Creating a Plugin to Render Markdown
---

```js
// vite-plugin-markdown-to-html.js
const fs = require('fs');
const path = require('path');
const marked = require('marked');

module.exports = function MarkdownToHtml() {
	return {
		name: 'markdown-to-html',
		resolveId(source) {
			// Resolve .md file imports
			if (source.endsWith('.md')) {
				return source;
			}
		},
		load(id) {
			// Load .md file content and transform it to HTML
			if (id.endsWith('.md')) {
				const markdownContent = fs.readFileSync(id, 'utf-8');
				const htmlContent = marked(markdownContent);

				// Export the HTML as a JavaScript string
				return `export default ${JSON.stringify(htmlContent)};`;
			}
		},
		transform(code, id) {
			// Add code transformation logic here (if needed)
		}
	};
};
```
