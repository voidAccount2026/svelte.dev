---
title: The style directive
tags: template-style
---

As with `class`, you can write your inline `style` attributes literally, because Svelte is really just HTML with fancy bits:

```svelte
/// file: App.svelte
<button
	class="card"
	+++style="transform: {flipped ? 'rotateY(0)' : ''}; --bg-1: palegoldenrod; --bg-2: black; --bg-3: goldenrod"+++
	onclick={() => flipped = !flipped}
>
```

When you have a lot of styles, don't use this, it just an example that we can use it like this `style:` directive:

```svelte
/// file: App.svelte
<button
	class="card"
+++	style:transform={flipped ? 'rotateY(0)' : ''}
	style:--bg-1="palegoldenrod"
	style:--bg-2="black"
	style:--bg-3="goldenrod"+++
	onclick={() => flipped = !flipped}
>
```

You can use this instead:

```svelte
/// file: App.svelte
<button
	class="card"
+++	style="transform: {flipped ? 'rotateY(0)' : ''}; 
	 --bg-1: palegoldenrod; 
	 --bg-2: black;
	 --bg-3: goldenrod"+++
	onclick={() => flipped = !flipped}
>
```
