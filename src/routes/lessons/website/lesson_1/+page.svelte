<script lang="ts">
	const quizQuestions = [
		{
			question: 'Which part of the document contains the visible content?',
			options: ['<head>', '<body>', '<title>', '<html lang="en">'],
			answer: 1
		},
		{
			question: 'What is the difference between <h1> and <h2>?',
			options: [
				'<h2> is always bold, but <h1> is not',
				'<h1> is the main heading, while <h2> marks a subsection',
				'<h1> is used for paragraphs',
				'There is no difference'
			],
			answer: 1
		},
		{
			question: 'How can you recognize a closing tag?',
			options: [
				'It contains a forward slash',
				'It contains a period',
				'It is written in capital letters',
				'It does not use brackets'
			],
			answer: 0
		},
		{
			question: 'What does <title> control?',
			options: [
				'The largest heading on the page',
				'The browser-tab title',
				'The page background',
				'The first paragraph'
			],
			answer: 1
		},
		{
			question: 'What should you do after changing your HTML?',
			options: [
				'Delete the file',
				'Restart your computer',
				'Save the file and refresh the browser',
				'Create a new folder'
			],
			answer: 2
		}
	];

	const objectives = [
		'Create and open an HTML file',
		'Set up the basic structure of an HTML document',
		'Add headings and paragraphs',
		'Find and correct common HTML errors'
	];

	const projectRequirements = [
		'One <h1> main heading',
		'At least two <h2> section headings',
		'At least four paragraphs',
		'One use of <strong>',
		'One use of <em>',
		'At least one HTML comment',
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
	<title>Lesson 1: Create Your First Webpage</title>
	<meta
		name="description"
		content="Learn how to create your first webpage using HTML headings, paragraphs, emphasis, and comments."
	/>
</svelte:head>

<div class="lesson-page">
	<header class="hero">
		<div class="hero-content">
			<p class="eyebrow">HTML BASICS</p>
			<h1>Lesson 1: Create Your First Webpage</h1>
			<p class="hero-description">
				Create your first webpage and learn how HTML elements organize the content that appears
				on a website.
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
					By the end of this lesson, you will understand the basic structure of an HTML
					document and be able to build a simple page of your own.
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
			<p class="section-label">Step 1</p>
			<h2>Create your project</h2>
			<p>Before coding, you need to create the folder and file for your webpage.</p>

			<ol class="steps">
				<li>
					Create a folder named <code>my-first-website</code>.
				</li>
				<li>
					Inside the folder, create a file named <code>index.html</code>.
				</li>
				<li>
					Make sure the filename ends in <code>.html</code>, not <code>.txt</code>.
				</li>
			</ol>

			<div class="folder-diagram" aria-label="Example project folder structure">
				<div class="folder">📁 my-first-website</div>
				<div class="file">└── 📄 index.html</div>
			</div>
		</section>

		<section class="content-section">
			<p class="section-label">Step 2</p>
			<h2>Run your first webpage</h2>
			<p>
				Copy the following code into your <code>index.html</code> file.
			</p>

			<div class="code-block">
				<div class="code-header">
					<span>index.html</span>
					<span>HTML</span>
				</div>

				<pre><code>{`<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta
        name="viewport"
        content="width=device-width, initial-scale=1.0"
    >
    <title>My First Website</title>
</head>

<body>
    <h1>Hello, world!</h1>
    <p>I just created my first webpage.</p>
</body>
</html>`}</code></pre>
			</div>

			<div class="instruction-card">
				<h3>Open the page</h3>
				<ol>
					<li>Save the file using <kbd>Ctrl</kbd> + <kbd>S</kbd> or <kbd>Command</kbd> + <kbd>S</kbd>.</li>
					<li>Locate <code>index.html</code> on your computer.</li>
					<li>Double-click the file to open it in your browser.</li>
				</ol>
			</div>

			<p>
				Whenever you change your code, save the file, return to the browser, and refresh the
				page to see the update.
			</p>

			<div class="try-it">
				<p class="try-it-title">Try it</p>
				<p>Change the content inside the heading from:</p>

				<pre><code>{`<h1>Hello, world!</h1>`}</code></pre>

				<p>to something personalized:</p>

				<pre><code>{`<h1>Hello, Raina!</h1>`}</code></pre>

				<p>Save the file and refresh the browser. Your new heading should appear.</p>
			</div>
		</section>

		<section class="content-section">
			<p class="section-label">Step 3</p>
			<h2>Understand the document</h2>
			<p>
				Most HTML pages begin with the same basic structure. Each section gives the browser
				information about the page.
			</p>

			<div class="definition-grid">
				<article class="definition-card">
					<code>&lt;!DOCTYPE html&gt;</code>
					<h3>Document type</h3>
					<p>Tells the browser that the file uses modern HTML.</p>
				</article>

				<article class="definition-card">
					<code>&lt;html lang="en"&gt;</code>
					<h3>Page container</h3>
					<p>
						Contains the entire webpage. The <code>lang="en"</code> attribute tells browsers
						and screen readers that the page is written in English.
					</p>
				</article>
			</div>

			<h3 class="subheading">The head section</h3>

			<div class="code-block">
				<div class="code-header">
					<span>HTML head</span>
					<span>HTML</span>
				</div>

				<pre><code>{`<head>
    <meta charset="UTF-8">
    <meta
        name="viewport"
        content="width=device-width, initial-scale=1.0"
    >
    <title>My First Website</title>
</head>`}</code></pre>
			</div>

			<div class="definition-list">
				<div>
					<code>&lt;head&gt;</code>
					<p>Stores information about the page that is not normally displayed as page content.</p>
				</div>

				<div>
					<code>&lt;meta charset="UTF-8"&gt;</code>
					<p>Allows the page to display letters, symbols, and other characters properly.</p>
				</div>

				<div>
					<code>&lt;meta name="viewport"&gt;</code>
					<p>Helps the webpage display properly on phones, tablets, and computers.</p>
				</div>

				<div>
					<code>&lt;title&gt;</code>
					<p>Controls the title displayed in the browser tab.</p>
				</div>
			</div>
		</section>

		<section class="content-section">
			<p class="section-label">Step 4</p>
			<h2>Understand HTML elements</h2>

			<div class="code-block">
				<div class="code-header">
					<span>Page body</span>
					<span>HTML</span>
				</div>

				<pre><code>{`<body>
    <h1>Hello, world!</h1>
    <p>I just created my first webpage.</p>
</body>`}</code></pre>
			</div>

			<p>
				The <code>&lt;body&gt;</code> element contains everything displayed on the webpage.
			</p>

			<div class="element-example">
				<div class="element-part">
					<code>&lt;p&gt;</code>
					<strong>Opening tag</strong>
					<p>Marks where the element begins.</p>
				</div>

				<div class="element-part">
					<code>I just created my first webpage.</code>
					<strong>Content</strong>
					<p>The information displayed to the visitor.</p>
				</div>

				<div class="element-part">
					<code>&lt;/p&gt;</code>
					<strong>Closing tag</strong>
					<p>Marks where the element ends.</p>
				</div>
			</div>

			<p>
				Together, the opening tag, content, and closing tag form an
				<strong>HTML element</strong>. Most closing tags contain a forward slash.
			</p>

			<div class="try-it">
				<p class="try-it-title">Try it</p>
				<p>Add another paragraph inside your <code>&lt;body&gt;</code>:</p>
				<pre><code>{`<p>This is my second paragraph.</p>`}</code></pre>
				<p>Save the file and refresh the browser to see the change.</p>
			</div>
		</section>

		<section class="content-section">
			<p class="section-label">Step 5</p>
			<h2>Add headings</h2>
			<p>HTML provides six heading levels.</p>

			<div class="code-block">
				<div class="code-header">
					<span>Heading levels</span>
					<span>HTML</span>
				</div>

				<pre><code>{`<h1>Heading Level One</h1>
<h2>Heading Level Two</h2>
<h3>Heading Level Three</h3>
<h4>Heading Level Four</h4>
<h5>Heading Level Five</h5>
<h6>Heading Level Six</h6>`}</code></pre>
			</div>

			<div class="note">
				<strong>Remember:</strong>
				<p>
					Use <code>&lt;h1&gt;</code> for the main page heading. Use lower heading levels to
					organize sections and subsections. Do not select a heading level only because you
					prefer its size; you will control appearance with CSS later.
				</p>
			</div>

			<h3 class="subheading">Example: All About Me</h3>

			<div class="code-block">
				<div class="code-header">
					<span>Page content</span>
					<span>HTML</span>
				</div>

				<pre><code>{`<body>
    <h1>All About Me</h1>

    <h2>Introduction</h2>
    <p>My name is Name, and I am learning web design.</p>

    <h2>My Interests</h2>
    <p>I enjoy making websites.</p>

    <h2>Why I Am Learning HTML</h2>
    <p>I want to create websites where I can share my work!</p>
</body>`}</code></pre>
			</div>
		</section>

		<section class="content-section">
			<p class="section-label">Step 6</p>
			<h2>Add emphasis</h2>

			<div class="two-column">
				<article class="mini-card">
					<h3>Important text</h3>
					<p>
						Use <code>&lt;strong&gt;</code> to mark text as important. Browsers normally
						display it in bold.
					</p>
					<pre><code>{`<p>
    My favorite subject is
    <strong>everything</strong>.
</p>`}</code></pre>
				</article>

				<article class="mini-card">
					<h3>Emphasized text</h3>
					<p>
						Use <code>&lt;em&gt;</code> to emphasize part of a sentence. Browsers normally
						display it in italics.
					</p>
					<pre><code>{`<p>
    I am <em>very excited</em>
    to learn web design.
</p>`}</code></pre>
				</article>
			</div>

			<p>
				These elements do more than change appearance. They also describe the meaning of the
				text to browsers and screen readers.
			</p>
		</section>

		<section class="content-section">
			<p class="section-label">Step 7</p>
			<h2>Use comments</h2>
			<p>
				Comments are notes in your code that the browser does not display. They begin with
				<code>&lt;!--</code> and end with <code>--&gt;</code>.
			</p>

			<div class="code-block">
				<div class="code-header">
					<span>HTML comments</span>
					<span>HTML</span>
				</div>

				<pre><code>{`<!-- Main page heading -->
<h1>All About Me</h1>

<h2>Introduction</h2>
<p>My name is Bob, and I am learning web design.</p>`}</code></pre>
			</div>

			<p>
				The comments remain visible in your code but will not appear when you open the page in
				your browser.
			</p>
		</section>

		<section class="content-section project-section">
			<p class="section-label">Final project</p>
			<h2>Build your own “All About Me” page</h2>
			<p>
				Use the starter code below and replace the example information with your own content.
			</p>

			<div class="code-block">
				<div class="code-header">
					<span>Starter code</span>
					<span>HTML</span>
				</div>

				<pre><code>{`<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta
        name="viewport"
        content="width=device-width, initial-scale=1.0"
    >
    <title>My Page</title>
</head>

<body>
    <h1>Hello, world!</h1>
    <p>This is where your website content goes.</p>
</body>
</html>`}</code></pre>
			</div>

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
						class:correct={
							submitted &&
							selectedAnswers[questionIndex] === quizQuestion.answer
						}
						class:incorrect={
							submitted &&
							selectedAnswers[questionIndex] !== quizQuestion.answer
						}
					>
						<legend>
							<span>{questionIndex + 1}</span>
							{quizQuestion.question}
						</legend>

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
					<button
						type="button"
						class="primary-button"
						disabled={!allAnswered}
						on:click={submitQuiz}
					>
						Check answers
					</button>

					<button type="button" class="secondary-button" on:click={resetQuiz}>
						Reset quiz
					</button>
				</div>

				{#if submitted}
					<div class="score-card" aria-live="polite">
						<p>Your score</p>
						<strong>{score} / {quizQuestions.length}</strong>

						{#if score === quizQuestions.length}
							<span>Excellent work! You are ready for the next lesson.</span>
						{:else if score >= 3}
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

	.overview,
	.double-section,
	.two-column,
	.definition-grid {
		display: flex;
		gap: 2%;
	}

	.overview > *,
	.double-section > *,
	.two-column > *,
	.definition-grid > * {
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
	fieldset {
		margin-top: 1rem;
		padding: 1rem;
		border-radius: 18px;
		background-color: #d9dcd6;
	}

	.definition-list > div {
		margin-top: 0.8rem;
		padding: 1rem;
		border-radius: 15px;
		background-color: #d9dcd6;
	}

	.element-example {
		display: flex;
		gap: 1rem;
		margin-top: 1rem;
	}

	.element-part {
		width: 33%;
		padding: 1rem;
		border-radius: 15px;
		background-color: #d9dcd6;
	}

	.answers {
		display: grid;
		gap: 0.6rem;
		margin-top: 1rem;
	}

	.answers label {
		display: flex;
		gap: 0.6rem;
		padding: 0.7rem;
		border-radius: 12px;
		background-color: #eef0ec;
		cursor: pointer;
	}

	.quiz-actions {
		display: flex;
		gap: 0.75rem;
		margin-top: 1rem;
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

	fieldset.correct {
		border: 2px solid #517457;
	}

	fieldset.incorrect {
		border: 2px solid #965b5b;
	}

	.rightbox {
		display: flex;
		width: 100%;
	}

	.switch-tab-demo,
	.open-lesson-demo {
		width: 700px;
		height: auto;
		padding-left: 2rem;
		object-fit: contain;
	}

	.half {
		width: 49%;
		padding-right: 3rem;
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

		.overview,
		.double-section,
		.two-column,
		.definition-grid,
		.element-example {
			display: block;
		}

		.overview > *,
		.double-section > *,
		.two-column > *,
		.definition-grid > *,
		.element-part,
		.half {
			width: 100%;
		}

		.element-part {
			margin-top: 1rem;
		}

		.switch-tab-demo,
		.open-lesson-demo {
			width: 100%;
			padding-left: 0;
		}
	}
</style>