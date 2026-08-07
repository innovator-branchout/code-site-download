<script lang="ts">
	const quizQuestions = [
		{
			question: 'Which HTML element creates a bulleted list?',
			options: ['<ol>', '<ul>', '<li>', '<list>'],
			answer: 1
		},
		{
			question: 'Which HTML element creates a numbered list?',
			options: ['<numbers>', '<ul>', '<ol>', '<li>'],
			answer: 2
		},
		{
			question: 'What does the href attribute do?',
			options: [
				'It changes the image width',
				'It tells the browser where a link should go',
				'It creates a heading',
				'It adds a new paragraph'
			],
			answer: 1
		},
		{
			question: 'Why should every image include an alt attribute?',
			options: [
				'To make the image load faster',
				'To change the image color',
				'To describe the image if it cannot load and for screen readers',
				'To open the image in a new tab'
			],
			answer: 2
		},
		{
			question: 'Which element groups related content together?',
			options: ['<group>', '<section>', '<content>', '<article-group>'],
			answer: 1
		},
		{
			question: 'What is the difference between <br> and <p>?',
			options: [
				'<br> creates a line break, while <p> creates a paragraph',
				'<br> creates a heading, while <p> creates a list',
				'There is no difference',
				'<p> only works inside a link'
			],
			answer: 0
		},
		{
			question: 'Which attribute changes the width of an image?',
			options: ['size', 'length', 'width', 'scale'],
			answer: 2
		},
		{
			question: 'What does target="_blank" do?',
			options: [
				'It opens the link in a new tab',
				'It makes the link bold',
				'It hides the link',
				'It opens the link only on a phone'
			],
			answer: 0
		}
	];

	const objectives = [
		'Create ordered and unordered lists',
		'Add links to other websites',
		'Display images on a webpage',
		'Organize a webpage into sections',
		'Build a webpage using multiple HTML elements'
	];

	const projectRequirements = [
		'One <h1> heading',
		'At least three <section> elements',
		'One unordered list',
		'One ordered list',
		'At least one hyperlink',
		'At least one image with an alt attribute',
		'One horizontal line (<hr>)',
		'One line break (<br>)',
		'A personalized browser-tab title'
	];

	let selectedAnswers: Array<number | null> = Array(quizQuestions.length).fill(null);
	let submitted = false;

	function selectAnswer(questionIndex: number, optionIndex: number) {
		selectedAnswers[questionIndex] = optionIndex;
		selectedAnswers = [...selectedAnswers];
		submitted = false;
	}

	function submitQuiz() {
		submitted = true;
	}

	function resetQuiz() {
		selectedAnswers = Array(quizQuestions.length).fill(null);
		submitted = false;
	}

	$: score = quizQuestions.reduce((total, question, index) => {
		return total + (selectedAnswers[index] === question.answer ? 1 : 0);
	}, 0);

	$: allAnswered = selectedAnswers.every((answer) => answer !== null);
</script>

<svelte:head>
	<title>Lesson 2: Adding and Organizing Content</title>
	<meta
		name="description"
		content="Learn how to organize HTML pages and add lists, links, images, sections, line breaks, and horizontal lines."
	/>
</svelte:head>

