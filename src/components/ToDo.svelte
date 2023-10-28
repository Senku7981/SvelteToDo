<script>
	import ToDoControls from './ToDoControls.svelte';
	import ToDoItem from './ToDoItem.svelte';

	let items = [
		{
			id: 1,
			text: 'Купить хлеб',
			status: false
		},
		{
			id: 2,
			text: 'Купить хлеб 2',
			status: true
		},
		{
			id: 3,
			text: 'Купить хлеб 3',
			status: false
		}
	];
	let lastId = 4;
	function onAdd(event) {
		const item = {
			id: lastId++,
			text: event.detail.text,
			status: false
		};
		items.push(item);
		items = items;
	}
</script>

<div class="todo">
	<ToDoControls on:add={onAdd} />
	<div class="todo__list">
		{#each items as item}
			<ToDoItem text={item.text} id={item.id} status={item.status} />
		{/each}
	</div>
</div>

<style>
	.todo {
		background: #e6e6e6;
		padding: 20px;
		height: 80%;
		width: 600px;
		border-radius: 20px;
		display: flex;
		flex-direction: column;
		gap: 20px;
	}
	.todo__list {
		background: white;
		flex-grow: 1;
		border-radius: 10px;
		padding: 20px;
		display: flex;
		flex-direction: column;
		gap: 20px;
		overflow: auto;
	}
</style>
