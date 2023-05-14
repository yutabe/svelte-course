<script>
	import TodoList from './lib/TodoList.svelte';
	import { v4 as uuid } from 'uuid';

	let todoList;

	let todos = [
		{
			id: uuid(),
			title: 'Todo1',
			completed: true
		},
		{
			id: uuid(),
			title: 'Todo2',
			completed: false
		},
		{
			id: uuid(),
			title: 'Todo3',
			completed: true
		}
	];

	$: console.log(todos);

	function handleAddTodo(event) {
		event.preventDefault();
		setTimeout(() => {
			todos = [
				...todos,
				{
					id: uuid(),
					title: event.detail.title,
					completed: false
				}
			];
			todoList.clearInput();
		}, 500);
	}

	function handleRemoveTodo(event) {
		todos = todos.filter((t) => t.id !== event.detail.id);
	}

	function handleToggleTodo(event) {
		todos = todos.map((todo) => {
			if (todo.id === event.detail.id) {
				return { ...todo, completed: event.detail.value };
			}
			return { ...todo };
		});
	}
</script>

<TodoList
	{todos}
	bind:this={todoList}
	on:addtodo={handleAddTodo}
	on:removetodo={handleRemoveTodo}
	on:toggletodo={handleToggleTodo}
/>

<button on:click={() => todoList.focusInput()}>Focus input</button>

<style>
</style>
