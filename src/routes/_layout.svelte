<style>
	main {
		position: relative;

		background-color: white;
		padding: 2em;
		margin: 0 auto;
		box-sizing: border-box;
		display: flex;
		justify-content: center;
		overflow-x: hidden;
	}

	.wrapper {
		display: flex;
		flex-direction: column;
		width: 100%;
		max-width: 56em;
	}
</style>

<main>
	<div class="wrapper">
	<slot></slot>
	</div>
</main>