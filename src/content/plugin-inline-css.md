---
title: Plugin for Inline CSS
---

# A Plugin for Inlining CSS

```ts
import fs from 'fs';
import path from 'path';

export default {
	plugins: [
		{
			name: 'inline-css',
			apply: 'build',
			transformIndexHtml: {
				enforce: 'post',
				transform(html) {
					const cssFilePath = path.resolve(__dirname, 'dist/assets/index.css');

					const css = fs.readFileSync(cssFilePath, 'utf-8');

					// Inline the CSS into the HTML's head as a style tag
					return html.replace('</head>', `<style>${css}</style>\n</head>`);
				}
			}
		}
	]
};
```

## A Lazier Way That You Shouldn't Do

```html
<script type="module">
	import styles from './src/style.css?inline';

	const styleElement = document.createElement('style');

	styleElement.textContent = styles;

	document.head.appendChild(styleElement);
</script>
```
