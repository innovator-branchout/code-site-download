<script lang="ts">
	const quizQuestions = [
		{
			question: 'Which HTML element connects a CSS file to an HTML file?',
			options: ['<css>', '<style>', '<link>', '<connect>'],
			answer: 2
		},
		{
			question: 'What are the three main parts of a CSS rule?',
			options: [
				'Selector, property, and value',
				'Element, tag, and attribute',
				'Color, font, and size',
				'Opening tag, content, and closing tag'
			],
			answer: 0
		},
		{
			question: 'What is the difference between color and background-color?',
			options: [
				'color changes text, while background-color changes the background',
				'color changes the background, while background-color changes text',
				'There is no difference',
				'color only works on images'
			],
			answer: 0
		},
		{
			question: 'What does a CSS selector do?',
			options: [
				'It chooses which elements will be styled',
				'It creates a new HTML file',
				'It opens a website',
				'It changes the browser window size'
			],
			answer: 0
		},
		{
			question: 'What is the difference between padding and margin?',
			options: [
				'Padding is outside an element, while margin is inside',
				'Padding is inside an element, while margin is outside',
				'They are exactly the same',
				'Padding only changes text color'
			],
			answer: 1
		},
		{
			question: 'How do you select every <h2> element?',
			options: ['#h2', '.h2', '<h2>', 'h2'],
			answer: 3
		},
		{
			question: 'How do you select an element with class="featured"?',
			options: ['featured', '#featured', '.featured', '<featured>'],
			answer: 2
		},
		{
			question: 'What does border-radius do?',
			options: [
				'Changes the text size',
				'Rounds the corners of an element',
				'Adds space outside an element',
				'Connects two files'
			],
			answer: 1
		},
		{
			question: 'Why is max-width: 100% useful for images?',
			options: [
				'It prevents the image from becoming wider than its container',
				'It makes every image exactly 100 pixels wide',
				'It removes the image border',
				'It opens the image in a new tab'
			],
			answer: 0
		},
		{
			question: 'What should you check if your CSS does not appear?',
			options: [
				'That the file is named style.css, is in the right folder, and is linked correctly',
				'That you delete index.html',
				'That you restart your computer',
				'That every rule uses a different font'
			],
			answer: 0
		}
	];

	const objectives = [
		'Connect a CSS file to an HTML file',
		'Write basic CSS rules',
		'Select HTML elements to style',
		'Change colors, fonts, and text alignment',
		'Add margins, padding, borders, and rounded corners',
		'Create reusable CSS classes'
	];

	const projectRequirements = [
		'A connected style.css file',
		'A background color',
		'A chosen text color and font',
		'A styled <h1>',
		'Styled section cards',
		'Padding and margins',
		'At least one border',
		'At least one use of border-radius',
		'At least one CSS class',
		'A styled link',
		'An image that does not overflow its section'
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
	<title>Lesson 3: Styling with CSS</title>
	<meta
		name="description"
		content="Learn how to connect CSS to HTML and style colors, fonts, spacing, borders, images, links, and reusable classes."
	/>
</svelte:head>

<div class="lesson-page">
	<header class="hero">
		<div class="hero-content">
			<p class="eyebrow">HTML AND CSS BASICS</p>
			<h1>Lesson 3: Styling with CSS</h1>
			<p class="hero-description">
				Use CSS to change your website’s colors, fonts, spacing, borders, and overall appearance.
				You will continue working on the “All About Me” page from Lessons 1 and 2.
			</p>

			<div class="lesson-meta">
				<span>Beginner</span>
				<span>Estimated time: 35–50 minutes</span>
			</div>
		</div>
	</header>

	<main>
		<section class="content-section overview">
			<div>
				<p class="section-label">Lesson overview</p>
				<h2>What you will learn</h2>
				<p>
					In this lesson, you will create a stylesheet and use CSS to style the webpage you built in
					Lessons 1 and 2.
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
			<h2>Create a CSS file</h2>
			<p>
				Open the <code>my-first-website</code> folder from the previous lessons. It currently
				contains <code>index.html</code>. Create a new file named <code>style.css</code>.
			</p>

			<div class="folder-diagram">
				<div>📁 my-first-website</div>
				<div class="file">├── 📄 index.html</div>
				<div class="file">└── 📄 style.css</div>
			</div>

			<p>
				The HTML file contains your content, while the CSS file contains instructions for how that
				content should look.
			</p>
		</section>

		<section class="content-section">
			<p class="section-label">Step 1</p>
			<h2>Connect your CSS file</h2>
			<p>
				Before the browser can use your CSS, connect <code>style.css</code> to
				<code>index.html</code>. Add this line inside the <code>&lt;head&gt;</code>:
			</p>

			<div class="code-block">
				<div class="code-header"><span>index.html</span><span>HTML</span></div>
				<pre><code>{`<link rel="stylesheet" href="style.css">`}</code></pre>
			</div>

			<p>Your complete <code>&lt;head&gt;</code> should look like this:</p>
			<div class="code-block">
				<div class="code-header"><span>HTML head</span><span>HTML</span></div>
				<pre><code>{`<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>All About Me</title>
    <link rel="stylesheet" href="style.css">
</head>`}</code></pre>
			</div>

			<p>The <code>href</code> attribute tells the browser where to find the CSS file. Save <code>index.html</code>.</p>
		</section>

		<section class="content-section">
			<p class="section-label">Step 2</p>
			<h2>Write your first CSS rule</h2>
			<p>Open <code>style.css</code> and add the following rule:</p>

			<div class="code-block">
				<div class="code-header"><span>style.css</span><span>CSS</span></div>
				<pre><code>{`body {
    background-color: lightblue;
}`}</code></pre>
			</div>

			<p>Save the file and refresh your browser. The background should now be light blue.</p>
			<p>A CSS rule has three main parts:</p>

			<div class="definition-list">
				<div><code>Selector</code><p><code>body</code> chooses what will be styled.</p></div>
				<div><code>Property</code><p><code>background-color</code> chooses what feature will change.</p></div>
				<div><code>Value</code><p><code>lightblue</code> chooses how the feature will change.</p></div>
			</div>

			<div class="note">
				<strong>Remember:</strong>
				<p>CSS properties and values are separated by a colon. Each declaration normally ends with a semicolon.</p>
			</div>
		</section>

		<section class="content-section">
			<p class="section-label">Step 3</p>
			<h2>Change page colors and fonts</h2>
			<p>The <code>color</code> property changes text color, while <code>background-color</code> changes the background.</p>

			<div class="code-block">
				<div class="code-header"><span>Colors and fonts</span><span>CSS</span></div>
				<pre><code>{`body {
    background-color: #f3f4f6;
    color: #1f2937;
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.6;
}`}</code></pre>
			</div>

			<p>
				You can use simple color names such as <code>red</code>, <code>blue</code>, or
				<code>purple</code>. Hexadecimal codes such as <code>#1f2937</code> let you choose more
				specific colors.
			</p>
			<p>
				The browser tries each font from left to right. A larger <code>line-height</code> can make
				paragraphs easier to read.
			</p>
		</section>

		<section class="content-section">
			<p class="section-label">Step 4</p>
			<h2>Style headings</h2>
			<p>CSS can select every element of a particular type. Add these rules to <code>style.css</code>:</p>

			<div class="code-block">
				<div class="code-header"><span>Heading styles</span><span>CSS</span></div>
				<pre><code>{`h1 {
    color: white;
    background-color: #263b59;
    text-align: center;
}

h2 {
    color: #263b59;
}`}</code></pre>
			</div>

			<p>
				This selects every <code>&lt;h1&gt;</code> element. The <code>text-align</code> property
				controls whether text is aligned left, centered, or right.
			</p>
		</section>

		<section class="content-section">
			<p class="section-label">Step 5</p>
			<h2>Understand spacing</h2>
			<p>
				CSS provides two important ways to add space around an element. Padding creates space inside
				an element, while margin creates space outside an element.
			</p>

			<div class="code-block">
				<div class="code-header"><span>Padding and margin</span><span>CSS</span></div>
				<pre><code>{`h1 {
    color: white;
    background-color: #263b59;
    text-align: center;
    padding: 30px;
    margin: 0;
}`}</code></pre>
			</div>

			<div class="definition-list">
				<div><code>padding</code><p>Creates space between an element’s content and its border.</p></div>
				<div><code>margin</code><p>Creates space outside an element, separating it from other elements.</p></div>
			</div>

			<div class="try-it">
				<p class="try-it-title">Try it</p>
				<p>Change <code>padding: 30px</code> to <code>padding: 10px</code>, then to <code>padding: 50px</code>. Save and refresh after each change.</p>
			</div>
		</section>

		<section class="content-section">
			<p class="section-label">Step 6</p>
			<h2>Style your sections</h2>
			<p>You can make every <code>&lt;section&gt;</code> look like a separate card:</p>

			<div class="code-block">
				<div class="code-header"><span>Section cards</span><span>CSS</span></div>
				<pre><code>{`section {
    width: 80%;
    max-width: 700px;
    margin: 24px auto;
    padding: 24px;
    background-color: white;
    border: 1px solid #d1d5db;
    border-radius: 10px;
}`}</code></pre>
			</div>

			<div class="definition-list">
				<div><code>background-color</code><p>Changes the section’s background.</p></div>
				<div><code>border</code><p>Draws a line around the section.</p></div>
				<div><code>border-radius</code><p>Rounds the section’s corners.</p></div>
				<div><code>max-width</code><p>Prevents the section from becoming too wide.</p></div>
			</div>

			<p>
				In <code>margin: 24px auto</code>, <code>24px</code> adds space above and below the section,
				while <code>auto</code> centers it horizontally.
			</p>
		</section>

		<section class="content-section">
			<p class="section-label">Step 7</p>
			<h2>Style images and links</h2>

			<h3 class="subheading">Images</h3>
			<div class="code-block">
				<div class="code-header"><span>Image styles</span><span>CSS</span></div>
				<pre><code>{`img {
    max-width: 100%;
    height: auto;
    border: 3px solid #263b59;
    border-radius: 10px;
}`}</code></pre>
			</div>
			<p>
				<code>max-width: 100%</code> prevents the image from becoming wider than its containing
				section. <code>height: auto</code> preserves the image’s proportions.
			</p>

			<h3 class="subheading">Links</h3>
			<div class="code-block">
				<div class="code-header"><span>Link styles</span><span>CSS</span></div>
				<pre><code>{`a {
    color: #176b87;
    font-weight: bold;
}`}</code></pre>
			</div>
			<p>
				You can remove the underline with <code>text-decoration: none</code>, but the underline
				helps visitors recognize that text is clickable.
			</p>
		</section>

		<section class="content-section">
			<p class="section-label">Step 8</p>
			<h2>Create a CSS class</h2>
			<p>
				An element selector such as <code>section</code> styles every element of that type. A class
				lets you style only the elements you choose.
			</p>

			<div class="code-block">
				<div class="code-header"><span>index.html</span><span>HTML</span></div>
				<pre><code>{`<section class="featured">
    <h2>My Hobbies</h2>
    <ul>
        <li>Programming</li>
        <li>Gaming</li>
        <li>Reading</li>
    </ul>
</section>`}</code></pre>
			</div>

			<div class="code-block">
				<div class="code-header"><span>style.css</span><span>CSS</span></div>
				<pre><code>{`.featured {
    border-left: 6px solid #e5a72e;
}`}</code></pre>
			</div>

			<p>
				The period before <code>featured</code> selects a class. Only elements with
				<code>class="featured"</code> receive this style. You can reuse the same class on multiple
				elements.
			</p>
		</section>

		<section class="content-section">
			<p class="section-label">Step 9</p>
			<h2>Make a link look like a button</h2>
			<p>Add a class to one of your links:</p>

			<div class="code-block">
				<div class="code-header"><span>Button-style link</span><span>HTML</span></div>
				<pre><code>{`<a
    class="button"
    href="https://www.wikipedia.org"
    target="_blank"
>
    Visit Wikipedia
</a>`}</code></pre>
			</div>

			<div class="code-block">
				<div class="code-header"><span>Button style</span><span>CSS</span></div>
				<pre><code>{`.button {
    display: inline-block;
    margin: 10px 0;
    padding: 10px 18px;
    background-color: #176b87;
    color: white;
    border-radius: 6px;
    text-decoration: none;
}`}</code></pre>
			</div>

			<p>The link still works as a link, but CSS makes it look like a button.</p>
		</section>

		<section class="content-section">
			<p class="section-label">Step 10</p>
			<h2>Add CSS comments</h2>
			<p>CSS comments are notes that do not change the appearance of the page.</p>

			<div class="code-block">
				<div class="code-header"><span>style.css</span><span>CSS</span></div>
				<pre><code>{`/* Styles for the entire page */
body {
    background-color: #f3f4f6;
}

/* Heading styles */
/* Section styles */
/* Link styles */`}</code></pre>
			</div>

			<p>A CSS comment begins with <code>/*</code> and ends with <code>*/</code>.</p>
		</section>

		<section class="content-section">
			<p class="section-label">Putting it together</p>
			<h2>Build a styled webpage</h2>
			<p>Your <code>index.html</code> might now look like this:</p>

			<div class="code-block">
				<div class="code-header"><span>index.html</span><span>HTML</span></div>
				<pre><code>{`<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Alex's Website</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>All About Alex</h1>

    <section>
        <h2>Introduction</h2>
        <p>Hello! My name is Alex, and I am learning how to build and style websites.</p>
    </section>

    <section class="featured">
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
            <li>Practice HTML and CSS</li>
        </ol>
    </section>

    <section>
        <h2>My Favorite Website</h2>
        <p>Wikipedia helps me begin learning about new subjects.</p>
        <a class="button" href="https://www.wikipedia.org" target="_blank">
            Visit Wikipedia
        </a>
    </section>

    <section>
        <h2>My Favorite Image</h2>
        <img src="https://picsum.photos/600/350" alt="A randomly selected landscape or object">
    </section>
</body>
</html>`}</code></pre>
			</div>

			<p>Copy the HTML example into <code>index.html</code> and the CSS rules into <code>style.css</code>. Save both files and refresh your browser.</p>
		</section>

		<section class="content-section">
			<p class="section-label">Troubleshooting</p>
			<h2>If the CSS does not appear</h2>
			<div class="instruction-card">
				<ol>
					<li>Make sure the file is named exactly <code>style.css</code>.</li>
					<li>Make sure <code>style.css</code> and <code>index.html</code> are in the same folder.</li>
					<li>Make sure <code>&lt;link rel="stylesheet" href="style.css"&gt;</code> is inside <code>&lt;head&gt;</code>.</li>
					<li>Save both files and refresh the browser.</li>
					<li>Check that every CSS rule has opening and closing braces.</li>
				</ol>
			</div>

			<div class="code-block">
				<div class="code-header"><span>Valid CSS rule</span><span>CSS</span></div>
				<pre><code>{`p {
    color: blue;
}`}</code></pre>
			</div>
		</section>

		<section class="content-section project-section">
			<p class="section-label">Final project</p>
			<h2>Build your own design</h2>
			<p>
				Continue styling your “All About Me” website. Choose your own colors and spacing rather than
				copying every value from the examples.
			</p>

			<div class="requirements">
				<h3>Your finished project should contain:</h3>
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
					<button type="button" class="primary-button" disabled={!allAnswered} on:click={submitQuiz}>Check answers</button>
					<button type="button" class="secondary-button" on:click={resetQuiz}>Reset quiz</button>
				</div>

				{#if submitted}
					<div class="score-card" aria-live="polite">
						<p>Your score</p>
						<strong>{score} / {quizQuestions.length}</strong>
						{#if score === quizQuestions.length}
							<span>Excellent work! You are ready for the next lesson.</span>
						{:else if score >= 6}
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
	.requirements {
		margin-top: 1rem;
		padding: 1rem;
		border-radius: 18px;
		background-color: #d9dcd6;
	}

	.folder-diagram .file {
		padding-left: 1rem;
	}

	.try-it-title {
		margin-top: 0;
		font-weight: bold;
	}

	.definition-list > div {
		display: grid;
		grid-template-columns: minmax(130px, 0.35fr) 1fr;
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