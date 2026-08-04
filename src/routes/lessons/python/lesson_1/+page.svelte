<svelte:head>
	<title>Lesson 1|CodeSite</title>
</svelte:head>
<script lang="ts">
    import CodeMirror from "svelte-codemirror-editor";
    import { python } from "@codemirror/lang-python";
    import { onMount } from "svelte";

    let code = $state('print("Hello World!")');
    let code2 = $state('my_first_variable = "Hello World"\nprint(my_first_variable)');
    let code3 = $state('# instantiate variables\nx = 12\ny = 5\n\n#Basic Math\nprint(x + y)#12 + 5 = 17\nprint(x - y)#12 - 5 = 7\nprint(x * y)#12 * 5 = 60\n\n#Division Variants\nprint(x / y)#12 / 5 = 2.4\nprint(x // y)#12 // 5 = 2\nprint(x % y)#12 % 5 = 2\n\n#Exponent\nprint(x ** y)#12^5 = 248832');
    let output = $state("");
    let output2 = $state("");
    let output3 = $state("");
    let isRunning = $state(false);
    let isRunning2 = $state(false);
    let isRunning3 = $state(false);
    let pyodide = $state<any>(null);
    let pyodide2 = $state<any>(null);
    let pyodide3 = $state<any>(null);

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

	let questions = [
        {
            id: 1,
            question: "What is the python identifier for a file?",
            options: [".python", ".py", ".script", ".language"],
            answer: ".py"
        },
        {
            id: 2,
            question: "Where does the print function output to?",
            options: ["The script file", "The frontend side", "a .txt file", "The console"],
            answer: "The console"
        },
        {
            id: 3,
            question: "Which of the following correctly instantiates a variable in python?",
            options: ["x = 5", "5 = x", "variable x = 5", "setVariable(x, 5)"],
            answer: "x = 5"
        },
        {
            id: 4,
            question: "What is the identifier for a comment in python?",
            options: ["#", "$", "//", "@"],
            answer: "#"
        },
        {
            id: 5,
            question: "What is the difference between an integer and a float?",
            option: ["A float is stored in the floating dictionary in the sky, while an int is not", "A float contains decimal values, while an int does not", "An integer is a number, while a float is not", "A float contains multiple integers"],
            answer: "A float contains decimal values, while an int does not"
        },
        {
            id: 6,
            question: " Solve the following math expression: ((5 + 1) * (6 / 3) + (3 - 1)**2) % 3",
            option: ["1", "3", "11", "2"],
            answer: "1"
        }
	]

	let currentIndex = 0;
	let score = 0;
	let selectedOption = null;
	let isFinished = false;

	function handleSelect(option) {
        selectedOption = option;
	}

	function nextQuestion() {
        if (selectedOption == questions[currentIndex].answer){
            score += 1;
        }

        selectedOption = null;

        if (currentIndex < questions.length -1) {
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
	}
</script>
<main>
    <h1>Lesson 1 - Python Fundamentals</h1>
    <p>Estimated Completion Time: __ min</p>
    <p>In this lesson, we will go over the fundamentals of Python, allowing you to create your first script! </p>

    <p>By the end of this lesson, you will be able to:</p>
    <ul>
        <li> Identify the capabilities of Python</li>
        <li> Set-up and run a python script</li>
        <li> Use the print function</li>
        <li> Create & manipulate variables</li>
        <li> Identify data types</li>
        <li> Complete basic math operations using python</li>
    </ul>
    <h3>What is Python?</h3>
    <section>
        <p>
            Python is a common scripting language, designed for readability. It has many strong capabilities and use cases. Some of these include:
        </p>
        <ul>
            <li>Automatic Scripting: Python scripts can automate tasks that would have otherwise taken hours to do in mere seconds. </li>
            <li>Data Science and Analyzation: Python can analyze and display big data </li>
            <li>Artificial Intelligence and Machine Learning: Python supports training AI models with libraries such as Pytorch</li>
            <li>Web Development: Python serves as the backend of many web applications</li>
        </ul>
    </section>
    <h3>First Set-up</h3>
    <section>
        <p>Usually, you need to set-up an online workspace before running scripts.</p>
        <ol>
            <li>
                Create a folder called **my-first-script**. This will store your first project
            </li>
            <li>
                Within that folder, create a file called **script.py**
                <ol class="letter-list">
                    <li>All python files must end with .py, otherwise it won’t be recognized as a python file.</li>
                    <li>The text before .py is the file's unique identifier, make sure you choose a useful name you’ll remember!</li>
                </ol>
            </li>
        </ol>
        <p>Instead of creating a project, we also provide a built-in text-editor for python. </p>
    </section>
    <h3>Print Function</h3>
    <p>The print function is a built in function in python. It is extremely useful for debugging and displaying values. Here is an example. Click the green “Run” button to see what happens:</p>

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
	<p>
        When run, the text “Hello World” will be outputted to the console below. The **script.py** file may be run using the following command on the terminal: <br>
    </p>

    <pre><code>
    python script.py
    </code></pre>

    <p>
        As you can see, whatever is within the parenthesis, (), and quotes, “”, after “print” is printed onto the console. Try changing text within the print function then click the “Run” button again.
	</p>

	<h3>Variables</h3>
	<p>Python uses variables, which store blocks of information within them and all have an unique identifier. Here is an example of creating a variable. </p>

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
	<p>When the green “Run” button is clicked, it outputs “Hello World” just like the first example. However, quite a few things are different. </p>
	<ul>
        <li>
            Instead of instantly printing “Hello World”, the string is first assigned to a variable called “my_first_variable”
            <ul>
                <li>The single equal sign assigns the value to the variable. </li>
                <li>The variable name should be to the left of the equal sign, while the variable value should be to the right of the equal sign.</li>
            </ul>
        </li>
        <li>After assigning the variable, we put it in the print function. This automatically retrieves the information stored in the variable, printing out “Hello World”.</li>
	</ul>

	<h3>Comments</h3>
	<p>Comments are non-functioning parts of code that make your code more readable. Good programmers should always use comments to stay organized. Comments are identified by a hashtag(#)</p>
	<p>Example:</p>
	<key><code>
	#This is a comment, and will not be run.<br>
    #The line below will do nothing, as it is a comment <br>
    #print(“hello world)”
    </code></key>

    <h3>Data Types</h3>
    <p>The statement “Hello World”  represents a string, which is a text-like object. All strings are encompassed by quotation marks. However, there are many other data types. Here are the main datatypes:</p>
    <p><strong>Integers: </strong> basic numbers used in mathematical operations, no decimals are supported. It comes from the built-in python int class.</p>
    <p>Here is how you define an int:</p>
    <key><code>
    x = 5
    </code></key>

    <p><strong>Floats: </strong> numbers which support decimal places, but take up more memory than ints. If applicable, always use int’s instead of floats to save memory. Comes from the built-in python float class. </p>
    <p>Here is how you define a float: </p>
    <key><code>
    x = 3.14
    </code></key>

    <p><strong>Strings:</strong> represent text, can be thought of as a list of characters. Strings should always be encompassed by quotation marks(“”). Comes from the built-in python str class. </p>
    <p>Again, here is how you define a string</p>
    <key><code>
    x = “Hello World”
    </code></key>

    <p><strong>Boolean:</strong> represents true or false values. Values can either be True or False (Note: case matters!). Comes from the built-in python bool class. </p>
    <p>Here is how you define a boolean:</p>
    <key><code>
    x = True
    </code></key>

    <p>Data types all have their unique properties and uses, and sometimes you may convert the data type of a variable. Here is an example:</p>
    <key><code>
    # instantiate x, which is an integer<br>
    x = 5<br>
    # x is now a string, “5”<br>
    x = str(x)
    </code></key>

    <h3>Arithmetic Operations</h3>
    <p>Python contains several arithmetic operators used to perform math with integers or floats. Here is a list of common arithmetic operators</p>
    <ul>
        <li>Addition(+): used to add 2 numbers together and get its sum.</li>
        <li>Subtraction(-): used to subtract 1 number from another</li>
        <li>Multiplication(*): used to multiply two numbers together </li>
        <li>
            Division(/): used to divide two numbers and always returns a float
            <ul>
                <li>Example: 5 / 2 = 2.5</li>
            </ul>
        </li>
        <li>
            Floor Division(//): used to divide two numbers and always returns an int
            <ul>
                <li>Rounds down to the nearest integer</li>
                <li>Example: 5 // 2 = 2</li>
            </ul>
        </li>
        <li>
            Modulus(%): used to get the remainder after dividing
            <ul>
                <li>Example: 5 % 2 = 1</li>
            </ul>
        </li>
        <li>
            Exponent(**): returns one number to the power of another
            <ul>
                <li>Example: 5**2 = 25</li>
            </ul>
        </li>
        <li>
            Parenthesis: gives an operation priority over another
            <ul>
                <li>Example: (5+1) * 5 = 30, while 5+1 * 5 = 10 </li>
            </ul>
        </li>

    </ul>

    <p>Note: All mathematical operations follow PEMDAS order</p>
    <p>Here is a code example:</p>
    <div class="controls">
		<button onclick={runCode3} disabled={!pyodide3 || isRunning3}>
			{isRunning3 ? "Running..." : pyodide3 ? "▶ Run Code" : "Loading Python..."}
		</button>
	</div>

    <div class="big-code-editor">
        <CodeMirror bind:value={code3} lang={python()}/>
    </div>

	{#if output3}
		<div class="console">
			<h3>Output:</h3>
			<pre>{output3}</pre>
		</div>
	{/if}
    <p>Note: feel free to play around with the text-editor!</p>
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
    background: #f9f9f9;
    border-radius: 8px;
    box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    font-family: sans-serif;
    }
    .question-text {
        font-size: 1.2rem;
        font-weight: bold;
        margin-bottom: 16px;
    }
    .options-list {
        display: flex;
        flex-direction: column;
        gap: 10px;
        margin-bottom: 20px;
    }
    .option-btn {
        padding: 12px;
        border: 1px solid #ccc;
        background: #fff;
        border-radius: 4px;
        cursor: pointer;
        text-align: left;
        font-size: 1rem;
    }
    .option-btn.selected {
        background: #ff3e00;
        color: #fff;
        border-color: #ff3e00;
    }
    .next-btn, .restart-btn {
        width: 100%;
        padding: 12px;
        background: #222;
        color: #fff;
        border: none;
        border-radius: 4px;
        font-size: 1rem;
        cursor: pointer;
    }
    .next-btn:disabled {
        background: #ccc;
        cursor: not-allowed;
    }

</style>
