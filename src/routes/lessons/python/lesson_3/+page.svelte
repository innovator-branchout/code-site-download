<svelte:head>
	<title>Lesson 3|CodeSite</title>
</svelte:head>
<script lang="ts">
	import CodeMirror from "svelte-codemirror-editor";
	import { python } from "@codemirror/lang-python";
	import { onMount } from "svelte";

	// --- Code state ---
	let code1 = $state('favorite_foods = ["Pizza", "Tacos", "Pasta"]\n\nprint(favorite_foods)');
	let code2 = $state('favorite_foods = ["Pizza", "Tacos", "Pasta"]\n\nprint(favorite_foods[0])');
	let code3 = $state('favorite_foods = ["Pizza", "Tacos", "Pasta"]\n\nfavorite_foods.append("Ice Cream")\n\nprint(favorite_foods)');
	let code4 = $state('favorite_foods = ["Pizza", "Tacos", "Pasta"]\n\nfavorite_foods[1] = "Burgers"\n\nprint(favorite_foods)');
	let code5 = $state('favorite_foods = ["Pizza", "Tacos", "Pasta"]\n\nfor food in favorite_foods:\n    print(food)');
	let code6 = $state('');
	let code7 = $state('favorite_colors = ("Blue", "Green", "Purple")\n\nprint(favorite_colors)');
	let code8 = $state('favorite_colors = ("Blue", "Green", "Purple")\n\nprint(favorite_colors[1])');
	let code9 = $state('');
	let code10 = $state('student = {\n    "name": "Alex",\n    "grade": 8,\n    "favorite_subject": "Science"\n}\n\nprint(student)');
	let code11 = $state('student = {\n    "name": "Alex",\n    "grade": 8,\n    "favorite_subject": "Science"\n}\n\nprint(student["favorite_subject"])');
	let code12 = $state('student = {\n    "name": "Alex",\n    "grade": 8\n}\n\nstudent["favorite_color"] = "Blue"\n\nprint(student)');
	let code13 = $state('');
	let code14 = $state('pets = {"Dog", "Cat", "Dog", "Fish"}\n\nprint(pets)');
	let code15 = $state('pets = {"Dog", "Cat", "Dog", "Fish"}\n\npets.add("Bird")\n\nprint(pets)');
	let code16 = $state('');

	// --- Output state ---
	let output1 = $state("");
	let output2 = $state("");
	let output3 = $state("");
	let output4 = $state("");
	let output5 = $state("");
	let output6 = $state("");
	let output7 = $state("");
	let output8 = $state("");
	let output9 = $state("");
	let output10 = $state("");
	let output11 = $state("");
	let output12 = $state("");
	let output13 = $state("");
	let output14 = $state("");
	let output15 = $state("");
	let output16 = $state("");

	// --- isRunning state ---
	let isRunning1 = $state(false);
	let isRunning2 = $state(false);
	let isRunning3 = $state(false);
	let isRunning4 = $state(false);
	let isRunning5 = $state(false);
	let isRunning6 = $state(false);
	let isRunning7 = $state(false);
	let isRunning8 = $state(false);
	let isRunning9 = $state(false);
	let isRunning10 = $state(false);
	let isRunning11 = $state(false);
	let isRunning12 = $state(false);
	let isRunning13 = $state(false);
	let isRunning14 = $state(false);
	let isRunning15 = $state(false);
	let isRunning16 = $state(false);

	// --- Pyodide instances ---
	let pyodide1 = $state<any>(null);
	let pyodide2 = $state<any>(null);
	let pyodide3 = $state<any>(null);
	let pyodide4 = $state<any>(null);
	let pyodide5 = $state<any>(null);
	let pyodide6 = $state<any>(null);
	let pyodide7 = $state<any>(null);
	let pyodide8 = $state<any>(null);
	let pyodide9 = $state<any>(null);
	let pyodide10 = $state<any>(null);
	let pyodide11 = $state<any>(null);
	let pyodide12 = $state<any>(null);
	let pyodide13 = $state<any>(null);
	let pyodide14 = $state<any>(null);
	let pyodide15 = $state<any>(null);
	let pyodide16 = $state<any>(null);

	onMount(async () => {
		if (!(window as any).loadPyodide) {
			const script = document.createElement("script");
			script.src = "/pyodide/pyodide.js";
			document.head.appendChild(script);
			await new Promise((resolve) => (script.onload = resolve));
		}
		const loader = (window as any).loadPyodide;
		[
			pyodide1, pyodide2, pyodide3, pyodide4,
			pyodide5, pyodide6, pyodide7, pyodide8,
			pyodide9, pyodide10, pyodide11, pyodide12,
			pyodide13, pyodide14, pyodide15, pyodide16
		] = await Promise.all([
			loader({ indexURL: "/pyodide/" }),
			loader({ indexURL: "/pyodide/" }),
			loader({ indexURL: "/pyodide/" }),
			loader({ indexURL: "/pyodide/" }),
			loader({ indexURL: "/pyodide/" }),
			loader({ indexURL: "/pyodide/" }),
			loader({ indexURL: "/pyodide/" }),
			loader({ indexURL: "/pyodide/" }),
			loader({ indexURL: "/pyodide/" }),
			loader({ indexURL: "/pyodide/" }),
			loader({ indexURL: "/pyodide/" }),
			loader({ indexURL: "/pyodide/" }),
			loader({ indexURL: "/pyodide/" }),
			loader({ indexURL: "/pyodide/" }),
			loader({ indexURL: "/pyodide/" }),
			loader({ indexURL: "/pyodide/" }),
		]);
	});

	async function makeRunner(
		getPyodide: () => any,
		getCode: () => string,
		setRunning: (v: boolean) => void,
		setOutput: (v: string) => void
	) {
		const py = getPyodide();
		if (!py) return;
		setRunning(true);
		setOutput("Running...");
		try {
			py.runPython(`
import sys
import io
sys.stdout = io.StringIO()
`);
			const snapshot = $state.snapshot(getCode());
			await py.runPythonAsync(snapshot);
			const stdout = py.runPython("sys.stdout.getvalue()");
			setOutput(stdout || "Program executed successfully with no output.");
		} catch (err: any) {
			setOutput(`Error:\n${err.message}`);
		} finally {
			setRunning(false);
		}
	}

	function runCode1() { return makeRunner(() => pyodide1, () => code1, v => { isRunning1 = v; }, v => { output1 = v; }); }
	function runCode2() { return makeRunner(() => pyodide2, () => code2, v => { isRunning2 = v; }, v => { output2 = v; }); }
	function runCode3() { return makeRunner(() => pyodide3, () => code3, v => { isRunning3 = v; }, v => { output3 = v; }); }
	function runCode4() { return makeRunner(() => pyodide4, () => code4, v => { isRunning4 = v; }, v => { output4 = v; }); }
	function runCode5() { return makeRunner(() => pyodide5, () => code5, v => { isRunning5 = v; }, v => { output5 = v; }); }
	function runCode6() { return makeRunner(() => pyodide6, () => code6, v => { isRunning6 = v; }, v => { output6 = v; }); }
	function runCode7() { return makeRunner(() => pyodide7, () => code7, v => { isRunning7 = v; }, v => { output7 = v; }); }
	function runCode8() { return makeRunner(() => pyodide8, () => code8, v => { isRunning8 = v; }, v => { output8 = v; }); }
	function runCode9() { return makeRunner(() => pyodide9, () => code9, v => { isRunning9 = v; }, v => { output9 = v; }); }
	function runCode10() { return makeRunner(() => pyodide10, () => code10, v => { isRunning10 = v; }, v => { output10 = v; }); }
	function runCode11() { return makeRunner(() => pyodide11, () => code11, v => { isRunning11 = v; }, v => { output11 = v; }); }
	function runCode12() { return makeRunner(() => pyodide12, () => code12, v => { isRunning12 = v; }, v => { output12 = v; }); }
	function runCode13() { return makeRunner(() => pyodide13, () => code13, v => { isRunning13 = v; }, v => { output13 = v; }); }
	function runCode14() { return makeRunner(() => pyodide14, () => code14, v => { isRunning14 = v; }, v => { output14 = v; }); }
	function runCode15() { return makeRunner(() => pyodide15, () => code15, v => { isRunning15 = v; }, v => { output15 = v; }); }
	function runCode16() { return makeRunner(() => pyodide16, () => code16, v => { isRunning16 = v; }, v => { output16 = v; }); }

	// --- Quiz ---
	let questions = [
		{
			id: 1,
			question: "What symbols are used to create a tuple?",
			options: ["[ ]", "{ }", "( )", "< >"],
			answer: "( )"
		},
		{
			id: 2,
			question: "What is the biggest difference between a list and a tuple?",
			options: [
				"A list uses curly braces, a tuple uses square brackets",
				"A list can be changed after creation, but a tuple cannot",
				"A tuple can store more items than a list",
				"A list stores only numbers, a tuple stores only strings"
			],
			answer: "A list can be changed after creation, but a tuple cannot"
		},
		{
			id: 3,
			question: "What is a key in a dictionary?",
			options: [
				"A number used to access items by position",
				"A label used to identify and access a value",
				"A special symbol that locks the dictionary",
				"The first item stored in the dictionary"
			],
			answer: "A label used to identify and access a value"
		},
		{
			id: 4,
			question: "How do you access a value in a dictionary?",
			options: [
				"Using an index number in square brackets, like dict[0]",
				"Using the .get() method only",
				"Using the key in square brackets, like dict[\"key\"]",
				"Using a for loop only"
			],
			answer: "Using the key in square brackets, like dict[\"key\"]"
		},
		{
			id: 5,
			question: "What makes a set different from a list?",
			options: [
				"A set can only store numbers",
				"A set automatically removes duplicate items",
				"A set is ordered and indexed",
				"A set cannot be printed"
			],
			answer: "A set automatically removes duplicate items"
		},
		{
			id: 6,
			question: "What happens if you add the same item to a set twice?",
			options: [
				"The set stores both copies of the item",
				"Python raises an error",
				"The set only keeps one copy of the item",
				"The original item is replaced by the new one"
			],
			answer: "The set only keeps one copy of the item"
		},
		{
			id: 7,
			question: "You want to store the names of your five favorite games in order, and you may add more later. Which collection type is best?",
			options: ["Tuple", "List", "Dictionary", "Set"],
			answer: "List"
		},
		{
			id: 8,
			question: "You want to store info about a pet — its name, age, and type of animal — with labels for each piece of info. Which collection type is best?",
			options: ["List", "Tuple", "Dictionary", "Set"],
			answer: "Dictionary"
		}
	];

	let currentIndex = $state(0);
	let score = $state(0);
	let selectedOption = $state<string | null>(null);
	let isFinished = $state(false);
	let userAnswers = $state<Array<{ question: string; answer: string; userAnswer: string; isCorrect: boolean }>>([]);

	function handleSelect(option: string) {
		selectedOption = option;
	}

	function nextQuestion() {
		const currentQ = questions[currentIndex];
		const isCorrect = currentQ.answer === selectedOption;
		if (isCorrect) {
			score += 1;
		}
		userAnswers.push({
			question: currentQ.question,
			answer: currentQ.answer,
			userAnswer: selectedOption ?? "",
			isCorrect
		});
		selectedOption = null;
		if (currentIndex < questions.length - 1) {
			currentIndex += 1;
		} else {
			isFinished = true;
		}
	}

	function restartQuiz() {
		currentIndex = 0;
		score = 0;
		selectedOption = null;
		isFinished = false;
		userAnswers = [];
	}
