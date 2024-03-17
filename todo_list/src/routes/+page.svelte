<script lang="ts">
	import Todolist from '$lib/Todolist.svelte';
	import { v4 as uuid } from 'uuid';

	let todos: { id: string; title: string; completed: boolean }[] = [
		{
			id: uuid(),
			title: 'First Task',
			completed: true
		},
		{
			id: uuid(),
			title: 'Second Task',
			completed: true
		},
		{
			id: uuid(),
			title: 'Third Task',
			completed: false
		}
	];
	function handleAddTodo(event) {
		todos = [...todos, { id: uuid(), title: event.detail.title, completed: false }];
		console.log(event.detail.title);
	}

	function handleToggleTodo(event) {
		todos = todos.map((todo) => {
			if (todo.id === event.detail.id) {
				return { ...todo, completed: !todo.completed };
			}
			return { ...todo };
		});

		console.log(todos);
	}

	function handleRemoveTodo(event) {
		todos = todos.filter((todo) => todo.id != event.detail.id);
	}
</script>

<Todolist
	bind:todos
	on:addtodo={handleAddTodo}
	on:toggletodo={handleToggleTodo}
	on:removetodo={handleRemoveTodo}
/>

<style>
	:root {
		--buttonBgColor: #ff3e00;
		--buttonTextColor: #fff;
		background-color: #1d1d1d;
		color: #fff;
	}
</style>
