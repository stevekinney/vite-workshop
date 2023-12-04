---
title: A Potential Solution for Glob Import Exercise
---

Here is one potential solution for the exercise found [here](./glob-import.md).

```jsx
import { test, expect } from 'vitest';

import renderCharacter from './render-character';

const characters = import.meta.glob('./*.json', { eager: true });

for (const [path, character] of Object.entries(characters)) {
	const name = path.slice(2, -5);

	test(`renders ${name}`, () => {
		const result = renderCharacter(character);
		expect(result).toMatchSnapshot();
	});
}
```
