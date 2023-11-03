<script>
	import ToDoControls from './ToDoControls.svelte';
	import ToDoItem from './ToDoItem.svelte';

	let items = []; // Здесь хранятся обекты(задачи) в формате {id: , text:'', status: false/true,}
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
	function onChange(event) {
		const item = items.find((i) => i.id === event.detail.id);
		item.status = !item.status;
		items = items;
	}
	function onRemove(event) {
		const idx = items.findIndex((i) => i.id === event.detail.id);
		items.splice(idx, 1);
		items = items;
	}
</script>

<div class="todo">
	<ToDoControls on:add={onAdd} />
	<div class="todo__list">
		{#each items as item}
			<ToDoItem
				text={item.text}
				id={item.id}
				status={item.status}
				on:change={onChange}
				on:remove={onRemove}
			/>
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
