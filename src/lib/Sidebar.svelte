<script lang="ts">
	import { page } from '$app/state';

	function isActive(path: string) {
		return page.url.pathname === path;
	}
</script>

<aside class="sidebar">
	<div class="site-name">CodeSite</div>

	<nav aria-label="Main navigation">
		<a
			href="/"
			class:active={isActive('/')}
			aria-current={isActive('/') ? 'page' : undefined}
		>
			Home
		</a>

		<a
			href="/how-it-works"
			class:active={isActive('/how-it-works')}
			aria-current={isActive('/how-it-works') ? 'page' : undefined}
		>
			How this site works
		</a>

		<details open>
			<summary>Lessons</summary>

			<div class="submenu">
				<details open>
					<summary>Website</summary>

					<a href="/lessons/website" class:active={isActive('/lessons/website')}>
						Overview
					</a>

					<a href="/lessons/website/lesson_1" class:active={isActive('/lessons/website/lesson_1')}>
						Lesson 1
					</a>

					<a href="/lessons/website/lesson_2" class:active={isActive('/lessons/website/lesson_2')}>
						Lesson 2
					</a>

					<a href="/lessons/website/lesson_3" class:active={isActive('/lessons/website/lesson_3')}>
						Lesson 3
					</a>
				</details>

				<details open>
					<summary>Python</summary>

					<a href="/lessons/python" class:active={isActive('/lessons/python')}>
						Overview
					</a>

					<a href="/lessons/python/lesson_1" class:active={isActive('/lessons/python/lesson_1')}>
						Lesson 1
					</a>

					<a href="/lessons/python/lesson_2" class:active={isActive('/lessons/python/lesson_2')}>
						Lesson 2
					</a>

					<a href="/lessons/python/lesson_3" class:active={isActive('/lessons/python/lesson_3')}>
						Lesson 3
					</a>

					<a href="/lessons/python/lesson_4" class:active={isActive('/lessons/python/lesson_4')}>
						Lesson 4
					</a>

					<a href="/lessons/python/lesson_5" class:active={isActive('/lessons/python/lesson_5')}>
						Lesson 5
					</a>
				</details>
			</div>
		</details>

		<a
			class="bottom-link"
			href="/about"
			class:active={isActive('/about')}
			aria-current={isActive('/about') ? 'page' : undefined}
		>
			About / Contact
		</a>
	</nav>
</aside>

<style>
	.sidebar {
		position: sticky;
		top: 0;
		display: flex;
		flex-direction: column;
		height: 100vh;
		padding: 1.5rem 1rem;
		overflow-y: auto;
		color: white;
		background: #5f7470;
	}

	.site-name {
		margin-bottom: 2rem;
		padding: 0 0.75rem;
		font-size: 1.5rem;
		font-weight: 700;
	}

	nav {
		display: flex;
		flex: 1;
		flex-direction: column;
		gap: 0.4rem;
	}

	a,
	summary {
		display: block;
		padding: 0.75rem;
		color: white;
		text-decoration: none;
		border-radius: 0.35rem;
	}

	a:hover,
	summary:hover {
		background: #6f8581;
	}

	a.active {
		font-weight: 600;
		background: #889696;
		box-shadow: inset 4px 0 #e0e2db;
	}

	summary {
		cursor: pointer;
		list-style: none;
	}

	summary::-webkit-details-marker {
		display: none;
	}

	summary::before {
		display: inline-block;
		margin-right: 0.5rem;
		content: "▸";
		transition: transform 0.15s;
	}

	details[open] > summary::before {
		transform: rotate(90deg);
	}

	.submenu {
		margin-left: 1rem;
		padding-left: 0.5rem;
		border-left: 1px solid #889696;
	}

	.submenu a {
		margin-left: 1rem;
		font-size: 0.95rem;
	}

	.bottom-link {
		margin-top: auto;
	}

	@media (max-width: 700px) {
		.sidebar {
			position: static;
			height: auto;
			min-height: auto;
		}

		.bottom-link {
			margin-top: 1rem;
		}
	}
</style>
