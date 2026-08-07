<script lang="ts">
	type Lesson = {
		number: number;
		title: string;
		description: string;
		topics: string[];
		href: string;
	};

	const lessons: Lesson[] = [
		{
			number: 1,
			title: 'Launch Your First Webpage',
			description:
				'Create an HTML file, learn the basic structure of a webpage, and open your first page in a browser.',
			topics: ['HTML document structure', 'Headings and paragraphs', 'Emphasis and comments'],
			href: '/lessons/website/lesson_1'
		},
		{
			number: 2,
			title: 'Add and Organize Content',
			description:
				'Organize your page into sections and add common content such as lists, links, and images.',
			topics: ['Sections and lists', 'Links and new tabs', 'Images and accessibility'],
			href: '/lessons/website/lesson_2'
		},
		{
			number: 3,
			title: 'Style Your Website with CSS',
			description:
				'Connect a stylesheet and use CSS to control your page’s colors, fonts, spacing, borders, and layout.',
			topics: ['CSS rules and selectors', 'Colors and typography', 'Spacing, borders, and classes'],
			href: '/lessons/website/lesson_3'
		}
	];
</script>

<svelte:head>
	<title>Website Building Lessons</title>
	<meta
		name="description"
		content="Learn the foundations of website building with beginner lessons on HTML, organizing content, and CSS."
	/>
</svelte:head>

