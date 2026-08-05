<svelte:head>
	<title>Python|CodeSite</title>
</svelte:head>

<main>
    <h1>Python Course Overview</h1>
    <p>Throughout this course, you will learn the essentials of Python. This includes numerous labs, quizzes, and lectures. This overview gives information about the content of each lesson. </p>
    <h3>Lesson 1</h3>
    <ul>
        <li>Introduction to Python.</li>
        <li>Setting up a project</li>
        <li>
            Running your first script
            <ul>
                <li>Variables</li>
                <li>Data types</li>
                <li>Math operations & Arithmetic </li>
            </ul>
        </li>
    </ul>
    <h3>Lesson 2</h3>
    <ul>
        <li>
            Conditionals: if, if-else, and else statements
            <ul>
                <li>Comparers, greater than, less than, and equals</li>
            </ul>
        </li>
        <li>Logical operators: and, or, not</li>
        <li>While-loops</li>
        <li>For-loops</li>
    </ul>
    <h3>Lesson 3</h3>
    <ul>
        <li>Lists</li>
        <li>Tuples</li>
        <li>Dictionaries</li>
        <li>Sets</li>
    </ul>
    <h3>Lesson 4</h3>
    <ul>
        <li>
            Python Functions
            <ul>
                <li>Return values and arguments</li>
            </ul>
        </li>
        <li>Scope</li>
        <li>Packages/Libraries</li>
    </ul>
    <h3>Lesson 5</h3>
    <ul>
        <li>
            Classes
            <ul>
                <li>Why classes</li>
                <li>Constructers</li>
                <li>Methods(class functions)</li>
            </ul>
        </li>
        <li>Inheritance</li>
    </ul>


</main>

<style>
    main {
		max-width: 1000px;
		min-height: calc(100vh - 70px);
		margin: 10 auto;
		padding: 1rem 2rem;
	}
	.controls {
		margin-top: 1rem;
	}
    section {
        margin-top: 1rem;
        padding-top: 1rem;
        padding-left: 2rem;
        padding-bottom: 2rem;
        background-color: #b8bdb5;
        border-radius: 50px;
        padding-right: 7rem;
    }
    p {
        max-width: 750px;
    }
    .code-editor {
        height: 100px;
        border: 1px solid #ccc;
        border-radius: 8px;
        overflow: hidden;
    }
    .big-code-editor {
        height: 300px;
        border: 1px solid #ccc;
        border-radius: 8px;
        overflow: hidden;
    }
    .console {
		margin-top: 1rem;
		margin-bottom: 1rem;
		padding: 1rem;
		background-color: #1e1e1e;
		color: #00ff00;
		border-radius: 6px;
		font-family: monospace;
	}
	button {
        margin-bottom: 1rem;
        background-color: #00c04b
	}
    ul {
        list-style-type: disc;
    }
    .letter-list {
        list-style-type: lower-alpha;
    }
    code {
        font-size:1rem;
    }
    li {
        max-width: 700px;
    }

</style>
