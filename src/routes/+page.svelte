<svelte:head>
	<title>Learn Web Development and Python</title>
	<meta
		name="description"
		content="Begin learning web development and Python through guided lessons and projects."
	/>
</svelte:head>

<div class="home-page">
	<main>
		<section class="hero">
			<p class="eyebrow">WELCOME</p>
			<h1>Learn Web Development and Python</h1>
			<p class="hero-description">
				This project will teach you the foundations of building websites and programming with
				Python through clear, beginner-friendly lessons.
			</p>

			<div class="subject-grid">
				<article>
					<p class="subject-label">WEB DEVELOPMENT</p>
					<h2>Build your first website</h2>
					<p>Learn how to create content with HTML and design webpages with CSS.</p>
					<a href="/lessons/website">View website lessons <span aria-hidden="true">→</span></a>
				</article>

				<article>
					<p class="subject-label">PYTHON</p>
					<h2>Start programming</h2>
					<p>Learn Python fundamentals and practice using code to solve problems.</p>
					<a href="/lessons/python">View Python lessons <span aria-hidden="true">→</span></a>
				</article>
			</div>

			<div class="getting-started">
				<div>
					<h2>Ready to begin?</h2>
					<p>
						Choose a lesson from the sidebar, or read about how the site works before getting
						started.
					</p>
				</div>

				<a class="how-link" href="/how-it-works">How this site works</a>
			</div>
		</section>
	</main>
</div>

<style>
	:global(*) {
		box-sizing: border-box;
	}

	:global(body) {
		margin: 0;
		background-color: #f4f5f2;
		color: #20231f;
		font-family: Arial, Helvetica, sans-serif;
		line-height: 1.6;
	}

	main {
		max-width: 900px;
		margin: 0 auto;
		padding: 4rem 2rem;
	}

	.hero {
		padding: 2.5rem;
		border-radius: 50px;
		background-color: #b8bdb5;
	}

	.eyebrow,
	.subject-label {
		margin: 0 0 0.4rem;
		font-size: 0.8rem;
		font-weight: bold;
		letter-spacing: 0.08rem;
		text-transform: uppercase;
	}

	h1 {
		max-width: 680px;
		margin: 0 0 0.8rem;
		font-size: 2.65rem;
		line-height: 1.15;
	}

	.hero-description {
		max-width: 650px;
		font-size: 1.08rem;
	}

	.subject-grid {
		display: grid;
		grid-template-columns: repeat(2, minmax(0, 1fr));
		gap: 1rem;
		margin-top: 2rem;
	}

	.subject-grid article {
		padding: 1.5rem;
		border-radius: 20px;
		background-color: #d9dcd6;
	}

	h2 {
		margin: 0 0 0.4rem;
		font-size: 1.35rem;
		line-height: 1.3;
	}

	.subject-grid p {
		margin-top: 0;
	}

	.subject-grid a,
	.how-link {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		gap: 0.4rem;
		padding: 0.7rem 1rem;
		border-radius: 15px;
		background-color: #454a43;
		color: white;
		font-weight: bold;
		text-decoration: none;
	}

	.subject-grid a:hover,
	.how-link:hover {
		background-color: #292c28;
	}

	.getting-started {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 2rem;
		margin-top: 1rem;
		padding: 1.5rem;
		border-radius: 20px;
		background-color: #454a43;
		color: white;
	}

	.getting-started p {
		max-width: 520px;
		margin: 0;
	}

	.how-link {
		flex: 0 0 auto;
		background-color: #eef0ec;
		color: #20231f;
	}

	.how-link:hover {
		background-color: white;
	}

	@media (max-width: 700px) {
		main {
			padding: 2rem 1rem;
		}

		.hero {
			padding: 1.5rem;
			border-radius: 30px;
		}

		h1 {
			font-size: 2rem;
		}

		.subject-grid {
			grid-template-columns: 1fr;
		}

		.getting-started {
			align-items: stretch;
			flex-direction: column;
			gap: 1rem;
		}

		.how-link {
			width: 100%;
		}
	}
</style>