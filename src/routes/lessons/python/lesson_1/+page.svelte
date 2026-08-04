<svelte:head>
	<title>Lesson 1|CodeSite</title>
</svelte:head>
<script lang="ts">
    import CodeMirror from "svelte-codemirror-editor";
    import { python } from "@codemirror/lang-python";
    import { onMount } from "svelte";

    let code = $state('print("Hello, World!")');
    let output = $state("");
    let isRunning = $state(false);
    let pyodide = $state<any>(null);

    onMount(async () => {
		if (!(window as any).loadPyodide) {
			const script = document.createElement("script");
			script.src = "/pyodide/pyodide.js";
			document.head.appendChild(script);
			await new Promise((resolve) => (script.onload = resolve));
		}

		pyodide = await (window as any).loadPyodide({
			indexURL: "/pyodide/"
		});
	});

	async function runCode() {
		if (!pyodide) return;
		isRunning = true;
		output = "Running...";

		try {
			// Redirect Python standard output to capture stdout
			pyodide.runPython(`
                import sys
                import io
                sys.stdout = io.StringIO()
            `);

			await pyodide.runPythonAsync(code);

			const stdout = pyodide.runPython("sys.stdout.getvalue()");
			output = stdout || "Program executed successfully with no output.";
		} catch (err: any) {
			output = `Error:\n${err.message}`;
		} finally {
			isRunning = false;
		}
	}
</script>
<main>
    <h1>Lesson 1 - Introduction</h1>
    <p>Welcome to your first Python lesson! In this lesson we will learn what Python actually is.</p>
    <h2>What is Python?</h2>
    <section>
        <p>
            Python is widely used programming language, designed by Guido van Rossum. It was first released in 1991.
            It can be used for a variety of things, including:
        </p>
        <ul>
            <li>scripts: packages of python code which can be run locally to complete tasks</li>
            <li>math: perform advanced & complicated mathimatical calculations in an instant</li>
            <li>backend: performs operations in the back of websites like this!</li>
        </ul>
    </section>
    <h2>Why Python?</h2>
    <section>
        <p>Python can accomplish a vast range of tasks, often used to organize data and manipulate data. Because of this, Python is used for a variety of tasks. Some of these tasks include: </p>
        <ul>
            <li>Machine Learning & Neurel networks</li>
            <p>Python excels at training machine learning models</p>
            <li>Data Science</li>
            <p>Python can be used to analyze big data through graphs and statistics</p>
            <li>Engineering</li>
            <p>Python can be used to control hardware</p>
        </ul>
        <p>Running Python scripts is often more efficent at doing tasks then humans can, able to perform millions of operations in mere seconds. It also avoids human error.</p>
        <h3>hi</h3>
    </section>
    <h2>Run your first script!</h2>

    <div class="code-editor">
        <CodeMirror bind:value={code} lang={python()}/>
    </div>

    <div class="controls">
		<button onclick={runCode} disabled={!pyodide || isRunning}>
			{isRunning ? "Running..." : pyodide ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>

	{#if output}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output}</pre>
		</div>
	{/if}

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
        margin-top: 2rem;
        padding: 2rem;
        background-color: #b8bdb5;
        border-radius: 50px;
        padding-right: 7rem;
    }
    p {
        max-width: 700px;
    }
    .code-editor {
        height: 400px;
        border: 1px solid #ccc;
        border-radius: 8px;
        overflow: hidden;
    }
    .console {
		margin-top: 1rem;
		padding: 1rem;
		background-color: #1e1e1e;
		color: #00ff00;
		border-radius: 6px;
		font-family: monospace;
	}

</style>
