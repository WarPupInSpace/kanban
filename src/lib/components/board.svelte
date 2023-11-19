<script>
	export let boardName;
	export let createItem;
    export let createHandler;

	let selected = true;
</script>

<div class:selected class="board">
	<div class="board-head">
		<h2>{boardName}</h2>
		{#if createItem}
			<button on:click={createHandler}>&#43;</button>
		{/if}
	</div>
	<hr />
	<slot />
</div>

<style>
	.selected {
	}

	h1,
	h2,
	h3,
	h4,
	h5,
	h6,
	p,
	a {
		font-family: Verdana, Geneva, Tahoma, sans-serif;
	}

	* {
		margin: 0;
		padding: 0;
	}

	.board {
		padding: 0.5rem;
		height: 20rem;
		box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px, rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
	}

	.board-head {
		display: flex;
		justify-content: space-between;
	}

	button {
		height: 2rem;
		padding: 0.5rem;
		border: none;
		border-radius: 0.5rem;
		cursor: pointer;
	}
</style>
