<svelte:head>
	<title>Lesson 2|CodeSite</title>
</svelte:head>
<script lang="ts">
    import CodeMirror from "svelte-codemirror-editor";
    import { python } from "@codemirror/lang-python";
    import { onMount } from "svelte";

    let code = $state('score = 85\nif score >= 70:\n\tprint("You passed!")');
    let code2 = $state('temperature = 75\nif temperature > 70:\n\tprint("It’s warm outside!")');
    let code3 = $state('age = 15\nif age >= 18:\n\tprint("Adult")\nelse:\n\tprint("Child")');
    let code4 = $state('grade = 88\nif grade >= 90:\n\tprint(“A”)\nelif grade >= 80:\n\tprint(“B”)\nelse:\n\tprint(“C”)');
    let code5 = $state('');
    let output = $state("");
    let output2 = $state("");
    let output3 = $state("");
    let output4 = $state("");
    let output5 = $state("");
    let isRunning = $state(false);
    let isRunning2 = $state(false);
    let isRunning3 = $state(false);
    let isRunning4 = $state(false);
    let isRunning5 = $state(false);
    let pyodide = $state<any>(null);
    let pyodide2 = $state<any>(null);
    let pyodide3 = $state<any>(null);
    let pyodide4 = $state<any>(null);
    let pyodide5 = $state<any>(null);

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
		pyodide2 = await (window as any).loadPyodide({
			indexURL: "/pyodide/"
		});
		pyodide3 = await (window as any).loadPyodide({
			indexURL: "/pyodide/"
		});
		pyodide4 = await (window as any).loadPyodide({
			indexURL: "/pyodide/"
		});
		pyodide5 = await (window as any).loadPyodide({
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
	async function runCode2() {
		if (!pyodide2) return;
		isRunning2 = true;
		output2 = "Running...";

		try {
			// Redirect Python standard output to capture stdout
			pyodide2.runPython(`
                import sys
                import io
                sys.stdout = io.StringIO()
            `);

			await pyodide2.runPythonAsync(code2);

			const stdout = pyodide2.runPython("sys.stdout.getvalue()");
			output2 = stdout || "Program executed successfully with no output.";
		} catch (err: any) {
			output2 = `Error:\n${err.message}`;
		} finally {
			isRunning2 = false;
		}
	}
	async function runCode3() {
		if (!pyodide3) return;
		isRunning3 = true;
		output3 = "Running...";

		try {
			// Redirect Python standard output to capture stdout
			pyodide3.runPython(`
                import sys
                import io
                sys.stdout = io.StringIO()
            `);

			await pyodide3.runPythonAsync(code3);

			const stdout = pyodide3.runPython("sys.stdout.getvalue()");
			output3 = stdout || "Program executed successfully with no output.";
		} catch (err: any) {
			output3 = `Error:\n${err.message}`;
		} finally {
			isRunning3 = false;
		}
	}
	async function runCode5() {
		if (!pyodide5) return;
		isRunning5 = true;
		output5 = "Running...";

		try {
			// Redirect Python standard output to capture stdout
			pyodide5.runPython(`
                import sys
                import io
                sys.stdout = io.StringIO()
            `);

			await pyodide5.runPythonAsync(code5);

			const stdout = pyodide5.runPython("sys.stdout.getvalue()");
			output5 = stdout || "Program executed successfully with no output.";
		} catch (err: any) {
			output5 = `Error:\n${err.message}`;
		} finally {
			isRunning5 = false;
		}
	}
	async function runCode4() {
		if (!pyodide4) return;
		isRunning4 = true;
		output4 = "Running...";

		try {
			// Redirect Python standard output to capture stdout
			pyodide4.runPython(`
                import sys
                import io
                sys.stdout = io.StringIO()
            `);

			await pyodide4.runPythonAsync(code4);

			const stdout = pyodide4.runPython("sys.stdout.getvalue()");
			output4 = stdout || "Program executed successfully with no output.";
		} catch (err: any) {
			output4 = `Error:\n${err.message}`;
		} finally {
			isRunning4 = false;
		}
	}

	let questions = [
        {
            id: 1,
            question: "What keyword is used to create a function in Python?",
            options: ["function", "func", "def", "define"],
            answer: "def"
        },
        {
            id: 2,
            question: "When are functions useful?",
            options: ["To store data instead of putting it in a datacenter", "When your code repeats a block of code multiple times", "When your code requires random data", "When computing power is limited"],
            answer: "When your code repeats a block of code multiple times"
        },
        {
            id: 3,
            question: "What is the difference between a parameter and an argument?",
            options: ["An argument is what you give the function when you call it, while a parameter is what the function receives", "An argument is what the function receives, while a parameter is what you give the function", "A parameter is reusuable while an argument is not", "An argument is harsh and bitter, while a parameter is just data"],
            answer: "An argument is what you give the function when you call it, while a parameter is what the function receives"
        },
        {
            id: 4,
            question: "What is the difference between print() and return?",
            options: ["return is only used and functions and transfers data, while print always shows data in the console", "return is only compatible with integers, while print works with any data type", "print() can only be used in functions, while return can be outside a function", "return is the outdated version of print"],
            answer: "return is only used and functions and transfers data, while print always shows data in the console"
        },
        {
            id: 5,
            question: "True or False: A variable created inside a function can always be used outside the function",
            options: ["True", "False"],
            answer: "False"
        },
        {
            id: 6,
            question: "Which keyword is used to retrieve Python library?",
            options: ["bring", "retrieve", "import", "library"],
            answer: "import"
        }
	]

	let currentIndex = $state(0);
	let score = $state(0);
	let selectedOption = $state<string | null>(null);
	let isFinished = $state(false);
	let userAnswers = $state<Array<{ question: string; answer: string; userAnswer: string; isCorrect: boolean }>>([]);

	function handleSelect(option) {
        selectedOption = option;
	}

	function nextQuestion() {
	    const currentQ = questions[currentIndex];
		const isCorrect = currentQ.answer === selectedOption
		if (isCorrect) {
            score += 1;
		}
		userAnswers.push({
		    question: currentQ.question,
			answer: currentQ.answer,
			userAnswer: selectedOption,
			isCorrect
		})

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
	let conditionData = $state([
	    {id: 1, operator: "==", meaning: "Compare/equal to"},
		{id: 2, operator: "!=", meaning: "Not equal to"},
		{id: 3, operator: ">", meaning: "Greater than"},
		{id: 4, operator: "<", meaning: "Less than"},
		{id: 5, operator: ">=", meaning: "Greater than or equal to"},
		{id: 6, operator: "<=", meaning: "Less than or equal to"}
	]);
</script>
<main>
    <h1>Lesson 2 - Loops & Conditional Statements </h1>
    <p>Estimated Completion Time: __ min</p>
    <p>In this lesson, we will learn how Python can make decisions and repeat tasks automatically.</p>

    <p>By the end of this lesson, you will be able to:</p>
    <ul>
        <li> Create programs using if statements</li>
        <li> Use if-else and if-elif-else statements</li>
        <li> Compare values using comparison operators</li>
        <li> Combine conditions using logical operators</li>
        <li> Create while loops</li>
        <li> Create for loops</li>
    </ul>
    <h3>What are Conditionals?</h3>
    <p>
        Conditionals allow a program to decide which code should be executed based on whether a condition is True or False.
    </p>
    <p>Instead of writing the same code many times, we can write it once inside a function and use it whenever we need it.</p>
    <p>Some common uses of conditionals include:</p>
    <ul>
        <li>Checking if a user entered the correct password</li>
        <li>Determining if student passed a test</li>
        <li>Deciding whether someone is old enough to vote</li>
        <li>Displaying different text based on the user’s input</li>
    </ul>
    <h3>If Statements</h3>
    <p>One of the simplest conditionals is the if statement.</p>
    <p>If the condition is True, Python runs the indented code underneath it. If the condition is False, Python skips it.</p>
    <div class="controls">
		<button onclick={runCode} disabled={!pyodide || isRunning}>
			{isRunning ? "Running..." : pyodide ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>

    <div class="code-editor">
        <CodeMirror bind:value={code} lang={python()}/>
    </div>

	{#if output}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output}</pre>
		</div>
	{/if}
	<p>Notice that:</p>
	<ul>
	    <li>Every if statement ends with a colon</li>
		<li>The code underneath is indented (tells Python the code belongs inside the if statement)</li>
	</ul>

    <h3>Comparison Operators</h3>
    <p>Conditions are created using comparison operators</p>
    <table>
    	<thead>
    		<tr>
    			<th>Operator</th>
    			<th>Meaning</th>
    		</tr>
    	</thead>
	    <tbody>
		    {#each conditionData as data (data.id)}
			    <tr>
				    <td>{data.operator}</td>
				    <td>{data.meaning}</td>
			    </tr>
		    {/each}
	    </tbody>
    </table>
    <p>Example:</p>

    <div class="controls">
		<button onclick={runCode2} disabled={!pyodide2 || isRunning}>
			{isRunning ? "Running..." : pyodide2 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>

	<div class="code-editor">
        <CodeMirror bind:value={code2} lang={python()}/>
    </div>

    {#if output2}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output2}</pre>
		</div>
	{/if}
	<p>
        Remember that = and == are different:
	</p>
	<ul>
	    <li>= assigns a value to a variable</li>
		<li>== compares two values</li>
	</ul>
    <h3>If-Else Statements</h3>
    <p>Sometimes you want your program to do one thing if a condition is True, and something else if it is False.</p>
    <p>This is done using an if-else statement:</p>
    <div class="controls">
		<button onclick={runCode3} disabled={!pyodide3 || isRunning3}>
			{isRunning3 ? "Running..." : pyodide3 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>

    <div class="code-editor">
        <CodeMirror bind:value={code3} lang={python()}/>
    </div>

	{#if output3}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output3}</pre>
		</div>
	{/if}

	<h3>If-Elif-Else Statements</h3>
	<p>If there are more than two possible outcomes, you can use elif, which stands for “else if.”</p>
	<p>Example:</p>
    <div class="controls">
		<button onclick={runCode4} disabled={!pyodide4 || isRunning}>
			{isRunning4 ? "Running..." : pyodide4 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>

    <div class="med-code-editor">
        <CodeMirror bind:value={code4} lang={python()}/>
    </div>

	{#if output4}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output4}</pre>
		</div>
	{/if}


	<h3>Logical Operators</h3>
	<p>
	    Sometimes you need to check multiple conditions at once
    </p>
    <p>
        Python provides three logical operators:
    </p>
    <p><strong>and</strong> - both conditions must be True.</p>
    <key><code>
        age = 15<br>
        has_schoolID = True<br>
        &nbsp; if age &lt;= 18 and has_schoolID:<br>
	    print(“Is A Student”)
    </code></key>
    <p><strong>or</strong> - at least one condition must be True.</p>
    <key><code>
        if age &lt= 18 or has_schoolID:<br>
	    &nbsp;print(“Is a Student”)
    </code></key>
    <p><strong>not</strong> - reverses a Boolean value.</p>
    <key><code>
        has_schoolID = False<br>
        if not has_schoolID:<br>
    	&nbsp;print(“Not A Student”)
    </code></key>

    <h3>Lab - Build your own function</h3>
    <div class="controls">
		<button onclick={runCode5} disabled={!pyodide5 || isRunning3}>
			{isRunning5 ? "Running..." : pyodide5 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>

    <div class="med-code-editor">
        <CodeMirror bind:value={code5} lang={python()}/>
    </div>

	{#if output5}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output5}</pre>
		</div>
	{/if}

    <h3>Parameters vs Arguments</h3>
    <p>A parameter is a variable listed inside a function's parentheses, it receives info. An argument is the value you give the function when you call it.</p>
    <key><code>
        def greet(name):<br>
	    &nbsp;print(“Hello,”, name)<br>
        <br>
        greet(“Alex”)
    </code></key>

    <p>Note: All mathematical operations follow PEMDAS order</p>
    <p>In this example:<p>
    <ul>
        <li><key><code>name</code></key> is the parameter</li>
        <li><key><code>“Alex”</code></key> is the argument</li>
    </ul>

	<h3>Post-Lesson Quiz</h3>
	<p>Demonstrate your understanding with this short quiz</p>

    <div class="quiz-box">
        {#if !isFinished}
            <h3>Question {currentIndex+1} out of {questions.length}</h3>
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
            <h3>Quiz Finished - Good job!</h3>
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
    .quiz-box {
        max-width: 500px;
        margin: 40px auto;
        padding: 24px;
        background: #5f7470;
        border-radius: 8px;
        box-shadow: 0 4px 10px rgba(0,0,0,0.1);
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
        background: #99A6A6;
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
    .next-btn, .restart-btn {
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

    table {
		width: 100%;
		border-collapse: collapse;
		margin-top: 1rem;
	}
	th, td {
		padding: 12px;
		border-bottom: 1px solid #ddd;
		text-align: left;
	}
	th {
		background-color: #f4f4f4;
	}
	    .active { color: green; font-weight: bold; }
	    .inactive { color: gray; }


</style>
