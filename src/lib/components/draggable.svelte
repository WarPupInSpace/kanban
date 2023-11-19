<script>
	let dragData = {
		draggedItem: null,
		initialIndex: null
	};

	let items = [
		{ id: 1, text: 'Item 1' },
		{ id: 2, text: 'Item 2' },
		{ id: 3, text: 'Item 3' }
		// Add more items as needed
	];

	const handleDragStart = (event, item, index) => {
		event.dataTransfer.effectAllowed = 'move';
		event.dataTransfer.setData('text/plain', index);
		dragData.draggedItem = item;
		dragData.initialIndex = index;
	};

	const handleDragOver = (event, index) => {
		event.preventDefault();
		const draggedIndex = parseInt(event.dataTransfer.getData('text/plain'));
		if (index !== draggedIndex) {
			// Swap the items in the array
			items[draggedIndex] = items[index];
			items[index] = dragData.draggedItem;

			// Update the UI
			items = [...items];
		}
	};

	const handleDragEnd = () => {
		dragData = { draggedItem: null, initialIndex: null };
	};
</script>

{#each items as item, index (item.id)}
	<div
		draggable="true"
		on:dragstart={(e) => handleDragStart(e, item, index)}
		on:dragover={(e) => handleDragOver(e, index)}
		on:dragend={handleDragEnd}
	>
		{item.text}
	</div>
{/each}

<style>
	main {
		display: flex;
		flex-direction: column;
	}

	div {
		margin: 8px;
		padding: 8px;
		background-color: #eee;
		cursor: grab;
	}
</style>
