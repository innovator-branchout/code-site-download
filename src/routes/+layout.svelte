<script>
	import Sidebar from '$lib/Sidebar.svelte';

	let { children } = $props();
</script>

<div class="site-layout">
	<Sidebar />

	<main>
		{@render children()}
	</main>
</div>

<style>
	:global(*) {
		box-sizing: border-box;
	}

	:global(html) {
		font-family: Inter, Arial, sans-serif;
	}

	:global(body) {
		margin: 0;
		color: #263331;
		background: #e0e2db;
	}

	.site-layout {
		display: grid;
		grid-template-columns: 250px 1fr;
		min-height: 100vh;
	}

	main {
		min-width: 0;
		padding: 3rem 3.5rem;
		background: #e0e2db;
	}

	main :global(h1) {
		margin: 0;
		color: #5f7470;
		font-size: clamp(2rem, 5vw, 3rem);
	}

	@media (max-width: 700px) {
		.site-layout {
			grid-template-columns: 1fr;
		}

		main {
			padding: 2rem 1.5rem;
		}
	}
</style>