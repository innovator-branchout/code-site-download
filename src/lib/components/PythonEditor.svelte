<script lang="ts">
    import CodeMirror from "svelte-codemirror-editor";
    import { python } from "@codemirror/lang-python";
    import { onMount, onDestroy } from "svelte";

    export let code = $state('print("Hello World!")');
    export let output = $state("");
    export let isRunning = $state(false);
    export let pyodide = $state<any>(null);
    export let runCodeFunction = $state<() => Promise<void>>(async () => {});
    export let stopExecution = $state<() => void>(() => {});

    let codeEditorRef: any = null;

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
        if (!pyodide || isRunning) return;

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

    function stopCode() {
        if (pyodide && pyodide.cancelAsync) {
            try {
                pyodide.cancelAsync();
                output = "Execution cancelled by user.";
            } catch (e) {
                console.error("Error stopping execution:", e);
                output = "Error stopping execution.";
            }
        }
    }

    // Set up the runCodeFunction and stopExecution for external use
    $: runCodeFunction = runCode;
    $: stopExecution = stopCode;

    onDestroy(() => {
        if (pyodide && pyodide.destroy) {
            pyodide.destroy();
        }
    });
</script>

<div class="python-editor">
    <div class="controls">
        <button
            onclick={runCode}
            disabled={!pyodide || isRunning}
        >
            {isRunning ? "Running..." : pyodide ? "▶ Run Code" : "Loading Python..."}
        </button>
        <button
            onclick={stopCode}
            disabled={!isRunning}
            class="stop-button"
        >
            ⏹ Stop
        </button>
    </div>

    <div class="code-editor">
        <CodeMirror bind:value={code} lang={python()} ref={codeEditorRef}/>
    </div>

    {#if output}
        <div class="console">
            <h3>Output:</h3>
            <pre>{output}</pre>
        </div>
    {/if}
</div>

<style>
    .python-editor {
        margin-bottom: 1rem;
    }

    .controls {
        margin-top: 0.5rem;
        margin-bottom: 0.5rem;
    }

    .controls button {
        margin-right: 0.5rem;
        padding: 0.5rem 1rem;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        font-weight: bold;
    }

    .controls button:not(.stop-button) {
        background-color: #00c04b;
        color: white;
    }

    .stop-button {
        background-color: #ff3e00;
        color: white;
    }

    .stop-button:disabled {
        background-color: #ccc;
        cursor: not-allowed;
    }

    .code-editor {
        height: 150px;
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
        max-height: 200px;
        overflow-y: auto;
    }
</style>