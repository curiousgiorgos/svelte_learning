<svelte:options immutable={true} />

<script lang="ts">
	import Button from '$lib/Button.svelte';
	import { createEventDispatcher, onMount } from 'svelte';

	// prompts exported
	export let todos: { id: string; title: string; completed: boolean }[] = [];

	// variables
	let inputText: string = '';
	const dispatch = createEventDispatcher();

	// functions
	function handleAddTodo() {
		if (!inputText) return;
		dispatch('addtodo', { title: inputText });
		inputText = '';
	}

	function handleToggleTodo(id: string) {
		dispatch('toggletodo', { id });
	}

	function handleRemove(id: String) {
		dispatch('removetodo', { id });
	}
</script>

<div class="todos-list">
	<ul>
		{#each todos as { id, title, completed }, index (id)}
			<li>
				<label>
					<input on:input={(event) => handleToggleTodo(id)} type="checkbox" checked={completed} />
					{title}
				</label>
				<button on:click={(event) => handleRemove(id)}> Remove </button>
			</li>
		{/each}
	</ul>
	<form class="add-todo-form" on:submit|preventDefault={handleAddTodo}>
		<input bind:value={inputText} />
		<Button type="submit" disabled={!inputText}>Add</Button>
	</form>
</div>
