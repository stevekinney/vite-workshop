---
title: Plugin for Inline CSS
---

# A Plugin for Inlining CSS

```js
function inlineCSS() {
	return {
		name: 'vite-inline-css',
		apply: 'build',
		enforce: 'post',
		transformIndexHtml(html, context) {
			for (const file in context.bundle) {
				if (file.endsWith('.css')) {
					const { fileName, source } = context.bundle[file];

					html = html.replace(
						`<link rel="stylesheet" href="/${fileName}">`,
						`<style>${source}</style>`
					);
				}
			}

			return html;
		}
	};
}
```

## A Lazier Way That You Shouldn't Do

```
<script type="module">
	import styles from './src/style.css?inline';

	const styleElement = document.createElement('style');

	styleElement.textContent = styles;

	document.head.appendChild(styleElement);
</script>
```
