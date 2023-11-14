<script>
</script>

<div class="board">
	<h2>{title}</h2>
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
