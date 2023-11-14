<script>
	import { onMount } from 'svelte';
	export let state;

	onMount(() => {
		document.addEventListener('click', handleOutsideClick);

		return () => {
			document.removeEventListener('click', handleOutsideClick);
		};
	});

	function handleOutsideClick(event) {
		const container = document.getElementById('your-container-id');

		if (container && !container.contains(event.target)) {
			openCreateState = false;
		}
	}

	function handleKeyPress(event) {}

	function handleSubmit(event) {}
</script>

<div role="button" tabindex="0" id="pop" on:click={handleOutsideClick} on:keydown={handleKeyPress}>
	<div>
		<slot />
	</div>
	<button on:click={() => (state = !state)}>&#10060;</button>
</div>

<style>
	#pop {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
	}
</style>
