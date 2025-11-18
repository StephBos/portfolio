<script lang="ts">
	import { onMount } from 'svelte';
	import { skills, experience, education, projects } from '../lib/constants.js';

	const sections = ['home', 'skills', 'experience', 'projects'];
	let isScrolling = false;
	let activeTab = 'experience';
	let selectedExperience: (typeof experience)[0] | null = null;
	let showModal = false;

	function scrollToSection(index: number) {
		if (index < 0 || index >= sections.length) return;
		const sectionEl = document.getElementById(sections[index]);
		if (sectionEl) {
			sectionEl.scrollIntoView({ behavior: 'smooth' });
		}
	}

	let width = 0;

	onMount(() => {
		width = window.innerWidth;

		const handleResize = () => {
			width = window.innerWidth;
		};

		window.addEventListener('resize', handleResize);

		window.addEventListener('wheel', (event: WheelEvent) => {
			console.log('Window width:', window.innerWidth);
			if (window.innerWidth <= 720) return;

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

			return () => {
				window.removeEventListener('resize', handleResize);
			};
		});
	});
</script>

<main>
	<div class="home" id="home">
		<div class="header-top">
			<div class="social-links">
				<a
					href="https://www.linkedin.com/in/stephenmbos/"
					target="_blank"
					rel="noopener noreferrer"
				>
					<div id="linkedin" class="social-btn flex-center">
						<svg viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"
							><path
								d="M4.98 3.5c0 1.381-1.11 2.5-2.48 2.5s-2.48-1.119-2.48-2.5c0-1.38 1.11-2.5 2.48-2.5s2.48 1.12 2.48 2.5zm.02 4.5h-5v16h5v-16zm7.982 0h-4.968v16h4.969v-8.399c0-4.67 6.029-5.052 6.029 0v8.399h4.988v-10.131c0-7.88-8.922-7.593-11.018-3.714v-2.155z"
							></path></svg
						><span>in/stephenmbos</span>
					</div>
				</a>

				<a href="https://github.com/StephBos" target="_blank" rel="noopener noreferrer">
					<div id="github" class="social-btn flex-center">
						<svg viewBox="0 0 24 24" height="24" width="24" xmlns="http://www.w3.org/2000/svg"
							><path
								d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
							></path></svg
						><span>stephbos</span>
					</div>
				</a>
			</div>
			<a
				class="contact-me"
				href="mailto:stephen.bos1029@gmail.com?subject=Contact%20Request&body=Please%20enter%20your%20first%20name,%20last%20name,%20and%20email."
				target="_blank"
				rel="noopener noreferrer">Contact Me</a
			>
		</div>
		<div class="words-and-pic">
			<img src="/headshot.JPEG" alt="Headshot" class="headshot" />
			<div class="introduction">
				<div class="intro-text">
					<h1 class="intro-title">Hi! I'm Stephen Bos</h1>
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
		<div class="skills-grid">
			{#each skills as skill}
				<div class="skill">
					<div class="skill-content">
						<span class="skill-title">{skill.skill}</span>
						<p class="skill-desc">{skill.description}</p>
					</div>
				</div>
			{/each}
		</div>
		<button class="learn-more-btn" on:click={() => scrollToSection(2)}>
			Experience
			<span class="arrow">↓</span>
		</button>
	</div>
	<div class="experience" id="experience">
		<h1>My Journey</h1>
		<div class="tabs-container">
			<div class="tab-buttons">
				<button
					class="tab-btn"
					class:active={activeTab === 'experience'}
					on:click={() => (activeTab = 'experience')}
				>
					Experience
				</button>
				<button
					class="tab-btn"
					class:active={activeTab === 'education'}
					on:click={() => (activeTab = 'education')}
				>
					Education
				</button>
			</div>
			<div class="tab-content">
				{#if activeTab === 'experience'}
					<div class="card-wrapper">
						{#each experience as exp}
							<div class="card">
								<div class="card-details">
									<p class="text-title">{exp.title}</p>
									<p class="text-body">{exp.company}</p>
									<p class="date">{exp.time}</p>
									<p class="text-body">{exp.location}</p>
								</div>
								<button
									class="card-button"
									on:click={() => {
										selectedExperience = exp;
										showModal = true;
									}}
								>
									More info
								</button>
							</div>
						{/each}
					</div>

					{#if showModal && selectedExperience}
						<div class="modal-overlay" on:click={() => (showModal = false)}>
							<div class="modal-content" on:click|stopPropagation>
								<button class="modal-close" on:click={() => (showModal = false)}>
									<svg
										width="20"
										height="20"
										viewBox="0 0 20 20"
										fill="none"
										xmlns="http://www.w3.org/2000/svg"
									>
										<path
											d="M15 5L5 15M5 5L15 15"
											stroke="currentColor"
											stroke-width="2"
											stroke-linecap="round"
											stroke-linejoin="round"
										/>
									</svg>
								</button>
								<h2>{selectedExperience.title}</h2>
								<div class="modal-subtitle">
									<span class="company">
										<svg
											width="16"
											height="16"
											viewBox="0 0 24 24"
											fill="none"
											xmlns="http://www.w3.org/2000/svg"
										>
											<path
												d="M3 21H21M3 18H21M6 18V10M10 18V10M14 18V10M18 18V10M21 10H3L5 4H19L21 10Z"
												stroke="currentColor"
												stroke-width="2"
												stroke-linecap="round"
												stroke-linejoin="round"
											/>
										</svg>
										{selectedExperience.company}
									</span>
									<span class="separator">•</span>
									<span class="location">
										<svg
											width="16"
											height="16"
											viewBox="0 0 24 24"
											fill="none"
											xmlns="http://www.w3.org/2000/svg"
										>
											<path
												d="M12 13C13.6569 13 15 11.6569 15 10C15 8.34315 13.6569 7 12 7C10.3431 7 9 8.34315 9 10C9 11.6569 10.3431 13 12 13Z"
												stroke="currentColor"
												stroke-width="2"
												stroke-linecap="round"
												stroke-linejoin="round"
											/>
											<path
												d="M12 22C16 18 20 14.4183 20 10C20 5.58172 16.4183 2 12 2C7.58172 2 4 5.58172 4 10C4 14.4183 8 18 12 22Z"
												stroke="currentColor"
												stroke-width="2"
												stroke-linecap="round"
												stroke-linejoin="round"
											/>
										</svg>
										{selectedExperience.location}
									</span>
									<span class="separator">•</span>
									<span class="time">
										<svg
											width="16"
											height="16"
											viewBox="0 0 24 24"
											fill="none"
											xmlns="http://www.w3.org/2000/svg"
										>
											<path
												d="M12 8V12L15 15M21 12C21 16.9706 16.9706 21 12 21C7.02944 21 3 16.9706 3 12C3 7.02944 7.02944 3 12 3C16.9706 3 21 7.02944 21 12Z"
												stroke="currentColor"
												stroke-width="2"
												stroke-linecap="round"
												stroke-linejoin="round"
											/>
										</svg>
										{selectedExperience.time}
									</span>
								</div>
								<div class="modal-description">
									{#each selectedExperience.descriptions as desc}
										<p>{desc}</p>
									{/each}
								</div>
							</div>
						</div>
					{/if}
				{:else}
					<div class="card-wrapper">
						{#each education as edu}
							<div class="card">
								<div class="card-details">
									<p class="text-title">{edu.section}</p>
									{#each edu.major as m, i}
										<div class="entry">
											<p class="text-body">{m}</p>
											<p class="text-body">{edu.school ? edu.school[i] : edu.schools[i]}</p>
											<p class="text-date">{edu.graduated[i]}</p>
										</div>
									{/each}
								</div>
							</div>
						{/each}
					</div>
				{/if}
			</div>
		</div>
		<button class="learn-more-btn" on:click={() => scrollToSection(3)}>
			Projects
			<span class="arrow">↓</span>
		</button>
	</div>
	<div class="projects" id="projects">
		<h1>My Projects</h1>
		<div class="projects-container">
			{#each projects as project}
				<div class="project-card">
					<h2>{project.name}</h2>
					<p class="project-description">{project.description}</p>
					<div class="tech-stack">
						{#each project.technologies as tech}
							<span class="tech-tag">{tech}</span>
						{/each}
					</div>
					{#if project.link.length > 0}
						<div class="project-links">
							{#each project.link as url}
								<a href={url} target="_blank" rel="noopener noreferrer" class="project-link">
									<svg viewBox="0 0 24 24" width="16" height="16">
										<path
											fill="currentColor"
											d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12"
										/>
									</svg>
									View Code
								</a>
							{/each}
						</div>
					{/if}
				</div>
			{/each}
		</div>
		<button class="learn-more-btn" on:click={() => scrollToSection(0)}>
			Back to top
			<span class="arrow">↑</span>
		</button>
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

	.skills-grid {
		display: grid;
		grid-template-columns: repeat(4, 1fr); /* 4 columns */
		row-gap: 1rem;
		column-gap: 5rem;
	}

	.skill {
		background: var(--skill-bg, #222);
		padding: 1rem;
		border-radius: 8px;
	}

	.skill-title {
		font-weight: bold;
		display: block;
		margin-bottom: 0.3rem;
	}

	.skill-desc {
		font-size: 0.9rem;
		opacity: 0.8;
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
		margin-bottom: 2rem; /* give breathing room from the next section */
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
		position: fixed;
		top: 20px;
		left: 20px;
		right: 20px;
		display: flex;
		justify-content: space-between;
		align-items: center;
		z-index: 1000;
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

	.contact-me {
		width: 10em;
		height: 3.5em;
		border: 3px ridge #00adb5;
		outline: none;
		background-color: transparent;
		color: white;
		transition: 1s;
		border-radius: 0.3em;
		font-size: 16px;
		font-weight: bold;
		cursor: pointer;
		margin-right: 20px;
		display: inline-block;
		text-align: center;
		line-height: 3.5em;
		text-decoration: none;
		position: relative;
	}

	.contact-me::after {
		content: '';
		position: absolute;
		top: -10px;
		left: 3%;
		width: 95%;
		height: 40%;
		background-color: transparent;
		transition: 0.5s;
		transform-origin: center;
	}

	.contact-me::before {
		content: '';
		transform-origin: center;
		position: absolute;
		top: 80%;
		left: 3%;
		width: 95%;
		height: 40%;
		background-color: transparent;
		transition: 0.5s;
	}

	.contact-me:hover::before,
	.contact-me:hover::after {
		transform: scale(0);
	}

	.contact-me:hover {
		box-shadow: inset 0px 0px 25px #1479ea;
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

	.tabs-container {
		width: 80%;
		max-width: 1200px;
		margin: 0 auto;
		background: #393e46;
		border-radius: 20px;
		padding: 2rem;
		border: 2px solid #eeeeee;
	}

	.tab-buttons {
		display: flex;
		gap: 1rem;
		justify-content: center;
		margin-bottom: 2rem;
		border-bottom: 2px solid #eeeeee;
		padding-bottom: 1rem;
	}

	.tab-btn {
		background: none;
		border: none;
		color: #eeeeee;
		font-size: 1.2rem;
		font-weight: 600;
		padding: 0.5rem 2rem;
		cursor: pointer;
		transition: all 0.3s ease;
		position: relative;
	}

	.tab-btn::after {
		content: '';
		position: absolute;
		/* place the indicator centered under the button label */
		bottom: -0.6rem;
		left: 50%;
		transform: translateX(-50%) scaleX(0);
		width: 60%;
		height: 3px;
		background-color: #00adb5;
		transition: transform 0.3s ease;
		border-radius: 2px;
	}

	.tab-btn.active {
		color: #00adb5;
	}

	.tab-btn.active::after {
		transform: translateX(-50%) scaleX(1);
	}

	.tab-content {
		min-height: 400px;
	}

	.card-wrapper {
		display: flex;
		gap: 2rem;
		justify-content: center;
		flex-wrap: wrap;
	}

	.card {
		width: 260px;
		height: 240px;
		border-radius: 16px;
		background: linear-gradient(180deg, #2b2f33 0%, #222831 100%);
		position: relative;
		padding: 1.2rem 1.2rem 2.4rem;
		border: 1px solid rgba(238, 238, 238, 0.08);
		box-shadow: 0 6px 18px rgba(8, 12, 16, 0.6);
		transition:
			transform 260ms cubic-bezier(0.2, 0.9, 0.3, 1),
			box-shadow 260ms ease,
			border-color 260ms ease;
		overflow: hidden;
		display: flex;
		flex-direction: column;
	}

	/* subtle colored accent on the top edge */
	.card::before {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		height: 4px;
		width: 100%;
		border-top-left-radius: 16px;
		border-top-right-radius: 16px;
		background: linear-gradient(90deg, #00adb5 0%, #7be5d8 100%);
		opacity: 0.95;
	}

	.card-details {
		color: #eeeeee;
		height: 100%;
		display: flex;
		flex-direction: column;
		gap: 0.4rem;
		padding-top: 0.4rem;
		overflow-y: auto;
		scrollbar-width: thin;
		scrollbar-color: #00adb5 #222831;
	}

	/* Webkit scrollbar styling */
	.card-details::-webkit-scrollbar {
		width: 8px;
		height: 8px;
	}

	.card-details::-webkit-scrollbar-track {
		background: #222831;
		border-radius: 4px;
		margin: 4px 0;
	}

	.card-details::-webkit-scrollbar-thumb {
		background: #00adb5;
		border-radius: 4px;
		border: 2px solid #222831;
		transition: all 0.2s ease;
	}

	.card-details::-webkit-scrollbar-thumb:hover {
		background: #00c5cf;
		border-width: 1px;
	}

	.card-details::-webkit-scrollbar-thumb:active {
		background: #00d8e3;
		border-width: 1px;
	}

	.card-list {
		text-align: left;
		margin: 0.6rem 0 0;
		padding-left: 1.25rem;
		color: #e9ecef;
	}

	.card-list li {
		margin-bottom: 0.45rem;
		line-height: 1.35;
	}

	.card-button {
		/* kept centered but pulled inside the card */
		transform: translate(-50%, 0%);
		width: 56%;
		border-radius: 999px;
		border: none;
		background-color: #00adb5;
		color: #0b0f10;
		font-size: 0.95rem;
		padding: 0.55rem 1rem;
		position: absolute;
		left: 50%;
		bottom: 14px;
		opacity: 0;
		transition:
			opacity 220ms ease,
			transform 220ms cubic-bezier(0.2, 0.9, 0.3, 1),
			box-shadow 220ms ease;
		cursor: pointer;
		box-shadow: 0 6px 18px rgba(0, 173, 181, 0.12);
	}

	.text-body {
		color: #7fd5cf;
		font-size: 0.95rem;
		font-weight: 600;
	}

	.date {
		color: #dfe7e9;
		font-size: 0.85rem;
		opacity: 0.9;
	}

	.text-title {
		font-size: 1.1rem;
		font-weight: 700;
		letter-spacing: 0.2px;
		margin-bottom: 0.2rem;
	}

	.card:hover {
		transform: translateY(-4px);
		border-color: rgba(0, 173, 181, 0.5);
		box-shadow: 0 12px 24px rgba(7, 12, 14, 0.6);
	}

	.card:hover .card-button {
		transform: translate(-50%, 0%);
		opacity: 1;
		box-shadow: 0 8px 16px rgba(0, 173, 181, 0.14);
	}

	/* responsive: slightly narrower cards on small screens */
	@media (max-width: 720px) {
		.card {
			width: calc(100% - 2rem);
			min-height: 220px;
		}
		.card-button {
			width: 70%;
		}

		/* Always show the More info / card-button on touch/smaller screens */
		.card-button {
			opacity: 1 !important;
			transform: translate(-50%, 0%) !important;
			box-shadow: 0 8px 16px rgba(0, 173, 181, 0.14) !important;
		}
	}

	.projects {
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

	.projects-container {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
		gap: 2rem;
		width: 100%;
		max-width: 1200px;
		padding: 2rem;
	}

	.project-card {
		background: linear-gradient(180deg, #2b2f33 0%, #222831 100%);
		border-radius: 16px;
		padding: 1.5rem;
		display: flex;
		flex-direction: column;
		gap: 1rem;
		border: 1px solid rgba(238, 238, 238, 0.08);
		box-shadow: 0 6px 18px rgba(8, 12, 16, 0.6);
		transition: all 0.3s ease;
		position: relative;
		overflow: hidden;
	}

	.project-card::before {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		height: 4px;
		width: 100%;
		background: linear-gradient(90deg, #00adb5 0%, #7be5d8 100%);
		opacity: 0.95;
	}

	.project-card:hover {
		transform: translateY(-4px);
		border-color: rgba(0, 173, 181, 0.5);
		box-shadow: 0 12px 24px rgba(7, 12, 14, 0.6);
	}

	.project-card h2 {
		font-size: 1.5rem;
		color: #00adb5;
		margin: 0;
	}

	.project-description {
		color: #eeeeee;
		font-size: 1rem;
		line-height: 1.6;
		flex-grow: 1;
	}

	.tech-stack {
		display: flex;
		flex-wrap: wrap;
		gap: 0.5rem;
		margin-top: auto;
	}

	.tech-tag {
		background: rgba(0, 173, 181, 0.15);
		color: #00adb5;
		padding: 0.25rem 0.75rem;
		border-radius: 999px;
		font-size: 0.8rem;
		font-weight: 600;
		border: 1px solid rgba(0, 173, 181, 0.3);
	}

	.project-links {
		display: flex;
		gap: 1rem;
		margin-top: 1rem;
		justify-content: flex-start;
	}

	.project-link {
		display: flex;
		align-items: center;
		gap: 0.5rem;
		color: #00adb5;
		text-decoration: none;
		font-size: 0.9rem;
		font-weight: 600;
		padding: 0.5rem 1rem;
		border-radius: 8px;
		background: rgba(0, 173, 181, 0.1);
		border: 1px solid rgba(0, 173, 181, 0.3);
		transition: all 0.2s ease;
	}

	.project-link:hover {
		background: rgba(0, 173, 181, 0.2);
		transform: translateY(-2px);
	}

	.project-link svg {
		transition: transform 0.2s ease;
	}

	.project-link:hover svg {
		transform: translate(2px, -2px);
	}

	@keyframes modalFadeIn {
		from {
			opacity: 0;
			transform: scale(0.95);
		}
		to {
			opacity: 1;
			transform: scale(1);
		}
	}

	.modal-overlay {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background-color: rgba(0, 0, 0, 0.85);
		display: flex;
		justify-content: center;
		align-items: center;
		z-index: 1000;
		padding: 1.5rem;
		backdrop-filter: blur(8px);
		animation: modalFadeIn 0.3s ease-out forwards;
	}

	.modal-content {
		background: linear-gradient(165deg, #2b2f33 0%, #222831 100%);
		padding: 2.5rem;
		border-radius: 24px;
		width: 100%;
		max-width: 680px;
		max-height: 85vh;
		overflow-y: auto;
		position: relative;
		border: 1px solid rgba(238, 238, 238, 0.12);
		box-shadow:
			0 24px 48px -12px rgba(0, 0, 0, 0.9),
			0 0 80px rgba(0, 173, 181, 0.15);
	}

	.modal-content::before {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		height: 3px;
		background: linear-gradient(90deg, #00adb5, #7be5d8);
		border-top-left-radius: 24px;
		border-top-right-radius: 24px;
		opacity: 0.8;
	}

	.modal-content h2 {
		background: linear-gradient(90deg, #00adb5, #7be5d8);
		-webkit-background-clip: text;
		background-clip: text;
		color: transparent;
		font-size: 1.8rem;
		margin-bottom: 0.75rem;
		padding-right: 2rem;
		font-weight: 700;
		letter-spacing: -0.02em;
	}

	.modal-subtitle {
		color: #7fd5cf;
		font-size: 1.05rem;
		margin-bottom: 2rem;
		display: flex;
		flex-wrap: wrap;
		gap: 0.75rem;
		align-items: center;
		opacity: 0.9;
	}

	.modal-subtitle .separator {
		color: #4a4f57;
		font-weight: 700;
	}

	.modal-description {
		position: relative;
		padding: 1.5rem;
		background: rgba(0, 0, 0, 0.2);
		border-radius: 16px;
		border: 1px solid rgba(238, 238, 238, 0.08);
	}

	.modal-description p {
		color: #eeeeee;
		line-height: 1.7;
		margin-bottom: 1.2rem;
		font-size: 1rem;
		text-align: left;
		letter-spacing: 0.01em;
	}

	.modal-description p:last-child {
		margin-bottom: 0;
	}

	.modal-close {
		position: absolute;
		top: 1.25rem;
		right: 1.25rem;
		background: rgba(0, 173, 181, 0.1);
		border: 1px solid rgba(0, 173, 181, 0.2);
		color: #7fd5cf;
		font-size: 1.5rem;
		cursor: pointer;
		width: 36px;
		height: 36px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 12px;
		transition: all 0.2s ease;
	}

	.modal-close:hover {
		background-color: rgba(0, 173, 181, 0.2);
		border-color: rgba(0, 173, 181, 0.3);
		color: #00adb5;
		transform: scale(1.05);
	}

	/* Webkit scrollbar styling for modal */
	.modal-content::-webkit-scrollbar {
		width: 8px;
	}

	.modal-content::-webkit-scrollbar-track {
		background: rgba(34, 40, 49, 0.6);
		border-radius: 4px;
	}

	.modal-content::-webkit-scrollbar-thumb {
		background: rgba(0, 173, 181, 0.5);
		border-radius: 4px;
		border: 2px solid rgba(34, 40, 49, 0.6);
	}

	.modal-content::-webkit-scrollbar-thumb:hover {
		background: rgba(0, 173, 181, 0.7);
	}

	/* Firefox scrollbar styling for modal */
	.modal-content {
		scrollbar-width: thin;
		scrollbar-color: rgba(0, 173, 181, 0.5) rgba(34, 40, 49, 0.6);
	}

	@media (max-width: 640px) {
		.modal-content {
			padding: 2rem 1.5rem;
		}

		.modal-content h2 {
			font-size: 1.5rem;
		}

		.modal-subtitle {
			font-size: 0.95rem;
		}

		.modal-description {
			padding: 1.25rem;
		}
	}

	.contact-modal {
		max-width: 400px;
		padding: 2rem 1.5rem;
		border-radius: 18px;
		background: linear-gradient(165deg, #2b2f33 0%, #222831 100%);
		box-shadow:
			0 24px 48px -12px rgba(0, 0, 0, 0.9),
			0 0 80px rgba(0, 173, 181, 0.15);
		border: 1px solid rgba(238, 238, 238, 0.12);
		position: relative;
	}
	.contact-modal h2 {
		color: #00adb5;
		font-size: 1.4rem;
		margin-bottom: 1.2rem;
		text-align: center;
	}
	.contact-form {
		display: flex;
		flex-direction: column;
		gap: 1.2rem;
	}
	.form-group {
		display: flex;
		flex-direction: column;
		gap: 0.3rem;
	}
	.form-group label {
		color: #eeeeee;
		font-size: 1rem;
		font-weight: 600;
	}
	.form-group input {
		padding: 0.5rem 0.8rem;
		border-radius: 8px;
		border: 1px solid #00adb5;
		background: #222831;
		color: #eeeeee;
		font-size: 1rem;
		outline: none;
		transition: border-color 0.2s;
	}
	.form-group input:focus {
		border-color: #7be5d8;
	}
	.form-error {
		color: #ff4c4c;
		font-size: 0.95rem;
		text-align: center;
		margin-bottom: 0.5rem;
	}
	.contact-submit {
		background: linear-gradient(90deg, #00adb5 0%, #7be5d8 100%);
		color: #222831;
		font-weight: 700;
		padding: 0.7rem 1.5rem;
		border-radius: 12px;
		border: none;
		cursor: pointer;
		font-size: 1.1rem;
		box-shadow: 0 4px 12px rgba(0, 173, 181, 0.2);
		transition: all 0.2s;
		margin-top: 0.5rem;
	}
	.contact-submit:hover {
		background: linear-gradient(90deg, #7be5d8 0%, #00adb5 100%);
		color: #222831;
		transform: translateY(-2px);
	}

	/* Small-screen placement adjustments for Skills (stacking only) */
	@media (max-width: 720px) {
		.skills-grid {
			grid-template-columns: 1fr; /* single column */
			width: 90%;
			max-width: 360px;
		}

		.skills-row {
			flex-direction: column;
			align-items: center;
			gap: 0.75rem;
		}
		/* keep visual appearance, only adjust placement/width */
		.skill {
			width: 90%;
			max-width: 360px;
			height: auto;
		}

		.words-and-pic {
			flex-direction: column !important;
			align-items: center !important;
			justify-content: center !important;
			width: 100% !important;
			text-align: center !important;
		}

		.headshot {
			display: block !important;
			width: clamp(180px, 30vw, 320px) !important;
			height: auto !important;
			margin: 0.25rem auto 0.5rem auto !important;
			border-radius: 50% !important;
		}

		.introduction,
		.intro-text {
			width: 100% !important;
			max-width: 100% !important;
			padding-left: 0 !important;
			padding-right: 0 !important;
			text-align: center !important;
		}

		/* slightly reduce contact button so it doesn't overlap when narrowing the desktop window */
		.contact-me {
			min-width: 6rem;
			font-size: 0.95rem;
		}
	}
	/* Small-screen improvements (phones) */
	@media (max-width: 480px) {
		/* Header and social */
		.header-top {
			top: 12px;
			left: 12px;
			right: 12px;
			padding: 0 8px;
			gap: 8px;
			align-items: center;
		}

		.social-links {
			gap: 8px;
		}

		.social-btn {
			height: 40px;
			width: 40px;
			margin: 4px;
			border-radius: 8px;
		}

		.social-btn span {
			display: none; /* hide text labels to save space */
		}

		/* Contact button */
		.contact-me {
			width: 8rem;
			height: 2.8rem;
			line-height: 2.8rem;
			font-size: 0.95rem;
			margin-right: 0;
			padding: 0 0.6rem;
		}

		/* Intro section stacks on phones */
		.words-and-pic {
			flex-direction: column !important;
			gap: 0.5rem;
			padding: 0;
			align-items: center !important;
			justify-content: center !important;
			text-align: center !important;
		}

		/* ensure the fixed header doesn't overlap the home content */
		.home {
			/* increase spacing so the fixed header and its button don't overlap the hero */
			padding-top: 80px;
			align-items: center;
		}

		.headshot {
			/* make the headshot larger and responsive on phones and force it above the text */
			display: block !important;
			width: clamp(200px, 44vw, 320px) !important;
			height: auto;
			border-radius: 50%;
			margin-top: 0 !important; /* remove extra top margin */
			flex-shrink: 0;
			margin: 0.25rem auto 0.5rem auto !important;
			order: 0;
		}

		.introduction {
			/* switch to block layout so text stacks under the picture cleanly */
			display: block !important;
			width: 100% !important;
			max-width: 100% !important;
			padding: 0.75rem 1rem 1rem 1rem !important;
			order: 1 !important;
			text-align: center !important;
		}

		/* ensure the hero area fills the available width and stacks cleanly */
		.words-and-pic {
			width: 100%;
			align-items: center;
			flex-direction: column !important;
		}

		/* shrink the contact button on phones so it doesn't overlap content */
		.contact-me {
			min-width: 5.2rem;
			width: auto;
			height: 2.6rem;
			font-size: 0.88rem;
			padding: 0 0.5rem;
			margin-left: 0.5rem;
			display: none !important; /* hide on very small screens to avoid overlapping the heading */
		}

		/* reduce extra left padding introduced by desktop rules */
		.intro-text {
			padding-left: 0 !important;
			padding-right: 0 !important;
			width: 100% !important;
			box-sizing: border-box !important;
		}

		.intro-title {
			font-size: 1.8rem;
			line-height: 1.05;
		}

		.band {
			height: 56px;
			margin: 1rem 0;
		}

		.band-text span {
			font-size: 1.6rem;
		}

		.learn-more-btn {
			margin-top: 2rem;
			margin-bottom: 1.5rem;
			padding: 0.6rem 1rem;
			font-size: 1rem;
		}

		/* Tabs and cards */
		.tabs-container {
			padding: 1.5rem !important;
			width: 95% !important;
			box-sizing: border-box !important;
		}

		.card-wrapper {
			flex-direction: column;
			align-items: center;
			gap: 1rem;
		}

		.card,
		.project-card {
			width: 100% !important;
			max-width: 520px !important;
			margin: 0 auto !important;
			height: auto;
			padding-bottom: 3.5rem;
			box-sizing: border-box !important;
		}

		.card-details {
			max-height: 220px;
		}

		.card-button {
			bottom: 12px;
			width: 70%;
		}

		.projects-container {
			grid-template-columns: 1fr;
			padding: 1rem;
		}

		/* Make interactive controls comfortably large for touch */
		.card-button,
		.contact-me,
		.project-link {
			min-height: 44px;
			padding: 0.6rem 1rem;
		}

		/* Reduce some spacing on very small screens */
		@media (max-height: 600px) {
			.header-top {
				top: 8px;
			}
			.learn-more-btn {
				margin-top: 1rem;
				margin-bottom: 1rem;
			}
		}
	}

	/* Extra-strong overrides for very narrow phones where the headshot should be large */
	@media (max-width: 420px) {
		.words-and-pic {
			flex-direction: column !important;
			align-items: center !important;
			justify-content: center !important;
			width: 100% !important;
		}

		.headshot {
			/* make the headshot very prominent on small devices */
			display: block !important;
			width: min(84vw, 360px) !important;
			height: auto !important;
			max-width: none !important;
			border-radius: 50% !important;
			margin: 0.25rem auto 0.75rem auto !important;
			order: 0 !important;
		}

		.introduction,
		.intro-text {
			width: 100% !important;
			max-width: 100% !important;
			padding-left: 0 !important;
			padding-right: 0 !important;
			text-align: center !important;
			box-sizing: border-box !important;
		}

		.experience {
			align-items: center;
		}

		/* keep the fixed contact control hidden on very narrow screens */
		.contact-me {
			display: none !important;
		}
	}
</style>