<div class="lesson-page">
	<header class="hero">
		<div class="hero-content">
			<p class="eyebrow">HTML BASICS</p>
			<h1>Lesson 2: Adding and Organizing Content</h1>
			<p class="hero-description">
				Learn how to organize information on a webpage and add lists, links, and images. These are
				some of the most common HTML elements used on nearly every website.
			</p>

			<div class="lesson-meta">
				<span>Beginner</span>
				<span>Estimated time: 30–45 minutes</span>
			</div>
		</div>
	</header>

	<main>
		<section class="content-section overview">
			<div>
				<p class="section-label">Lesson overview</p>
				<h2>What you will learn</h2>
				<p>
					In this lesson, you will continue your webpage from Lesson 1 by adding more kinds of
					content and organizing it into clear sections.
				</p>
			</div>

			<ul class="objective-list">
				{#each objectives as objective}
					<li>
						<span class="checkmark" aria-hidden="true">✓</span>
						<span>{objective}</span>
					</li>
				{/each}
			</ul>
		</section>

		<section class="content-section">
			<p class="section-label">Continue your project</p>
			<h2>Open your Lesson 1 webpage</h2>
			<p>
				Open the <code>my-first-website</code> folder you created in Lesson 1. Then open
				<code>index.html</code> in your code editor. You will continue building on the webpage you
				already created.
			</p>

			<div class="instruction-card">
				<h3>Before you begin</h3>
				<ol>
					<li>Open your <code>index.html</code> file.</li>
					<li>Keep your browser open so you can preview each change.</li>
					<li>Save the file and refresh the browser after making changes.</li>
				</ol>
			</div>
		</section>

		<section class="content-section">
			<p class="section-label">Step 1</p>
			<h2>Organize your page into sections</h2>
			<p>
				As webpages become larger, it helps to separate content into logical sections. Replace your
				current <code>body</code> with the following example:
			</p>

			<div class="code-block">
				<div class="code-header"><span>index.html</span><span>HTML</span></div>
				<pre><code>{`<body>
    <h1>All About Me</h1>

    <section>
        <h2>Introduction</h2>
        <p>Hello! My name is Alex, and I am learning HTML.</p>
    </section>

    <section>
        <h2>My Hobbies</h2>
        <p>I enjoy programming, gaming, and reading.</p>
    </section>
</body>`}</code></pre>
			</div>

			<p>
				The <code>&lt;section&gt;</code> element groups related content together. Notice that each
				heading now belongs to its own section. As your websites grow, this makes them much easier to
				organize and understand.
			</p>
			<div class="try-it">
				<p class="try-it-title">Try it</p>
				<p>Create a third section about something that interests you.</p>
				<p>Save your file and refresh your browser to view the changes.</p>
			</div>
		</section>

		<section class="content-section">
			<p class="section-label">Step 2</p>
			<h2>Create lists</h2>
			<p>Lists are useful whenever you want to display several related pieces of information.</p>

			<h3 class="subheading">Unordered lists</h3>
			<p>An unordered list displays bullet points.</p>
			<div class="code-block">
				<div class="code-header"><span>Unordered list</span><span>HTML</span></div>
				<pre><code>{`<ul>
    <li>Gaming</li>
    <li>Drawing</li>
    <li>Programming</li>
</ul>`}</code></pre>
			</div>

			<div class="definition-list">
				<div><code>&lt;ul&gt;</code><p>Starts an unordered list.</p></div>
				<div><code>&lt;li&gt;</code><p>Creates one list item.</p></div>
			</div>

			<div class="example-output">
				<p class="output-label">The browser displays:</p>
				<ul>
					<li>Gaming</li>
					<li>Drawing</li>
					<li>Programming</li>
				</ul>
			</div>

			<p>Try adding an unordered list underneath your hobbies paragraph.</p>

			<h3 class="subheading">Ordered lists</h3>
			<p>Ordered lists automatically number each item.</p>
			<div class="code-block">
				<div class="code-header"><span>Ordered list</span><span>HTML</span></div>
				<pre><code>{`<ol>
    <li>Wake up</li>
    <li>Go to school</li>
    <li>Practice coding</li>
</ol>`}</code></pre>
			</div>

			<div class="example-output">
				<p class="output-label">The browser displays:</p>
				<ol>
					<li>Wake up</li>
					<li>Go to school</li>
					<li>Practice coding</li>
				</ol>
			</div>

			<p>Use ordered lists whenever the order of the items matters.</p>
		</section>

		<section class="content-section">
			<p class="section-label">Step 3</p>
			<h2>Add links</h2>
			<p>
				One of the most important features of the web is the ability to connect pages together using
				hyperlinks. Links are created using the <code>&lt;a&gt;</code> element.
			</p>

			<div class="code-block">
				<div class="code-header"><span>Link to a website</span><span>HTML</span></div>
				<pre><code>{`<a href="https://www.google.com">Visit Google</a>`}</code></pre>
			</div>

			<p>
				The <code>href</code> attribute tells the browser where the link should go. Everything between
				the opening and closing tags becomes clickable.
			</p>

			<div class="try-it">
				<p class="try-it-title">Try it</p>
				<p>Add a link to your favorite website:</p>
				<pre><code>{`<p>
    Visit <a href="https://www.wikipedia.org">Wikipedia</a>
    to learn something new.
</p>`}</code></pre>
				<p>Save your page and click the link in your browser.</p>
			</div>
		</section>

		<section class="content-section">
			<p class="section-label">Step 4</p>
			<h2>Open links in a new tab</h2>
			<p>
				Sometimes you want a link to open without replacing your webpage. You can add the
				<code>target</code> attribute.
			</p>

			<div class="code-block">
				<div class="code-header"><span>New-tab link</span><span>HTML</span></div>
				<pre><code>{`<a
    href="https://www.youtube.com"
    target="_blank"
>
    Visit YouTube
</a>`}</code></pre>
			</div>

			<p>
				The value <code>"_blank"</code> tells the browser to open the website in a new tab. Try
				adding this to one of your own links.
			</p>
		</section>

		<section class="content-section">
			<p class="section-label">Step 5</p>
			<h2>Add images</h2>
			<p>Images make webpages more interesting. The image element looks different from the elements you have used so far.</p>

			<div class="code-block">
				<div class="code-header"><span>Image</span><span>HTML</span></div>
				<pre><code>{`<img
    src="https://picsum.photos/300"
    alt="Random picture"
>`}</code></pre>
			</div>

			<p>
				Unlike headings and paragraphs, <code>&lt;img&gt;</code> does not have a closing tag. Instead,
				it uses attributes.
			</p>

			<div class="definition-list">
				<div><code>src</code><p>Tells the browser where to find the image.</p></div>
				<div><code>alt</code><p>Describes the image for screen readers and if the image cannot load.</p></div>
			</div>

			<div class="image-preview">
				<p class="output-label">Example image:</p>
				<img src="https://picsum.photos/300" alt="A randomly selected example photograph" />
			</div>

			<p>Add an image to your page, save the page, and refresh it.</p>
		</section>

		<section class="content-section">
			<p class="section-label">Step 6</p>
			<h2>Resize an image</h2>
			<p>You can control the size of an image using the <code>width</code> attribute.</p>

			<div class="code-block">
				<div class="code-header"><span>Image width</span><span>HTML</span></div>
				<pre><code>{`<img
    src="https://picsum.photos/300"
    alt="Random picture"
    width="250"
>`}</code></pre>
			</div>

			<p>Try changing the width to different values, such as <code>150</code>, <code>250</code>, or <code>400</code>.</p>
		</section>

		<section class="content-section">
			<p class="section-label">Step 7</p>
			<h2>Add horizontal lines and line breaks</h2>

			<h3 class="subheading">Horizontal lines</h3>
			<p>Horizontal lines help separate different parts of a webpage.</p>
			<div class="code-block">
				<div class="code-header"><span>Horizontal line</span><span>HTML</span></div>
				<pre><code>{`<hr>`}</code></pre>
			</div>
			<p>Try placing one between two sections of your page.</p>

			<h3 class="subheading">Line breaks</h3>
			<p>
				Sometimes you want text to continue on the next line without creating a new paragraph. Use
				the <code>&lt;br&gt;</code> element.
			</p>
			<div class="code-block">
				<div class="code-header"><span>Line breaks</span><span>HTML</span></div>
				<pre><code>{`<p>
    My name is Alex<br>
    I enjoy building websites<br>
    HTML is fun!
</p>`}</code></pre>
			</div>
			<p>Notice that <code>&lt;br&gt;</code> does not have a closing tag.</p>
		</section>

		<section class="content-section">
			<p class="section-label">Putting it together</p>
			<h2>Build a complete webpage</h2>
			<p>Your webpage might now look something like this:</p>

			<div class="code-block">
				<div class="code-header"><span>Complete page body</span><span>HTML</span></div>
				<pre><code>{`<body>
    <h1>All About Me</h1>

    <section>
        <h2>Introduction</h2>
        <p>Hello! My name is Alex and I am learning HTML.</p>
    </section>

    <hr>

    <section>
        <h2>My Hobbies</h2>
        <ul>
            <li>Programming</li>
            <li>Gaming</li>
            <li>Reading</li>
        </ul>
    </section>

    <section>
        <h2>My Daily Routine</h2>
        <ol>
            <li>Wake up</li>
            <li>Go to school</li>
            <li>Practice HTML</li>
        </ol>
    </section>

    <section>
        <h2>Favorite Website</h2>
        <p>
            Visit
            <a href="https://www.wikipedia.org" target="_blank">
                Wikipedia
            </a>
            to learn something new.
        </p>
        <img
            src="https://picsum.photos/300"
            alt="Random picture"
            width="250"
        >
    </section>
</body>`}</code></pre>
			</div>
		</section>

		<section class="content-section project-section">
			<p class="section-label">Final project</p>
			<h2>Build your own page</h2>
			<p>
				Continue improving your “All About Me” website. You can make your page about yourself, your
				favorite sport, your pets, your favorite games, or anything else that interests you.
			</p>

			<div class="requirements">
				<h3>Your finished page should contain:</h3>
				<ul>
					{#each projectRequirements as requirement}
						<li>
							<span class="empty-check" aria-hidden="true"></span>
							<code>{requirement}</code>
						</li>
					{/each}
				</ul>
			</div>
		</section>

		<section class="content-section quiz-section">
			<p class="section-label">Knowledge check</p>
			<h2>Check your understanding</h2>
			<p>Answer each question, then submit your responses to see your score.</p>

			<div class="quiz">
				{#each quizQuestions as quizQuestion, questionIndex}
					<fieldset
						class:correct={submitted && selectedAnswers[questionIndex] === quizQuestion.answer}
						class:incorrect={submitted && selectedAnswers[questionIndex] !== quizQuestion.answer}
					>
						<legend class="visually-hidden">{quizQuestion.question}</legend>

						<div class="question-heading">
							<span class="question-number">{questionIndex + 1}</span>
							<span>{quizQuestion.question}</span>
						</div>

						<div class="answers">
							{#each quizQuestion.options as option, optionIndex}
								<label>
									<input
										type="radio"
										name={`question-${questionIndex}`}
										checked={selectedAnswers[questionIndex] === optionIndex}
										on:change={() => selectAnswer(questionIndex, optionIndex)}
									/>
									<span>{option}</span>
								</label>
							{/each}
						</div>

						{#if submitted}
							<p class="feedback">
								{#if selectedAnswers[questionIndex] === quizQuestion.answer}
									Correct!
								{:else}
									The correct answer is
									<strong>{quizQuestion.options[quizQuestion.answer]}</strong>.
								{/if}
							</p>
						{/if}
					</fieldset>
				{/each}

				<div class="quiz-actions">
					<button type="button" class="primary-button" disabled={!allAnswered} on:click={submitQuiz}>
						Check answers
					</button>
					<button type="button" class="secondary-button" on:click={resetQuiz}>Reset quiz</button>
				</div>

				{#if submitted}
					<div class="score-card" aria-live="polite">
						<p>Your score</p>
						<strong>{score} / {quizQuestions.length}</strong>
						{#if score === quizQuestions.length}
							<span>Excellent work! You are ready for the next lesson.</span>
						{:else if score >= 5}
							<span>Good job! Review the questions you missed and try again.</span>
						{:else}
							<span>Review the lesson and try the quiz again.</span>
						{/if}
					</div>
				{/if}
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
		min-height: calc(100vh - 70px);
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
		margin-bottom: 0.75rem;
		font-size: 2.5rem;
		line-height: 1.15;
	}

	.hero-description {
		max-width: 650px;
		font-size: 1.05rem;
	}

	.eyebrow,
	.section-label {
		margin-bottom: 0.4rem;
		font-size: 0.8rem;
		font-weight: bold;
		letter-spacing: 0.08rem;
		text-transform: uppercase;
	}

	.lesson-meta {
		display: flex;
		flex-wrap: wrap;
		gap: 0.75rem;
		margin-top: 1rem;
	}

	.lesson-meta span {
		padding: 0.35rem 0.7rem;
		border: 1px solid #777d73;
		border-radius: 20px;
	}

	section {
		margin-top: 2rem;
		padding: 2rem;
		padding-right: 5rem;
		background-color: #b8bdb5;
		border-radius: 50px;
	}

	h2 {
		margin-top: 0;
	}

	h3 {
		margin-bottom: 0.5rem;
	}

	.subheading {
		margin-top: 2rem;
	}

	p {
		max-width: 650px;
	}

	code {
		padding: 0.1rem 0.3rem;
		border-radius: 4px;
		background-color: #e7e9e4;
		font-family: monospace;
	}

	pre {
		overflow-x: auto;
		margin: 1rem 0;
		padding: 1rem;
		border-radius: 12px;
		background-color: #292c28;
		color: white;
		line-height: 1.5;
	}

	pre code {
		padding: 0;
		background: none;
		color: inherit;
	}

	.code-header {
		display: flex;
		justify-content: space-between;
		padding: 0.6rem 1rem;
		border-radius: 12px 12px 0 0;
		background-color: #454a43;
		color: white;
		font-size: 0.8rem;
	}

	.code-block pre {
		margin-top: 0;
		border-radius: 0 0 12px 12px;
	}

	.overview {
		display: flex;
		gap: 2%;
	}

	.overview > * {
		width: 49%;
	}

	.objective-list,
	.requirements ul {
		padding-left: 0;
		list-style: none;
	}

	.objective-list li,
	.requirements li {
		display: flex;
		gap: 0.6rem;
		margin-bottom: 0.7rem;
	}

	.checkmark {
		font-weight: bold;
	}

	.folder-diagram,
	.instruction-card,
	.try-it,
	.note,
	.definition-card,
	.mini-card,
	.requirements,
	.example-output,
	.image-preview {
		margin-top: 1rem;
		padding: 1rem;
		border-radius: 18px;
		background-color: #d9dcd6;
	}

	.instruction-card ol {
		margin-bottom: 0;
	}

	.try-it-title,
	.output-label {
		margin-top: 0;
		font-weight: bold;
	}

	.definition-list > div {
		display: grid;
		grid-template-columns: minmax(90px, 0.3fr) 1fr;
		gap: 1rem;
		align-items: start;
		margin-top: 0.8rem;
		padding: 1rem;
		border-radius: 15px;
		background-color: #d9dcd6;
	}

	.definition-list p {
		margin: 0;
	}

	.example-output ul,
	.example-output ol {
		margin-bottom: 0;
	}

	.image-preview img {
		display: block;
		max-width: 100%;
		border-radius: 12px;
	}

	.quiz {
		width: 100%;
	}

	.quiz fieldset {
		min-width: 0;
		width: 100%;
		margin: 1.5rem 0;
		padding: 1.5rem;
		border: 1px solid #8c928a;
		border-radius: 24px;
		background-color: #d9dcd6;
	}

	.question-heading {
		display: flex;
		align-items: flex-start;
		gap: 0.7rem;
		margin: 0 0 1.25rem;
		font-size: 1.25rem;
		font-weight: 500;
		line-height: 1.35;
	}

	.question-number {
		display: inline-flex;
		flex: 0 0 auto;
		align-items: center;
		justify-content: center;
		width: 2rem;
		height: 2rem;
		border-radius: 50%;
		background-color: #454a43;
		color: white;
		font-size: 1rem;
		font-weight: bold;
		line-height: 1;
	}

	.answers {
		display: grid;
		gap: 0.75rem;
		margin: 0;
	}

	.answers label {
		display: flex;
		align-items: center;
		gap: 1rem;
		width: 100%;
		min-height: 4.5rem;
		margin: 0;
		padding: 1rem 1.25rem;
		border-radius: 18px;
		background-color: #eef0ec;
		cursor: pointer;
		font-size: 1.1rem;
		line-height: 1.35;
	}

	.answers label:hover {
		background-color: #e5e8e3;
	}

	.answers input[type='radio'] {
		flex: 0 0 auto;
		width: 1.25rem;
		height: 1.25rem;
		margin: 0;
		accent-color: #454a43;
	}

	.answers label span {
		flex: 1;
	}

	.visually-hidden {
		position: absolute;
		width: 1px;
		height: 1px;
		padding: 0;
		margin: -1px;
		overflow: hidden;
		clip: rect(0, 0, 0, 0);
		white-space: nowrap;
		border: 0;
	}

	.feedback {
		margin: 1rem 0 0;
		padding: 0.75rem 1rem;
		border-radius: 12px;
		background-color: #eef0ec;
	}

	.quiz fieldset.correct {
		border: 2px solid #517457;
	}

	.quiz fieldset.incorrect {
		border: 2px solid #965b5b;
	}

	.quiz-actions {
		display: flex;
		flex-wrap: wrap;
		gap: 0.75rem;
		margin-top: 1.5rem;
	}

	button {
		padding: 0.7rem 1rem;
		border: none;
		border-radius: 15px;
		background-color: #454a43;
		color: white;
		font: inherit;
		cursor: pointer;
	}

	button:disabled {
		opacity: 0.5;
		cursor: not-allowed;
	}

	.secondary-button {
		background-color: #72786f;
	}

	.score-card {
		margin-top: 1rem;
		padding: 1rem;
		border-radius: 18px;
		background-color: #454a43;
		color: white;
	}

	.score-card p {
		margin: 0;
	}

	.score-card strong {
		display: block;
		font-size: 1.8rem;
	}

	.empty-check {
		display: inline-block;
		flex: 0 0 auto;
		width: 1.1rem;
		height: 1.1rem;
		border: 2px solid #72786f;
		border-radius: 4px;
	}

	@media (max-width: 750px) {
		main {
			padding: 1rem;
		}

		.hero {
			padding: 2rem 1rem 0;
		}

		.hero h1 {
			font-size: 2rem;
		}

		section {
			padding: 1.5rem;
			border-radius: 30px;
		}

		.overview {
			display: block;
		}

		.overview > * {
			width: 100%;
		}

		.definition-list > div {
			grid-template-columns: 1fr;
			gap: 0.35rem;
		}

		.quiz fieldset {
			padding: 1rem;
			border-radius: 18px;
		}

		.question-heading {
			font-size: 1.05rem;
		}

		.answers label {
			min-height: 4rem;
			padding: 0.85rem 1rem;
			font-size: 1rem;
		}
	}
</style>