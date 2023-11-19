<script>
	import ListItem from "../components/boardListItem.svelte";
    export let clickHandler;
	let inputValue = '';
	let isInEditMode = false;
	let shake = false;
	let pulse = false;

	// handle input change
	function handleInput(event) {
		inputValue = event.target.value;
	}

	// will require renaming
	function handleKey(event) {
		if (event.key === 'Enter') {
			handleSubmit();
		}
	}

	function startShakeAnimation() {
		shake = true;
		setTimeout(() => (shake = false), 500);
	}

	function startPulseAnimation() {
		pulse = true;
		setTimeout(() => (pulse = false), 500);
	}

	function handleSubmit() {
		const isInTodos = todos.includes(inputValue);
		const isInPending = pending.includes(inputValue);
		const isInCompleted = completed.includes(inputValue);
		if (isInTodos || isInPending || isInCompleted || inputValue === '') {
			startPulseAnimation();
		} else {
			todos = [...todos, inputValue];
			inputValue = '';
		}
	}

	function onClickMoveToPedningState(event) {
		const todo = event.target.id;
		pending = [...pending, todo];
		todos = todos.filter((aTodo) => aTodo !== todo);
	}

	function onClickMoveToCompletedState(event) {
		const todo = event.target.id;
		completed = [...completed, todo];
		pending = pending.filter((aTodo) => aTodo !== todo);
	}

	function onClickdDeleteTodo(event) {
		const todo = event.target.id;
		completed = completed.filter((aTodo) => aTodo !== todo);
	}
</script>

<header>
	<h1>Kanban</h1>
</header>

<div class="container">
	<div class="board">
		<div class="board-head">
			<h2>Todo</h2>
			<button
				on:click={() => {
					return (openCreateState = !openCreateState);
				}}>&#43;</button
			>
		</div>
		<hr />
		{#if openCreateState}
			<div class:pulse id="input-area">
				<input
					id="todo-input"
					type="text"
					on:input={handleInput}
					on:keydown={handleKey}
					bind:value={inputValue}
					placeholder="name of todo"
				/>
				<button on:click={handleSubmit}>Add </button>
			</div>
		{/if}
		<div class="list-container">
			<div class="list">
				{#if todos.length > 0}
					{#each todos as todo}
                        <ListItem id={todo} clickHandler={} />
					{/each}
				{/if}
			</div>
		</div>
	</div>

	<div class="board">
		<h2>Doing</h2>
		<hr />
		<div class="list-container">
			<div class="list">
				{#if pending.length > 0}
					{#each pending as todo}
						<div id={todo} class="list-item">
							<p>
								{todo}
							</p>
							<div class="list-button-container">
								<button id={todo} on:click={onClickMoveToCompletedState}>&#10003;</button>
							</div>
						</div>
					{/each}
				{/if}
			</div>
		</div>
	</div>

	<div class="board">
		<h2>Done</h2>
		<hr />
		<div class="list-container">
			<div class="list">
				{#if completed.length > 0}
					{#each completed as todo}
						<div id={todo} class="list-item">
							<p>
								{todo}
							</p>
							<div class="list-button-container">
								<button id={todo} on:click={onClickdDeleteTodo}>&#128465;</button>
							</div>
						</div>
					{/each}
				{/if}
			</div>
		</div>
	</div>
</div>

<style>
	* {
		margin: 0;
		padding: 0;
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

	#todo-input {
		box-sizing: content-box;
		width: 100%;
	}

	header {
		padding: 1rem;
	}

	body {
		margin: 0;
		padding: 0;
	}

	.container {
		display: grid;
		grid-template-columns: 32% 32% 32%;
		grid-gap: 1rem;
		padding: 1rem;
	}

	header {
		background-color: #6bd4a5;
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

	.list-container {
		height: 14rem;
		overflow: hidden;
	}

	.list {
		height: 100%;
		overflow-y: auto;
	}

	.list-item {
		box-sizing: border-box;
		margin-top: 0.2rem;
		padding: 0.5rem;
		border-radius: 5px;
		box-shadow: rgba(0, 0, 0, 0.05) 0px 0px 0px 1px, rgb(209, 213, 219) 0px 0px 0px 1px inset;
	}

	#input-area {
		display: flex;
		margin-top: 0.2rem;
	}

	.pulse {
		animation: pulse 0.5s infinite;
	}

	@keyframes pulse {
		0% {
			box-shadow: rgba(0, 0, 0, 0.16) 0px 3px 6px, rgba(0, 0, 0, 0.23) 0px 3px 6px;
		}
		50% {
			box-shadow: rgba(0, 0, 0, 0.983) 0px 3px 6px, rgba(0, 0, 0, 0.839) 0px 3px 6px;
		}
		100% {
			box-shadow: rgba(0, 0, 0, 0.16) 0px 3px 6px, rgba(0, 0, 0, 0.23) 0px 3px 6px;
		}
	}

	.shake {
		animation: shake 0.82s cubic-bezier(0.36, 0.07, 0.19, 0.97) both;
		transform: translate3d(0, 0, 0);
		backface-visibility: hidden;
		perspective: 1000px;
	}

	@keyframes shake {
		10%,
		90% {
			transform: translate3d(-1px, 0, 0);
		}

		20%,
		80% {
			transform: translate3d(2px, 0, 0);
		}

		30%,
		50%,
		70% {
			transform: translate3d(-4px, 0, 0);
		}

		40%,
		60% {
			transform: translate3d(4px, 0, 0);
		}
	}

	.list-item-title > p {
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
	}

	.list-button-container {
		width: 100%;
		/* would not say best practice */
		text-align: right;
	}

	button {
		height: 2rem;
		padding: 0.5rem;
		border: none;
		border-radius: 0.5rem;
		cursor: pointer;
	}
</style>