<div class="overview-page">
	<header class="hero">
		<div class="hero-content">
			<p class="eyebrow">LEARNING PATH</p>
			<h1>Website Building</h1>
			<p class="hero-description">
				Learn how websites are built by creating your own webpage from the ground up. You will
				start with HTML, add useful content, and then use CSS to design the finished page.
			</p>

			<div class="course-meta">
				<span>Beginner</span>
				<span>3 lessons</span>
				<span>No experience required</span>
			</div>
		</div>
	</header>

	<main>
		<section class="content-section introduction">
			<div>
				<p class="section-label">Introduction</p>
				<h2>What makes a website?</h2>
				<p>
					A website is a collection of files that a browser reads and displays. These files work
					together to determine what appears on the page and how everything looks.
				</p>
				<p>
					Two of the most important languages used to build webpages are
					<strong>HTML</strong> and <strong>CSS</strong>.
				</p>
			</div>

			<div class="language-grid">
				<article class="language-card">
					<div class="language-mark" aria-hidden="true">HTML</div>
					<h3>Content and structure</h3>
					<p>
						HTML identifies and organizes the content on a webpage, including headings,
						paragraphs, lists, links, and images.
					</p>
				</article>

				<article class="language-card">
					<div class="language-mark" aria-hidden="true">CSS</div>
					<h3>Appearance and design</h3>
					<p>
						CSS controls how the content looks, including its colors, fonts, spacing, borders,
						and arrangement.
					</p>
				</article>
			</div>
		</section>

		<section class="content-section analogy-section">
			<p class="section-label">A helpful comparison</p>
			<h2>Think of a webpage as a house</h2>

			<div class="analogy-grid">
				<div class="analogy-card">
					<span class="analogy-number" aria-hidden="true">1</span>
					<div>
						<h3>HTML builds the house</h3>
						<p>
							HTML creates the rooms, doors, and walls. It gives the page its structure and
							determines what content exists.
						</p>
					</div>
				</div>

				<div class="analogy-card">
					<span class="analogy-number" aria-hidden="true">2</span>
					<div>
						<h3>CSS decorates the house</h3>
						<p>
							CSS chooses the colors, decorations, spacing, and arrangement. It changes the
							appearance without replacing the structure.
						</p>
					</div>
				</div>
			</div>
		</section>

		<section class="content-section lessons-section">
			<p class="section-label">Course outline</p>
			<h2>Your website-building path</h2>
			<p class="section-intro">
				Complete the lessons in order. Each lesson continues the same project, so by the end you
				will have built and styled a complete webpage.
			</p>

			<div class="lesson-list">
				{#each lessons as lesson}
					<article class="lesson-card">
						<div class="lesson-number" aria-hidden="true">{lesson.number}</div>

						<div class="lesson-content">
							<p class="lesson-label">Lesson {lesson.number}</p>
							<h3>{lesson.title}</h3>
							<p>{lesson.description}</p>

							<ul>
								{#each lesson.topics as topic}
									<li>
										<span aria-hidden="true">✓</span>
										{topic}
									</li>
								{/each}
							</ul>
						</div>

						<a class="lesson-link" href={lesson.href} aria-label={`Open Lesson ${lesson.number}: ${lesson.title}`}>
							Open lesson <span aria-hidden="true">→</span>
						</a>
					</article>
				{/each}
			</div>
		</section>

		<section class="content-section project-section">
			<div>
				<p class="section-label">Course project</p>
				<h2>Build an “All About Me” webpage</h2>
				<p>
					Throughout these lessons, you will build one webpage about yourself or any subject that
					interests you. Each lesson adds a new layer to the same project.
				</p>
			</div>

			<ol class="project-steps">
				<li><strong>Create</strong><span>Build the page structure with HTML.</span></li>
				<li><strong>Organize</strong><span>Add sections, lists, links, and images.</span></li>
				<li><strong>Design</strong><span>Use CSS to personalize the finished page.</span></li>
			</ol>
		</section>

		<section class="start-section">
			<div>
				<p class="section-label">Ready to begin?</p>
				<h2>Launch your first webpage</h2>
				<p>Start with Lesson 1. You only need a code editor and a web browser.</p>
			</div>

			<a class="primary-button" href="/lessons/website/lesson_1">
				Start Lesson 1 <span aria-hidden="true">→</span>
			</a>
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
		margin: 10px auto;
		padding: 1rem 2rem 4rem;
	}

	.hero {
		max-width: 900px;
		margin: 0 auto;
		padding: 3rem 2rem 1rem;
	}

	.hero-content {
		max-width: 750px;
	}

	.hero h1 {
		margin: 0 0 0.75rem;
		font-size: 2.75rem;
		line-height: 1.15;
	}

	.hero-description {
		max-width: 680px;
		font-size: 1.08rem;
	}

	.eyebrow,
	.section-label,
	.lesson-label {
		margin: 0 0 0.4rem;
		font-size: 0.8rem;
		font-weight: bold;
		letter-spacing: 0.08rem;
		text-transform: uppercase;
	}

	.course-meta {
		display: flex;
		flex-wrap: wrap;
		gap: 0.75rem;
		margin-top: 1rem;
	}

	.course-meta span {
		padding: 0.35rem 0.7rem;
		border: 1px solid #777d73;
		border-radius: 20px;
	}

	.content-section,
	.start-section {
		margin-top: 2rem;
		padding: 2rem;
		background-color: #b8bdb5;
		border-radius: 50px;
	}

	h2 {
		margin-top: 0;
		line-height: 1.25;
	}

	h3 {
		margin: 0 0 0.4rem;
		line-height: 1.3;
	}

	p {
		max-width: 680px;
	}

	.introduction {
		display: grid;
		grid-template-columns: minmax(0, 0.9fr) minmax(0, 1.1fr);
		gap: 2rem;
	}

	.language-grid,
	.analogy-grid {
		display: grid;
		gap: 1rem;
	}

	.language-card,
	.analogy-card,
	.lesson-card,
	.project-steps {
		background-color: #d9dcd6;
		border-radius: 18px;
	}

	.language-card {
		padding: 1.25rem;
	}

	.language-card p,
	.analogy-card p {
		margin-bottom: 0;
	}

	.language-mark {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		min-width: 4rem;
		margin-bottom: 0.8rem;
		padding: 0.3rem 0.65rem;
		border-radius: 20px;
		background-color: #454a43;
		color: white;
		font-family: monospace;
		font-weight: bold;
	}

	.analogy-grid {
		grid-template-columns: repeat(2, minmax(0, 1fr));
	}

	.analogy-card {
		display: flex;
		gap: 1rem;
		padding: 1.25rem;
	}

	.analogy-number,
	.lesson-number {
		display: inline-flex;
		flex: 0 0 auto;
		align-items: center;
		justify-content: center;
		border-radius: 50%;
		background-color: #454a43;
		color: white;
		font-weight: bold;
	}

	.analogy-number {
		width: 2rem;
		height: 2rem;
	}

	.section-intro {
		margin-bottom: 1.5rem;
	}

	.lesson-list {
		display: grid;
		gap: 1rem;
	}

	.lesson-card {
		display: grid;
		grid-template-columns: auto minmax(0, 1fr) auto;
		gap: 1.25rem;
		align-items: start;
		padding: 1.4rem;
	}

	.lesson-number {
		width: 2.75rem;
		height: 2.75rem;
		font-size: 1.15rem;
	}

	.lesson-content p {
		margin: 0.4rem 0 0.8rem;
	}

	.lesson-content ul {
		display: flex;
		flex-wrap: wrap;
		gap: 0.45rem 1rem;
		margin: 0;
		padding: 0;
		list-style: none;
		font-size: 0.9rem;
	}

	.lesson-content li {
		display: flex;
		gap: 0.35rem;
	}

	.lesson-link,
	.primary-button {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		gap: 0.45rem;
		border-radius: 15px;
		background-color: #454a43;
		color: white;
		font-weight: bold;
		text-decoration: none;
	}

	.lesson-link {
		padding: 0.65rem 0.9rem;
		white-space: nowrap;
	}

	.lesson-link:hover,
	.primary-button:hover {
		background-color: #292c28;
	}

	.project-section {
		display: grid;
		grid-template-columns: minmax(0, 1fr) minmax(280px, 0.8fr);
		gap: 2rem;
	}

	.project-steps {
		margin: 0;
		padding: 1.25rem 1.25rem 1.25rem 3rem;
	}

	.project-steps li + li {
		margin-top: 0.8rem;
	}

	.project-steps strong,
	.project-steps span {
		display: block;
	}

	.start-section {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 2rem;
		background-color: #454a43;
		color: white;
	}

	.start-section p {
		margin-bottom: 0;
	}

	.primary-button {
		flex: 0 0 auto;
		padding: 0.85rem 1.2rem;
		background-color: #eef0ec;
		color: #20231f;
	}

	.primary-button:hover {
		background-color: white;
	}

	@media (max-width: 750px) {
		main {
			padding: 1rem;
		}

		.hero {
			padding: 2rem 1rem 0;
		}

		.hero h1 {
			font-size: 2.1rem;
		}

		.content-section,
		.start-section {
			padding: 1.5rem;
			border-radius: 30px;
		}

		.introduction,
		.analogy-grid,
		.project-section {
			grid-template-columns: 1fr;
		}

		.lesson-card {
			grid-template-columns: auto minmax(0, 1fr);
		}

		.lesson-link {
			grid-column: 1 / -1;
			width: 100%;
		}

		.start-section {
			align-items: stretch;
			flex-direction: column;
		}

		.primary-button {
			width: 100%;
		}
	}
</style>