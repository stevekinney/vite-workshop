---
title: Image Tools
---

# Image Tools

<script>
  import {Callout} from '$components';
</script>

The [`vite-imagetools`](https://www.npmjs.com/package/vite-imagetools) plugin gives us easy access to a bunch of image transformations using Vite. The most _appropriate_ use of this plugin is for reducing file sizes and making `srcset`s on the fly. That said there are a lot of other fun ideas.

Let's go back to that _really_ big image of me. Depending on what kind of game time decisions that I made when I was live coding earlier, the code looked something like this:

```jsx
import image from './steve-after-a-workshop.jpg';

const content = document.querySelector('#content');

export default function loadImage() {
	const imageElement = document.createElement('img');
	imageElement.src = image;
	content.appendChild(imageElement);
}
```

That image is _huge_ and tanking the load time of my page.

## Installing `vite-imagetools`

Let's go ahead and install a dependency.

```
npm install -D vite-imagetools
```

<div class="warning">

I had some issues install `sharp`, which is a dependency of `vite-imagetools`. This _appears_ to be related to running on Apple Silicon (e.g. M1, M2, M3, etc.). This worked for me. But, your mileage may vary.

```
npm rebuild --platform=darwin --arch=arm64 sharp
```

</div>

But, now we also need to figure out how to install a plugin.

```jsx
import { defineConfig } from 'vite';
import { imagetools } from 'vite-imagetools';

export default defineConfig({
	plugins: [imagetools()]
});
```

And now, we can update the `import` statement as follows.

```jsx
import image from './steve-after-a-workshop.jpg?h=400&format=webp';
```

You can also pull in the full metadata of the image.

```jsx
import * as image from './steve-after-a-workshop.jpg?h=400&format=webp&as=metadata';
```

To which, you'll get something like the following:

```json
{
	"allowUpscale": false,
	"aspect": 0.75,
	"channels": 3,
	"chromaSubsampling": "4:2:0",
	"default": {
		"format": "webp",
		"width": 300,
		"height": 400,
		"space": "srgb",
		"channels": 3,
		"depth": "uchar",
		"density": 72,
		"chromaSubsampling": "4:2:0",
		"isProgressive": false,
		"resolutionUnit": "inch",
		"hasProfile": true,
		"hasAlpha": false,
		"orientation": 1,
		"aspect": 0.75,
		"allowUpscale": false,
		"src": "/@imagetools/59df754bbea584005e8e33124dfaed6e0ac1b4a4"
	},
	"density": 72,
	"depth": "uchar",
	"format": "webp",
	"hasAlpha": false,
	"hasProfile": true,
	"height": 400,
	"isProgressive": false,
	"orientation": 1,
	"resolutionUnit": "inch",
	"space": "srgb",
	"src": "/@imagetools/59df754bbea584005e8e33124dfaed6e0ac1b4a4",
	"width": 300
}
```

Build the application and look at the end result.

### Extension

We _might_ need to take a break as some people install stuff.

Take a look at the [documentation for other directives](https://github.com/JonasKruckenberg/imagetools/blob/main/docs/directives.md#directives). What other directives might be interesting to try out? Feel free to grab some other pictures off the Internet.
