<script lang="ts">
	import { onMount } from 'svelte';

	const sections = ['home', 'skills']; 
	let isScrolling = false;

	function scrollToSection(index: number) {
		if (index < 0 || index >= sections.length) return;
		const sectionEl = document.getElementById(sections[index]);
		if (sectionEl) {
			sectionEl.scrollIntoView({ behavior: 'smooth' });
		}
	}

	onMount(() => {
		window.addEventListener('wheel', (event: WheelEvent) => {
			if (isScrolling) return; 

			const delta = event.deltaY;
			const currentSectionId = sections.find((id) => {
				const el = document.getElementById(id);
				if (!el) return false;
				const rect = el.getBoundingClientRect();
				
				return rect.top <= window.innerHeight / 2 && rect.bottom >= window.innerHeight / 2;
			});

			if (!currentSectionId) return;

			const currentIndex = sections.indexOf(currentSectionId);

			if (delta > 0) {
				// scroll down
				scrollToSection(currentIndex + 1);
			} else if (delta < 0) {
				// scroll up
				scrollToSection(currentIndex - 1);
			}

			isScrolling = true;
			setTimeout(() => {
				isScrolling = false;
			}, 1000);
		});
	});
</script>

<main>
	<div class="home" id="home">
		<div class="words-and-pic">
			<img src="/headshot.JPEG" alt="Headshot" class="headshot" />
			<div class="introduction">
				<div class="intro-text">
					<h1 class="intro-title">Hi I'm Stephen Bos</h1>
					<h2>
						I am a Skilled Software Engineer who leads the design, development, and implementation
						of innovative software features and enhancements.
					</h2>
				</div>
			</div>
		</div>
		<div class="band">
			<div class="band-text">
				<span>
					Typescript Node React PostgreSQL Javascript GraphQL NextJS Git Jira HTML CSS Tailwind BASH
					Python
				</span>
				<span>
					Typescript Node React PostgreSQL Javascript GraphQL NextJS Git Jira HTML CSS Tailwind BASH
					Python
				</span>
			</div>
		</div>
		<button class="learn-more-btn" on:click={() => scrollToSection(1)}>
			Learn more about me
			<span class="arrow">↓</span>
		</button>
	</div>
	<div class="skills" id="skills">
		<!-- Skills content goes here -->
	</div>
</main>

<style>
	main {
		position: relative;
		display: flex;
		flex-direction: column;
		width: 100%;
		color: #eeeeee;
		text-align: left;
		overflow: hidden;
	}

	.home,
	.skills {
		min-height: 100vh;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		position: relative;
	}

	.band {
		width: 100%;
		height: 80px;
		background-color: #393e46;
		display: flex;
		align-items: center;
		overflow: hidden;
		margin: 2rem 0;
	}

	.band-text {
		display: flex;
		width: max-content;
		animation: slide 30s linear infinite;
	}

	.band-text span {
		white-space: nowrap;
		padding-right: 2rem;
		font-family: 'Lucida Console', Monaco, monospace;
		font-size: 4rem;
		color: #222831;
	}

	@keyframes slide {
		0% {
			transform: translateX(0);
		}
		100% {
			transform: translateX(-50%);
		}
	}

	.words-and-pic {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: center;
		gap: 2rem;
		z-index: 1;
		font-family: 'arial', sans-serif;
		font-size: 1rem;
	}

	.introduction {
		max-width: 20%;
		display: flex;
		flex-direction: row;
		align-items: center;
		padding: 2rem;
		border-radius: 10px;
	}

	.headshot {
		width: 15%;
		height: auto;
		padding-right: 1rem;
		border-radius: 35%;
		object-fit: cover;
	}

	.intro-text {
		display: flex;
		flex-direction: column;
		padding-left: 1rem;
	}

	.intro-title {
		color: #00adb5;
		font-size: 2.5rem;
	}

	.learn-more-btn {
		margin-top: 5rem;
		background: none;
		border: 2px solid #00adb5;
		color: #00adb5;
		font-size: 1.2rem;
		font-weight: 600;
		padding: 0.75rem 1.5rem;
		border-radius: 50px;
		cursor: pointer;
		display: flex;
		align-items: center;
		gap: 0.5rem;
		transition: all 0.3s ease;
		z-index: 2;
	}

	.learn-more-btn:hover {
		background-color: #00adb5;
		color: #222831;
		transform: translateY(-3px);
	}

	.arrow {
		display: inline-block;
		animation: bounce 1.5s infinite;
	}

	@keyframes bounce {
		0%,
		20%,
		50%,
		80%,
		100% {
			transform: translateY(0);
		}
		40% {
			transform: translateY(6px);
		}
		60% {
			transform: translateY(3px);
		}
	}

	.skills {
		background-color: #393e46;
		color: #eeeeee;
		text-align: center;
		padding: 4rem;
	}
</style>
