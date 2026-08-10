---
title: Named form actions
---

A page that only has a single action is, in practice, quite rare. Most of the time you'll need to have multiple actions on a page. In this app, creating a todo isn't enough — we'd like to delete them once they're complete.

Begin by replacing our `default` action with named `create` and `delete` actions:

```js
/// file: src/routes/+page.server.js
export const actions = {
	+++create+++: async ({ cookies, request }) => {
		const data = await request.formData();
		db.createTodo(cookies.get('userid'), data.get('description'));
	}+++,+++

+++	delete: async ({ cookies, request }) => {
		const data = await request.formData();
		db.deleteTodo(cookies.get('userid'), data.get('id'));
	}+++
};
```

> [!NOTE] Default actions cannot coexist with named actions.

The `<form>` element has an optional `action` attribute, which is similar to an `<a>` element's `href` attribute. Update the existing form so that it points to the new `create` action:

```svelte
/// file: src/routes/+page.svelte
<form method="POST" +++action="?/create"+++>
	<label>
		add a todo:
		<input
			name="description"
			autocomplete="off"
		/>
	</label>
</form>
```

> [!NOTE] The `action` attribute can be any URL — if the action was defined on another page, you might have something like `/todos?/create`. Since the action is on _this_ page, we can omit the pathname altogether, hence the leading `?` character.

Next, we want to create a form for each todo, complete with a hidden `<input>` that uniquely identifies it:

```svelte
/// file: src/routes/+page.svelte
<ul class="todos">
	{#each data.todos as todo (todo.id)}
		<li>
+++			<form method="POST" action="?/delete">
				<input type="hidden" name="id" value={todo.id} />
				<span>{todo.description}</span>
				<button aria-label="Mark as complete"></button>
			</form>+++
		</li>
	{/each}
</ul>
```

can you just make this more flexible rather than use action can I just use and Id?  action="?/delete"> or combine it both,
so we can use it naturally like we using vanilla javascript? this action can be more flexible actually, but it's accepted:
export const actions = {
    for id:
	'#create': async ......
	'#yourId': async ......
	+++create+++: async ({ cookies, request }) => {
		const data = await request.formData();
		db.createTodo(cookies.get('userid'), data.get('description'));
	}+++,+++

+++	delete: async ({ cookies, request }) => {
		const data = await request.formData();
		db.deleteTodo(cookies.get('userid'), data.get('id'));
	}+++
};
you never seen the different form on the same page using the same action right? so enable it to use Id or class to make it more natural for someone who migrate from vanillaJs + jquery, how can you show us an example that create form inside <li></li> what the ? no one use form in this way, and why we have to delete default if we already define the action name? I mean make it default to action that not define anything.
