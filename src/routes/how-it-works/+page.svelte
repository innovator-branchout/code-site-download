<svelte:head>
	<title>How It Works|CodeSite</title>
</svelte:head>
<main>
    <h1>How it works</h1>
    <p> Navigating a website for the first time can be hard. Here is how you do it </p>
    <br>

    <h2>The Navigation Bars</h2>
    <section class="bar-guide">
        <div class="rightbox">
            <p>The website consists of multiple tabs each representing a different page. Think of it like the pages of a book(or smt else idk). <br>
                    <br>
                    In order to flip through these tabs, you need to use the teal navigation bar to your left. Click on the tab title to switch to that tab.<br>
                    <br>
                    Try switching to the home screen then back like in the demonstration to the right
            </p>
            <image src="src/routes/how-it-works/dummygif.png" class="switch-tab-demo" alt="demonstration gif"> </image>
        </div>

        <h3>Dropdowns</h3>

        <p>Notice that the “Lessons” title is different……………… Once you open the lessons dropdown, there is 2 options, website and python. </p>
    </section>
    <br>
    <h2>Organization</h2>
    <p>This website has 4 pages. You are currently in the “How to use the website” tab so we won’t cover that here. Here is what the rest of the tabs they do</p>
    <div class="double-section">
        <section class="half">
            <p>
                <strong>Home</strong><br><br>
                All good websites begin with the homepage....
            </p>
        </section>
        <section class="half">
            <p>
                <strong>About/Contact</strong> <br> <br>
                View this tab to learn more about our organization - Branchout! ……………
            </p>
        </section>
    </div>
    <section>
        <h3>Lessons</h3>
        <p>
            This is the tab you’ll be using the most. It contains all lessons, including over __ lessons for HTML and Python<br><br>
        </p>
        <div class="rightbox">
            <p>
                To view lessons, open the dropdown and click
                on any of the topics to expand it. Then click on a lesson in order to open that lesson. There, you
                can learn more about programming! <br><br>
                Follow the video to the right to open your first lesson!
            </p>
            <image src="src/routes/how-it-works/dummygif.png" class="open-lesson-demo" alt="demonstration gif"></image>
        </div>
    </section>
</main>

<style>
    main {
		max-width: 900px;
		min-height: calc(100vh - 70px);
		margin: 10 auto;
		padding: 1rem 2rem;
	}
    section {
        margin-top: 2rem;
        padding: 2rem;
        background-color: #b8bdb5;
        border-radius: 50px;
        padding-right: 7rem;
    }
    .rightbox {
        display: flex;
        width: 100%
    }
    .switch-tab-demo {
        padding-left:2rem;
        width: 700px;
        height: auto;
        object-fit: contain;
        justify-content: flex-end;
    }
    .open-lesson-demo {
        padding-left:2rem;
        width: 700px;
        height: auto;
        object-fit: contain;
        justify-content: flex-end;
    }
    p {
        max-width: 650px;
    }
    .half {
        width: 49%;
        padding-right: 3rem;
    }
    .double-section{
        display: flex;
        gap: 2%;
    }
</style>
