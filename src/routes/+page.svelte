<script lang="ts">
	import { onMount } from 'svelte';

	const sections = ['home', 'skills', 'experience'];
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
			isScrolling = false;
			
		});
	});
</script>

<main>
	<div class="home" id="home">
		<div class="header-top">
			<div class="social-links">
				<div id="linkedin" class="social-btn flex-center">
					<svg viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"
						><path
							d="M4.98 3.5c0 1.381-1.11 2.5-2.48 2.5s-2.48-1.119-2.48-2.5c0-1.38 1.11-2.5 2.48-2.5s2.48 1.12 2.48 2.5zm.02 4.5h-5v16h5v-16zm7.982 0h-4.968v16h4.969v-8.399c0-4.67 6.029-5.052 6.029 0v8.399h4.988v-10.131c0-7.88-8.922-7.593-11.018-3.714v-2.155z"
						></path></svg
					><span>in/stephenmbos</span>
				</div>

				<div id="github" class="social-btn flex-center">
					<svg viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"
						><path
							d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
						></path></svg
					><span>stephbos</span>
				</div>
			</div>
		</div>
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
		<h1>Skills & Technologies</h1>
		<div class="skills-row">
			<div class="skill">
				<div class="skill-content">
					<span class="skill-title">JavaScript</span>
					<p class="skill-desc">Versatile scripting language used for dynamic web development.</p>
				</div>
			</div>

			<div class="skill">
				<div class="skill-content">
					<span class="skill-title">TypeScript</span>
					<p class="skill-desc">Superset of JS adding static typing for safer, scalable apps.</p>
				</div>
			</div>

			<div class="skill">
				<div class="skill-content">
					<span class="skill-title">React</span>
					<p class="skill-desc">UI library for building dynamic, component-based web apps.</p>
				</div>
			</div>

			<div class="skill">
				<div class="skill-content">
					<span class="skill-title">Node.js</span>
					<p class="skill-desc">Runtime enabling fast, scalable server-side JavaScript.</p>
				</div>
			</div>
		</div>
		<div class="skills-row">
			<div class="skill">
				<div class="skill-content">
					<span class="skill-title">PostgreSQL</span>
					<p class="skill-desc">Versatile scripting language used for dynamic web development.</p>
				</div>
			</div>

			<div class="skill">
				<div class="skill-content">
					<span class="skill-title">MySQL</span>
					<p class="skill-desc">Superset of JS adding static typing for safer, scalable apps.</p>
				</div>
			</div>

			<div class="skill">
				<div class="skill-content">
					<span class="skill-title">Svelte</span>
					<p class="skill-desc">UI library for building dynamic, component-based web apps.</p>
				</div>
			</div>
		</div>
		<div class="skills-row">
			<div class="skill">
				<div class="skill-content">
					<span class="skill-title">BASH</span>
					<p class="skill-desc">Versatile scripting language used for dynamic web development.</p>
				</div>
			</div>

			<div class="skill">
				<div class="skill-content">
					<span class="skill-title">Git</span>
					<p class="skill-desc">Superset of JS adding static typing for safer, scalable apps.</p>
				</div>
			</div>

			<div class="skill">
				<div class="skill-content">
					<span class="skill-title">GraphQL</span>
					<p class="skill-desc">UI library for building dynamic, component-based web apps.</p>
				</div>
			</div>

			<div class="skill">
				<div class="skill-content">
					<span class="skill-title">Tailwind</span>
					<p class="skill-desc">Runtime enabling fast, scalable server-side JavaScript.</p>
				</div>
			</div>
		</div>
		<div class="skills-row">
			<div class="skill">
				<div class="skill-content">
					<span class="skill-title">NextJS</span>
					<p class="skill-desc">Versatile scripting language used for dynamic web development.</p>
				</div>
			</div>

			<div class="skill">
				<div class="skill-content">
					<span class="skill-title">HTML/CSS</span>
					<p class="skill-desc">Superset of JS adding static typing for safer, scalable apps.</p>
				</div>
			</div>

			<div class="skill">
				<div class="skill-content">
					<span class="skill-title">Python</span>
					<p class="skill-desc">UI library for building dynamic, component-based web apps.</p>
				</div>
			</div>
		</div>
		<div class="skills-row">
			<div class="skill">
				<div class="skill-content">
					<span class="skill-title">C++</span>
					<p class="skill-desc">Versatile scripting language used for dynamic web development.</p>
				</div>
			</div>

			<div class="skill">
				<div class="skill-content">
					<span class="skill-title">Java</span>
					<p class="skill-desc">Superset of JS adding static typing for safer, scalable apps.</p>
				</div>
			</div>

			<div class="skill">
				<div class="skill-content">
					<span class="skill-title">C#</span>
					<p class="skill-desc">UI library for building dynamic, component-based web apps.</p>
				</div>
			</div>

			<div class="skill">
				<div class="skill-content">
					<span class="skill-title">Confluence</span>
					<p class="skill-desc">Runtime enabling fast, scalable server-side JavaScript.</p>
				</div>
			</div>
		</div>
		<button class="learn-more-btn" on:click={() => scrollToSection(2)}>
			Continue Exploring
			<span class="arrow">↓</span>
		</button>
	</div>
	<div class="experience" id="experience">

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

	.header-top {
		position: absolute;
		top: 20px;
		left: 20px;
		z-index: 3;
	}

	.social-links,
	.flex-center {
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.social-btn {
		cursor: pointer;
		height: 50px;
		width: 50px;
		font-family: 'Titillium Web', sans-serif;
		color: #00adb5;
		border-radius: 10px;
		box-shadow: 0px 10px 10px rgba(0, 0, 0, 0.1);
		background: #393e46;
		margin: 5px;
		transition: 0.3s;
		justify-content: center;
	}

	.social-btn svg {
		height: 24px;
		width: 24px;
	}

	.social-btn span {
		width: 0px;
		overflow: hidden;
		transition: 0.3s;
		text-align: center;
		margin-left: 5px;
	}

	.social-btn:hover {
		width: 150px;
		border-radius: 5px;
	}

	.social-btn:hover span {
		padding: 2px;
		width: 120px;
	}

	#linkedin svg {
		fill: #0e76a8;
	}

	#github {
		fill: hsl(0, 0%, 0%);
	}

	.skills {
		background-color: #393e46;
		text-align: center;
		padding: 3rem 1.5rem 2rem;
		min-height: 100vh;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: flex-start;
		gap: 1.5rem;
	}

	.skills-row {
		display: flex;
		flex-direction: row;
		gap: 20rem;
		justify-content: center;
		margin-top: 2rem;
	}

	.skill {
		position: relative;
		width: 10em;
		height: 3.5em;
		border: 3px ridge #00adb5;
		background-color: transparent;
		color: white;
		border-radius: 0.3em;
		font-size: 1rem;
		font-weight: bold;
		cursor: pointer;
		overflow: hidden;
		display: flex;
		align-items: center; /* vertical centering */
		justify-content: center; /* horizontal centering */
		text-align: center;
		transition: all 0.4s ease;
	}

	.skill-content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center; /* centers both title and desc together */
		text-align: center;
		height: 100%;
		width: 100%;
		line-height: 1.2; /* keeps text tightly aligned */
	}

	/* Title appears centered until hover */
	.skill-title {
		font-size: 1.2rem;
		line-height: 1.2;
		transition:
			transform 0.4s ease,
			color 0.4s ease;
	}

	/* Hidden description starts collapsed */
	.skill-desc {
		display: none;
		opacity: 0;
		max-height: 0;
		overflow: hidden;
		font-size: 0.85rem;
		line-height: 1.1;
		color: #00adb5;
		margin-top: 0; /* eliminate unwanted spacing */
		transition:
			opacity 0.3s ease,
			max-height 0.4s ease,
			margin-top 0.3s ease;
	}

	/* Hover: grows smoothly and reveals text */
	.skill:hover {
		height: 8em;
		box-shadow: inset 0px 0px 25px #00adb5;
		background-color: rgba(0, 173, 181, 0.1);
	}

	.skill:hover .skill-title {
		transform: translateY(-0.5rem);
		color: #00adb5;
	}

	.skill:hover .skill-desc {
		display: block;
		opacity: 1;
		max-height: 4em;
		margin-top: 0.5rem;
	}

	.experience {
		background-color: #222831;
		text-align: center;
		padding: 3rem 1.5rem 2rem;
		min-height: 100vh;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: flex-start;
		gap: 1.5rem;
	}
</style>
