<script>
	import Board from '$lib/components/board.svelte';
	import BoardListItem from '$lib/components/boardListItem.svelte';
	import Draggable from '$lib/components/draggable.svelte';

	let createState = false;

	const lists = {
		todo: [],
		doing: [],
		done: []
	};

	const updateHandler = (currentList, item, newItem) => {
		if (lists[currentList].includes(item)) {
			const index = lists[currentList].indexOf(item);
			lists[currentList][index] = newItem;
		}
	};

	const moveHandler = (currentList, nextList, item) => {
		if (lists[currentList].includes(item)) {
			lists[currentList] = lists[currentList].filter((anItem) => anItem !== item);

			lists[nextList] = [...lists[nextList], item];
		}
	};

	const deleteHandler = (currentList, item) => {
		if (lists[currentList].includes(item)) {
			lists[currentList] = lists[currentList].filter((anItem) => anItem !== item);
		}
	};

	const createHandler = () => {
		lists['todo'] = [{ text: 'New Item', state: 'todo' }, ...lists['todo']];
	};

	// list state handler
	// const stateHandler = (state, item) => {
	// 	switch (state) {
	// 		case 'edit':
	// 			// put all items in lock

	// 			break;
	// 		default:
	// 		// neutral state
	// 	}
	// };
</script>

<div class="container">
	<Board boardName="Todo" createItem={true} {createHandler}>
		<div class="list-container">
			<div class="list">
				{#if lists.todo.length > 0}
					{#each lists.todo as item}
						<BoardListItem
							currentList="todo"
							nextList="doing"
							{moveHandler}
							{updateHandler}
							{deleteHandler}
							{item}
						/>
					{/each}
				{/if}
			</div>
		</div>
	</Board>

	<Board boardName="Doing">
		<div class="list-container">
			<div class="list">
				{#if lists.doing.length > 0}
					{#each lists.doing as item}
						<BoardListItem
							{item}
							currentList="doing"
							nextList="done"
							{moveHandler}
							{updateHandler}
							{deleteHandler}
						/>
					{/each}
				{/if}
			</div>
		</div>
	</Board>

	<Board boardName="Done">
		<div class="list-container">
			<div class="list">
				{#if lists.done.length > 0}
					{#each lists.done as item}
						<BoardListItem {item} />
					{/each}
				{/if}
			</div>
		</div>
	</Board>
</div>

<style>
	* {
		margin: 0;
		padding: 0;
	}

	.container {
		display: grid;
		grid-template-columns: 32% 32% 32%;
		grid-gap: 1rem;
		padding: 1rem;
	}

	.list-container {
		height: 100%;
		overflow: hidden;
	}

	.list {
		height: 100%;
		overflow-y: auto;
	}
</style>
