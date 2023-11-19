<header>
	<h1>Kanban</h1>
</header>

<slot />

<footer>
	<p>&copy; 2023 I Have no Company</p>
</footer>

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

	header {
		background-color: #6bd4a5;
		text-align: center;
		padding: 2rem;
	}

	footer {
        margin: 0;
		background-color: #333;
		color: white;
		text-align: center;
		position: fixed;
		bottom: 0;
		width: 100%;
	}
</style>
