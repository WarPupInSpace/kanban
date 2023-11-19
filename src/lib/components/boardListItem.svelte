<script>
	export let item;
	export let moveHandler;
	export let deleteHandler;
	export let updateHandler;
	export let currentList;
	export let nextList;

	// disable list
	// export let disabledListHandler;
	export let toggleDisableList;

	// individual item values
	let itemEditState = false;
	let deleteValidate = false;

	let itemCopy;

	// transfer between lists
	let onClickMove = () => {
		if (!itemEditState) {
			moveHandler(currentList, nextList, item);
		}
	};

	// delete from list
	let onClickDelete = () => {
		itemEditState = !itemEditState;
		deleteValidate = !deleteValidate;
		deleteHandler(currentList, item);
	};

	// update in list keydown
	let onKeyDownUpdate = (event) => {
		if (event.key === 'Enter') {
			const value = event.target.value;
			const trimmedValue = value.trim();
			if (trimmedValue != '') {
				updateHandler(currentList, item, itemCopy);
				itemEditState = !itemEditState;
			}
		}
	};

	// Update in List click
	let onClickUpdate = () => {
		updateHandler(currentList, item, itemCopy);
		itemEditState = !itemEditState;
	};

	// state
	let onClickToggleEditState = () => {
		// set or reset copy
		itemCopy = { ...item };
		// toggle between is in edit state
		itemEditState = !itemEditState;
	};
</script>

<div class="list-item">
	<div class="list-item-title">
		{#if itemEditState}
			<input required bind:value={itemCopy.text} on:keydown={onKeyDownUpdate} />
			<button on:click={onClickUpdate}>Update</button>
		{:else}
			<p>
				{item.text}
			</p>
		{/if}
	</div>
	<div class="list-button-container">
		<div>
			{#if itemEditState}
				{#if !deleteValidate}
					<button on:click={() => (deleteValidate = !deleteValidate)}>Delete</button>
				{/if}
				{#if deleteValidate}
					<button on:click={onClickDelete}>Yes</button>
					<button on:click={() => (deleteValidate = !deleteValidate)}>no</button>
				{/if}
			{/if}
		</div>
		<div>
			<button on:click={onClickToggleEditState}>&#9998;</button>

			<button on:click={() => onClickMove(currentList, nextList, item)}>&#8594;</button>
		</div>
	</div>
</div>

<style>
	.disabled {
		pointer-events: none;
		opacity: 0.5;
	}

	.active {
		border: 0.2px solid violet;
		/* pointer-events: none; */
	}

	h1,
	h2,
	h3,
	h4,
	h5,
	h6,
	p,
	a {
		padding: 0;
		margin: 0;
		font-family: Verdana, Geneva, Tahoma, sans-serif;
	}

	.list-item {
		box-sizing: border-box;
		margin-top: 0.2rem;
		padding: 0.5rem;
		border-radius: 5px;
		box-shadow: rgba(0, 0, 0, 0.05) 0px 0px 0px 1px, rgb(209, 213, 219) 0px 0px 0px 1px inset;
	}

	.list-button-container {
		padding-top: 0.5rem;
		border-top: 1px solid black;
		width: 100%;
		/* would not say best practice */
		display: flex;
		justify-content: space-between;
	}

	.list-item-title {
		height: 2rem;
		padding: 0.5rem 0;
		display: flex;
	}

	.list-item-title > input {
		margin: 0;
		width: 100%;
	}

	button {
		height: 2rem;
		padding: 0.5rem;
		border: none;
		border-radius: 0.5rem;
		cursor: pointer;
	}

	.list-item-title > p {
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
	}
</style>