</script>

<main>
	<h1>Lesson 3 - Collections</h1>
	<p>Estimated Completion Time: 45 min</p>
	<p>In this lesson, we will learn how Python stores multiple pieces of information inside a single variable.</p>
	<p>By the end of this lesson, you will be able to:</p>
	<ul>
		<li>Create a list, tuple, dictionary, and set</li>
		<li>Add new items to a list, dictionary, or set</li>
		<li>Access values using a key</li>
		<li>Access items within a list or tuple</li>
		<li>Explain the difference between a list and a tuple</li>
		<li>Modify list items</li>
		<li>Loop through a list</li>
		<li>Add new key-value pairs in a dictionary</li>
		<li>Explain why duplicate items are removed from a set</li>
	</ul>

	<!-- ===== LISTS ===== -->
	<h2>Lists</h2>

	<h3>What is a list?</h3>
	<p>
		Sometimes we want to store many related values instead of many separate variables. Python allows us to do this using a list.
	</p>
	<p>For example, instead of writing:</p>
	<div class="code-editor">
		<CodeMirror value={`food1 = "Pizza"\nfood2 = "Tacos"\nfood3 = "Pasta"\n\nprint(food1)\nprint(food2)\nprint(food3)`} lang={python()} readonly />
	</div>
	<p>We can create a single list:</p>
	<div class="controls">
		<button onclick={runCode1} disabled={!pyodide1 || isRunning1}>
			{isRunning1 ? "Running..." : pyodide1 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>
	<div class="code-editor">
		<CodeMirror bind:value={code1} lang={python()} />
	</div>
	{#if output1}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output1}</pre>
		</div>
	{/if}
	<p>Notice that the list uses square brackets <key><code>[ ]</code></key> and each item is separated by a comma. Try changing one of the foods!</p>

	<h3>Accessing list items</h3>
	<p>Each item inside a list has a numbered position called an <strong>index</strong>. Python begins counting at 0.</p>
	<table class="index-table">
		<thead>
			<tr><th>Index</th><th>0</th><th>1</th><th>2</th></tr>
		</thead>
		<tbody>
			<tr><td>Value</td><td>Pizza</td><td>Tacos</td><td>Pasta</td></tr>
		</tbody>
	</table>
	<p>To access the first item:</p>
	<div class="controls">
		<button onclick={runCode2} disabled={!pyodide2 || isRunning2}>
			{isRunning2 ? "Running..." : pyodide2 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>
	<div class="code-editor">
		<CodeMirror bind:value={code2} lang={python()} />
	</div>
	{#if output2}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output2}</pre>
		</div>
	{/if}
	<p>Try printing the second and third items. Since counting starts at 0, the second item has an index of 1.</p>

	<h3>Adding items</h3>
	<p>Lists can grow as your program runs. You can add new items to the end of the list using <key><code>append()</code></key>.</p>
	<div class="controls">
		<button onclick={runCode3} disabled={!pyodide3 || isRunning3}>
			{isRunning3 ? "Running..." : pyodide3 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>
	<div class="code-editor">
		<CodeMirror bind:value={code3} lang={python()} />
	</div>
	{#if output3}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output3}</pre>
		</div>
	{/if}
	<p>Try adding another food of your own.</p>

	<h3>Modifying items</h3>
	<p>You can also replace an existing item by assigning a new value to its index.</p>
	<div class="controls">
		<button onclick={runCode4} disabled={!pyodide4 || isRunning4}>
			{isRunning4 ? "Running..." : pyodide4 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>
	<div class="code-editor">
		<CodeMirror bind:value={code4} lang={python()} />
	</div>
	{#if output4}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output4}</pre>
		</div>
	{/if}
	<p>Try changing another item.</p>

	<h3>Using a loop</h3>
	<p>If a list contains many items that you want to print, writing multiple print statements becomes difficult. Instead, we can use a <key><code>for</code></key> loop.</p>
	<div class="controls">
		<button onclick={runCode5} disabled={!pyodide5 || isRunning5}>
			{isRunning5 ? "Running..." : pyodide5 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>
	<div class="code-editor">
		<CodeMirror bind:value={code5} lang={python()} />
	</div>
	{#if output5}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output5}</pre>
		</div>
	{/if}

	<h3>Lab — Build your own list</h3>
	<p>Create a list with five of your favorite foods, movies, games, or hobbies. By the end, your program should:</p>
	<ul>
		<li>Create a list with at least five items</li>
		<li>Print the entire list</li>
		<li>Print the first item</li>
		<li>Add one new item</li>
		<li>Replace one existing item</li>
		<li>Print every item using a loop</li>
	</ul>
	<div class="controls">
		<button onclick={runCode6} disabled={!pyodide6 || isRunning6}>
			{isRunning6 ? "Running..." : pyodide6 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>
	<div class="big-code-editor">
		<CodeMirror bind:value={code6} lang={python()} />
	</div>
	{#if output6}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output6}</pre>
		</div>
	{/if}

	<!-- ===== TUPLES ===== -->
	<h2>Tuples</h2>

	<h3>What is a tuple?</h3>
	<p>A tuple stores multiple pieces of info, just like a list. The difference is that tuples <strong>can't be changed</strong> after they're created. Tuples use parentheses <key><code>( )</code></key> instead of square brackets.</p>
	<div class="controls">
		<button onclick={runCode7} disabled={!pyodide7 || isRunning7}>
			{isRunning7 ? "Running..." : pyodide7 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>
	<div class="code-editor">
		<CodeMirror bind:value={code7} lang={python()} />
	</div>
	{#if output7}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output7}</pre>
		</div>
	{/if}
	<p>Try changing one of the colors and running the program again. What happens?</p>

	<h3>Accessing tuple items</h3>
	<p>Just like lists, tuples use indexes that start at 0.</p>
	<div class="controls">
		<button onclick={runCode8} disabled={!pyodide8 || isRunning8}>
			{isRunning8 ? "Running..." : pyodide8 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>
	<div class="code-editor">
		<CodeMirror bind:value={code8} lang={python()} />
	</div>
	{#if output8}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output8}</pre>
		</div>
	{/if}
	<p>Try printing the first and third colors.</p>

	<h3>Why use a tuple?</h3>
	<p>Sometimes you don't want the info to change. For example:</p>
	<ul>
		<li>The months of the year</li>
		<li>The days of the week</li>
		<li>The coordinates of a point</li>
	</ul>
	<p>A tuple helps protect the info from getting changed by accident.</p>

	<h3>Lab — Build your own tuple</h3>
	<p>Create a tuple containing the names of the four seasons. Once you're done:</p>
	<ul>
		<li>Print the entire tuple</li>
		<li>Print the first season</li>
		<li>Print the last season</li>
	</ul>
	<div class="controls">
		<button onclick={runCode9} disabled={!pyodide9 || isRunning9}>
			{isRunning9 ? "Running..." : pyodide9 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>
	<div class="big-code-editor">
		<CodeMirror bind:value={code9} lang={python()} />
	</div>
	{#if output9}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output9}</pre>
		</div>
	{/if}

	<!-- ===== DICTIONARIES ===== -->
	<h2>Dictionaries</h2>

	<h3>What is a dictionary?</h3>
	<p>A dictionary stores info in <strong>key-value pairs</strong>. Think of it like a real dictionary, where the word is the key, and the definition is the value. Each key has a matching value. Python dictionaries use curly braces <key><code>{"{ }"}</code></key>.</p>
	<div class="controls">
		<button onclick={runCode10} disabled={!pyodide10 || isRunning10}>
			{isRunning10 ? "Running..." : pyodide10 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>
	<div class="med-code-editor">
		<CodeMirror bind:value={code10} lang={python()} />
	</div>
	{#if output10}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output10}</pre>
		</div>
	{/if}

	<h3>Accessing values</h3>
	<p>Instead of using an index like for lists and tuples, dictionaries use <strong>keys</strong> to access values.</p>
	<div class="controls">
		<button onclick={runCode11} disabled={!pyodide11 || isRunning11}>
			{isRunning11 ? "Running..." : pyodide11 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>
	<div class="med-code-editor">
		<CodeMirror bind:value={code11} lang={python()} />
	</div>
	{#if output11}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output11}</pre>
		</div>
	{/if}
	<p>Now try printing the student's name.</p>

	<h3>Adding info</h3>
	<p>You can add another key-value pair to a dictionary at any time.</p>
	<div class="controls">
		<button onclick={runCode12} disabled={!pyodide12 || isRunning12}>
			{isRunning12 ? "Running..." : pyodide12 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>
	<div class="med-code-editor">
		<CodeMirror bind:value={code12} lang={python()} />
	</div>
	{#if output12}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output12}</pre>
		</div>
	{/if}
	<p>Try adding another piece of info about the student.</p>

	<h3>Lab — Build your own dictionary</h3>
	<p>Create a dictionary about yourself. Include at least:</p>
	<ul>
		<li>Name</li>
		<li>Favorite food</li>
		<li>Favorite hobby</li>
	</ul>
	<p>Then print each value using its key. Lastly, add another key-value pair and print it as well.</p>
	<div class="controls">
		<button onclick={runCode13} disabled={!pyodide13 || isRunning13}>
			{isRunning13 ? "Running..." : pyodide13 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>
	<div class="big-code-editor">
		<CodeMirror bind:value={code13} lang={python()} />
	</div>
	{#if output13}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output13}</pre>
		</div>
	{/if}

	<!-- ===== SETS ===== -->
	<h2>Sets</h2>

	<h3>What is a set?</h3>
	<p>A set stores a collection of <strong>unique items</strong>. If the same item appears more than once, Python only keeps one copy.</p>
	<div class="controls">
		<button onclick={runCode14} disabled={!pyodide14 || isRunning14}>
			{isRunning14 ? "Running..." : pyodide14 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>
	<div class="code-editor">
		<CodeMirror bind:value={code14} lang={python()} />
	</div>
	{#if output14}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output14}</pre>
		</div>
	{/if}
	<p>Notice that "Dog" only appears once in the output, even though it was added twice.</p>

	<h3>Adding items</h3>
	<p>Use <key><code>add()</code></key> to add a new item to a set. Try adding another animal, then try adding "Dog" again. What happens?</p>
	<div class="controls">
		<button onclick={runCode15} disabled={!pyodide15 || isRunning15}>
			{isRunning15 ? "Running..." : pyodide15 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>
	<div class="med-code-editor">
		<CodeMirror bind:value={code15} lang={python()} />
	</div>
	{#if output15}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output15}</pre>
		</div>
	{/if}

	<h3>When are sets useful?</h3>
	<p>Sets are useful when you only want one copy of each item. For example:</p>
	<ul>
		<li>You want to know what types of fruits you have in the house</li>
		<li>You want to know what species of animals are in a forest</li>
		<li>You want to know what types of hair colors the students in your class have</li>
	</ul>

	<h3>Lab — Build your own set</h3>
	<p>Create a set of five fruits. Once you're done:</p>
	<ul>
		<li>Print the set</li>
		<li>Add another fruit</li>
		<li>Try adding one of the fruits a second time — did the set change?</li>
	</ul>
	<div class="controls">
		<button onclick={runCode16} disabled={!pyodide16 || isRunning16}>
			{isRunning16 ? "Running..." : pyodide16 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>
	<div class="big-code-editor">
		<CodeMirror bind:value={code16} lang={python()} />
	</div>
	{#if output16}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output16}</pre>
		</div>
	{/if}

	<!-- ===== COMPARISON TABLE ===== -->
	<h2>Choosing the right collection</h2>
	<p>Now that we've learned many ways to store groups of information, let's compare them. When is it best to use one over the other?</p>
	<table class="collection-table">
		<thead>
			<tr>
				<th>Collection</th>
				<th>Symbols</th>
				<th>Can it Change?</th>
				<th>Best Used For</th>
			</tr>
		</thead>
		<tbody>
			<tr>
				<td>List</td>
				<td><code>[ ]</code></td>
				<td>Yes</td>
				<td>A collection that may change</td>
			</tr>
			<tr>
				<td>Tuple</td>
				<td><code>( )</code></td>
				<td>No</td>
				<td>Info that should stay the same</td>
			</tr>
			<tr>
				<td>Dictionary</td>
				<td><code>{"{ }"}</code></td>
				<td>Yes</td>
				<td>Info with labels and matching values/descriptions</td>
			</tr>
			<tr>
				<td>Set</td>
				<td><code>{"{ }"}</code></td>
				<td>Yes</td>
				<td>An unordered collection of unique items (no duplicates)</td>
			</tr>
		</tbody>
	</table>

	<!-- ===== QUIZ ===== -->
	<h3>Post-Lesson Quiz</h3>
	<p>Demonstrate your understanding with this short quiz.</p>
	<div class="quiz-box">
		{#if !isFinished}
			<h3>Question {currentIndex + 1} out of {questions.length}</h3>
			<p class="question-text">{questions[currentIndex].question}</p>
			<div class="options-list">
				{#each questions[currentIndex].options as option}
					<button class="option-btn {selectedOption === option ? 'selected' : ''}" onclick={() => handleSelect(option)}>
						{option}
					</button>
				{/each}
			</div>
			<button class="next-btn" disabled={!selectedOption} onclick={nextQuestion}>
				Next Question
			</button>
		{:else}
			<h3>Quiz Finished — Good job!</h3>
			<p>Your final score is {score} out of {questions.length}</p>
			<div class="review">
				<h4>Quiz Summary:</h4>
				{#each userAnswers as item, index}
					<div class="result-card {item.isCorrect ? 'correct' : 'incorrect'}">
						<p class="review-question"><strong>Q{index + 1}:</strong> {item.question}</p>
						<p>
							Your Answer:
							<span class="badge {item.isCorrect ? 'bg-correct' : 'bg-incorrect'}">
								{item.userAnswer} {item.isCorrect ? '✓' : '✗'}
							</span>
						</p>
						{#if !item.isCorrect}
							<p class="correct-answer">
								Correct Answer: <strong>{item.answer}</strong>
							</p>
						{/if}
					</div>
				{/each}
			</div>
			<button class="try-again-btn" onclick={restartQuiz}>Try Again</button>
		{/if}
	</div>
</main>

<style>
	main {
		max-width: 1000px;
		min-height: calc(100vh - 70px);
		margin: 10px auto;
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
	.med-code-editor {
		height: 200px;
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
		background-color: #00c04b;
	}
	ul {
		list-style-type: disc;
	}
	.letter-list {
		list-style-type: lower-alpha;
	}
	code {
		font-size: 1rem;
	}
	li {
		max-width: 700px;
	}
	.index-table {
		border-collapse: collapse;
		margin: 1rem 0;
	}
	.index-table th,
	.index-table td {
		border: 1px solid #ccc;
		padding: 8px 16px;
		text-align: center;
	}
	.index-table th {
		background-color: #e8e8e8;
	}
	.collection-table {
		border-collapse: collapse;
		margin: 1rem 0;
		max-width: 750px;
		width: 100%;
	}
	.collection-table th,
	.collection-table td {
		border: 1px solid #ccc;
		padding: 10px 16px;
		text-align: left;
	}
	.collection-table th {
		background-color: #e8e8e8;
		font-weight: bold;
	}
	.collection-table tr:nth-child(even) {
		background-color: #f5f5f5;
	}
	.quiz-box {
		max-width: 500px;
		margin: 40px auto;
		padding: 24px;
		background: #5f7470;
		border-radius: 8px;
		box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
		font-family: sans-serif;
		color: #e0e2db;
	}
	.question-text {
		font-size: 1rem;
		font-weight: bold;
		margin-bottom: 16px;
		color: #e0e2db;
	}
	.options-list {
		display: flex;
		flex-direction: column;
		gap: 10px;
		margin-bottom: 20px;
	}
	.option-btn {
		padding: 12px;
		border: 1px solid;
		background: #99a6a6;
		border-radius: 4px;
		cursor: pointer;
		text-align: left;
		font-size: 1rem;
	}
	.option-btn.selected {
		background: #889696;
		color: #fff;
		border-color: #889696;
	}
	.next-btn,
	.restart-btn {
		width: 100%;
		padding: 12px;
		background: #d2d4c8;
		border: none;
		border-radius: 4px;
		font-size: 1rem;
		cursor: pointer;
	}
	.next-btn:disabled {
		background: #ccc;
		cursor: not-allowed;
	}
	.try-again-btn {
		width: 100%;
		padding: 12px;
		background: #d2d4c8;
		border: none;
		border-radius: 4px;
		font-size: 1rem;
		cursor: pointer;
	}
	.review {
		text-align: left;
	}
	.result-card {
		padding: 12px 16px;
		border-radius: 6px;
		border-left: 5px solid #ccc;
		background-color: #d2d3c8;
		color: #5f7470;
		margin-bottom: 1rem;
	}
	.correct-answer {
		color: #2e7d32;
		font-size: 0.9rem;
		margin-top: 4px;
	}
	.bg-correct {
		color: #2e7d32;
	}
	.bg-incorrect {
		color: #c62828;
	}
</style>
