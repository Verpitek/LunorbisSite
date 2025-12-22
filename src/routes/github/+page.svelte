<script lang="ts">
	import DescriptionBlock from '$lib/components/DescriptionBlock.svelte';
	import Footer from '$lib/components/Footer.svelte';

	interface Repository {
		name: string;
		description: string;
		url: string;
		language: string;
		stars: number;
		topics: string[];
	}

	const repositories: Repository[] = [
		{
			name: 'Lunorbis Core',
			description: 'The main runtime engine that replaces QuickJS with V8 for Bedrock',
			url: 'https://github.com/lunorbis/lunorbis-core',
			language: 'C++',
			stars: 2847,
			topics: ['bedrock', 'minecraft', 'v8', 'runtime']
		},
		{
			name: 'Bedrock API',
			description: 'Comprehensive API documentation and type definitions for Bedrock development',
			url: 'https://github.com/lunorbis/bedrock-api',
			language: 'TypeScript',
			stars: 1543,
			topics: ['bedrock', 'api', 'documentation', 'typescript']
		},
		{
			name: 'Add-on Toolkit',
			description: 'Official development toolkit and utilities for creating Lunorbis add-ons',
			url: 'https://github.com/lunorbis/addon-toolkit',
			language: 'TypeScript',
			stars: 892,
			topics: ['addon', 'toolkit', 'development', 'bedrock']
		},
		{
			name: 'Server Examples',
			description: 'Complete working examples and starter templates for Lunorbis servers',
			url: 'https://github.com/lunorbis/server-examples',
			language: 'TypeScript',
			stars: 654,
			topics: ['examples', 'templates', 'tutorial', 'bedrock']
		},
		{
			name: 'Performance Benchmarks',
			description: 'Comprehensive benchmarking suite comparing V8 vs QuickJS performance',
			url: 'https://github.com/lunorbis/benchmarks',
			language: 'Python',
			stars: 456,
			topics: ['benchmarks', 'performance', 'v8', 'comparison']
		},
		{
			name: 'Community Add-ons',
			description: 'Curated collection of high-quality community-created add-ons',
			url: 'https://github.com/lunorbis/community-addons',
			language: 'TypeScript',
			stars: 721,
			topics: ['addons', 'community', 'showcase', 'bedrock']
		}
	];

	function getLanguageColor(language: string): string {
		const colors: Record<string, string> = {
			'C++': '#00ffcf',
			'TypeScript': '#3178c6',
			'Python': '#ffd43b',
			'JavaScript': '#f1e05a'
		};
		return colors[language] || '#999';
	}
</script>

<svelte:head>
	<title>GitHub - Lunorbis</title>
	<meta name="description" content="Explore Lunorbis open-source projects on GitHub" />
</svelte:head>

<div class="page github-page">
	<div class="background-effects">
		<div class="moving-stripes"></div>
		<div class="crt-vignette"></div>
		<div class="scanlines"></div>
	</div>

	<main class="content">
		<!-- Hero Section -->
		<section class="hero">
			<div class="hero-content">
				<div class="hero-icon">🐙</div>
				<h1 class="page-title">Open Source on GitHub</h1>
				<p class="page-subtitle">
					Lunorbis is proudly open-source. Explore our repositories, contribute to the
					project, and help us build the future of Minecraft Bedrock servers
				</p>
			</div>
		</section>

		<!-- GitHub Stats Section -->
		<section class="stats-section">
			<div class="stats-grid">
				<div class="stat-card">
					<DescriptionBlock icon="⭐" title="Stars">
						<span class="stat-number">8,113</span>
					</DescriptionBlock>
				</div>
				<div class="stat-card">
					<DescriptionBlock icon="🍴" title="Forks">
						<span class="stat-number">1,247</span>
					</DescriptionBlock>
				</div>
				<div class="stat-card">
					<DescriptionBlock icon="👥" title="Contributors">
						<span class="stat-number">156</span>
					</DescriptionBlock>
				</div>
				<div class="stat-card">
					<DescriptionBlock icon="📦" title="Repositories">
						<span class="stat-number">12</span>
					</DescriptionBlock>
				</div>
			</div>
		</section>

		<!-- Repositories Section -->
		<section class="repos-section">
			<h2 class="section-title">Featured Repositories</h2>
			<div class="repos-container">
				{#each repositories as repo (repo.name)}
					<a href={repo.url} target="_blank" rel="noopener noreferrer" class="repo-card">
						<div class="repo-header">
							<h3 class="repo-name">
								<span class="repo-icon">📂</span>
								{repo.name}
							</h3>
							<div class="repo-meta">
								<span class="language-badge" style="color: {getLanguageColor(repo.language)}">
									<span class="language-dot"></span>
									{repo.language}
								</span>
								<span class="stars-badge">
									⭐ {repo.stars.toLocaleString()}
								</span>
							</div>
						</div>

						<p class="repo-description">{repo.description}</p>

						<div class="repo-topics">
							{#each repo.topics as topic}
								<span class="topic-badge">{topic}</span>
							{/each}
						</div>
					</a>
				{/each}
			</div>
		</section>

		<!-- Contributing Section -->
		<section class="contributing-section">
			<h2 class="section-title">Contribute to Lunorbis</h2>
			<div class="contribute-grid">
				<div class="contribute-card">
					<DescriptionBlock icon="🐛" title="Report Bugs">
						Found an issue? Help us improve by reporting bugs and edge cases to our issue
						tracker
					</DescriptionBlock>
				</div>
				<div class="contribute-card">
					<DescriptionBlock icon="✨" title="Suggest Features">
						Have an idea to make Lunorbis better? Share your feature requests and
						suggestions
					</DescriptionBlock>
				</div>
				<div class="contribute-card">
					<DescriptionBlock icon="💻" title="Submit PRs">
						Contribute code improvements, documentation, or new features through pull
						requests
					</DescriptionBlock>
				</div>
				<div class="contribute-card">
					<DescriptionBlock icon="📚" title="Write Docs">
						Help us document features, write tutorials, and improve our knowledge base
					</DescriptionBlock>
				</div>
			</div>

			<div class="contributing-box">
				<h3>Getting Started with Contributions</h3>
				<ol class="contribution-steps">
					<li>Fork the repository you want to contribute to</li>
					<li>Create a new branch for your changes</li>
					<li>Make your improvements or fixes</li>
					<li>Write clear commit messages and tests</li>
					<li>Submit a pull request with a detailed description</li>
					<li>Review feedback and iterate with maintainers</li>
				</ol>
				<a href="https://github.com/lunorbis/lunorbis-core/blob/main/CONTRIBUTING.md" target="_blank" rel="noopener noreferrer" class="contributing-link">
					View Full Contributing Guide →
				</a>
			</div>
		</section>

		<!-- CTA Section -->
		<section class="cta-section">
			<div class="cta-box">
				<h2>Join Our Community</h2>
				<p>Star us on GitHub, discuss with fellow developers, and help shape the future</p>
				<div class="cta-buttons">
					<a href="https://github.com/lunorbis" target="_blank" rel="noopener noreferrer" class="cta-button primary">
						Visit GitHub
					</a>
					<a href="https://github.com/lunorbis/lunorbis-core" target="_blank" rel="noopener noreferrer" class="cta-button secondary">
						View Main Repo
					</a>
				</div>
			</div>
		</section>
	</main>

	<Footer />
</div>

<style>
	:root {
		--accent: #00ffcf;
		--accent-rgb: 0, 255, 207;
		--bg-deep: #050606;
		--bg-stripe: #0a0d0d;
	}

	.page {
		position: relative;
		background: var(--bg-deep);
		min-height: 100vh;
		color: white;
		overflow-x: hidden;
	}

	.background-effects {
		position: fixed;
		inset: 0;
		pointer-events: none;
		z-index: 0;
	}

	.moving-stripes {
		position: fixed;
		inset: -100px;
		z-index: 0;
		background: repeating-linear-gradient(
			-45deg,
			var(--bg-deep),
			var(--bg-deep) 30px,
			var(--bg-stripe) 30px,
			var(--bg-stripe) 60px
		);
		background-size: 84.85px 84.85px;
		animation: stripe-move 20s linear infinite;
	}

	@keyframes stripe-move {
		from {
			background-position: 0 0;
		}
		to {
			background-position: 84.85px 84.85px;
		}
	}

	.crt-vignette {
		position: fixed;
		inset: 0;
		background: radial-gradient(circle, transparent 40%, rgba(0, 0, 0, 0.95) 100%);
		pointer-events: none;
		z-index: 100;
	}

	.scanlines {
		position: fixed;
		inset: 0;
		background: linear-gradient(to bottom, rgba(255, 255, 255, 0.02) 50%, transparent 50%);
		background-size: 100% 4px;
		pointer-events: none;
		z-index: 101;
	}

	.content {
		position: relative;
		z-index: 2;
		max-width: 1400px;
		margin: 0 auto;
		padding: 2rem 1rem;
	}

	.hero {
		min-height: 40vh;
		display: flex;
		align-items: center;
		justify-content: center;
		margin-bottom: 4rem;
	}

	.hero-content {
		text-align: center;
	}

	.hero-icon {
		font-size: 4rem;
		margin-bottom: 1rem;
		display: inline-block;
	}

	.page-title {
		font-size: clamp(2rem, 8vw, 4rem);
		margin: 0 0 1rem 0;
		color: var(--accent);
		letter-spacing: 3px;
		text-shadow: 0 0 30px rgba(var(--accent-rgb), 0.3);
	}

	.page-subtitle {
		font-size: 1.2rem;
		color: #999;
		max-width: 700px;
		margin: 0;
		line-height: 1.6;
	}

	.section-title {
		text-align: center;
		font-size: 2rem;
		color: var(--accent);
		margin-bottom: 3rem;
		letter-spacing: 2px;
	}

	.stats-section {
		margin-bottom: 5rem;
	}

	.stats-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
		gap: 2rem;
	}

	.stat-card {
		min-height: 180px;
	}

	.stat-number {
		font-size: 2.5rem;
		color: var(--accent);
		font-weight: bold;
	}

	.repos-section {
		margin-bottom: 5rem;
	}

	.repos-container {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
		gap: 2rem;
	}

	.repo-card {
		background: rgba(255, 255, 255, 0.02);
		backdrop-filter: blur(10px);
		border: 1px solid rgba(255, 255, 255, 0.1);
		border-radius: 15px;
		padding: 1.5rem;
		transition: all 0.3s ease;
		display: flex;
		flex-direction: column;
		gap: 1rem;
		text-decoration: none;
		color: inherit;
		cursor: pointer;
	}

	.repo-card:hover {
		background: rgba(255, 255, 255, 0.05);
		border-color: rgba(0, 255, 207, 0.2);
		box-shadow: 0 0 30px rgba(0, 255, 207, 0.1);
		transform: translateY(-3px);
	}

	.repo-header {
		padding-bottom: 1rem;
		border-bottom: 1px solid rgba(255, 255, 255, 0.1);
	}

	.repo-name {
		margin: 0 0 0.5rem 0;
		color: var(--accent);
		font-size: 1.2rem;
		display: flex;
		align-items: center;
		gap: 0.5rem;
	}

	.repo-icon {
		display: inline-block;
		font-size: 1.3rem;
	}

	.repo-meta {
		display: flex;
		gap: 1rem;
		align-items: center;
		flex-wrap: wrap;
	}

	.language-badge {
		display: flex;
		align-items: center;
		gap: 0.4rem;
		font-size: 0.85rem;
	}

	.language-dot {
		display: inline-block;
		width: 8px;
		height: 8px;
		border-radius: 50%;
		background: currentColor;
	}

	.stars-badge {
		display: flex;
		align-items: center;
		gap: 0.3rem;
		font-size: 0.85rem;
		color: #999;
	}

	.repo-description {
		margin: 0;
		color: #999;
		font-size: 0.95rem;
		line-height: 1.5;
		flex: 1;
	}

	.repo-topics {
		display: flex;
		flex-wrap: wrap;
		gap: 0.5rem;
	}

	.topic-badge {
		display: inline-block;
		padding: 0.3rem 0.8rem;
		background: rgba(0, 255, 207, 0.08);
		border: 1px solid rgba(0, 255, 207, 0.2);
		color: var(--accent);
		border-radius: 20px;
		font-size: 0.7rem;
		font-weight: bold;
		text-transform: lowercase;
	}

	.contributing-section {
		margin-bottom: 5rem;
	}

	.contribute-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
		gap: 2rem;
		margin-bottom: 3rem;
	}

	.contribute-card {
		min-height: 250px;
	}

	.contributing-box {
		background: linear-gradient(135deg, rgba(0, 255, 207, 0.05), rgba(0, 255, 207, 0.02));
		border: 1px solid rgba(0, 255, 207, 0.2);
		border-radius: 15px;
		padding: 2rem;
		backdrop-filter: blur(10px);
	}

	.contributing-box h3 {
		margin: 0 0 1.5rem 0;
		color: var(--accent);
		font-size: 1.5rem;
		letter-spacing: 1px;
	}

	.contribution-steps {
		margin: 0 0 1.5rem 0;
		padding-left: 1.5rem;
		color: #999;
		line-height: 1.8;
	}

	.contribution-steps li {
		margin-bottom: 0.8rem;
	}

	.contributing-link {
		display: inline-block;
		color: var(--accent);
		text-decoration: none;
		font-weight: bold;
		transition: all 0.2s ease;
	}

	.contributing-link:hover {
		text-shadow: 0 0 10px rgba(var(--accent-rgb), 0.4);
	}

	.cta-section {
		margin-bottom: 3rem;
	}

	.cta-box {
		background: linear-gradient(135deg, rgba(0, 255, 207, 0.08), rgba(0, 255, 207, 0.02));
		border: 2px solid rgba(0, 255, 207, 0.2);
		border-radius: 20px;
		padding: 3rem;
		text-align: center;
		backdrop-filter: blur(10px);
	}

	.cta-box h2 {
		margin: 0 0 1rem 0;
		color: var(--accent);
		font-size: 2rem;
		letter-spacing: 2px;
	}

	.cta-box p {
		margin: 0 0 2rem 0;
		color: #999;
		font-size: 1.1rem;
	}

	.cta-buttons {
		display: flex;
		gap: 1rem;
		justify-content: center;
		flex-wrap: wrap;
	}

	.cta-button {
		padding: 1rem 2rem;
		border-radius: 8px;
		font-family: 'Monocraft', monospace;
		font-weight: bold;
		cursor: pointer;
		transition: all 0.3s ease;
		font-size: 1rem;
		text-decoration: none;
		display: inline-block;
		border: none;
	}

	.cta-button.primary {
		background: var(--accent);
		color: #000;
	}

	.cta-button.primary:hover {
		transform: translateY(-3px);
		box-shadow: 0 0 30px rgba(var(--accent-rgb), 0.5);
	}

	.cta-button.secondary {
		background: rgba(0, 255, 207, 0.1);
		color: var(--accent);
		border: 1px solid rgba(0, 255, 207, 0.3);
	}

	.cta-button.secondary:hover {
		background: rgba(0, 255, 207, 0.2);
		box-shadow: 0 0 20px rgba(var(--accent-rgb), 0.3);
	}

	@media (max-width: 768px) {
		.content {
			padding: 1.5rem 0.75rem;
		}

		.hero {
			margin-bottom: 2rem;
			min-height: 30vh;
		}

		.stats-grid {
			grid-template-columns: repeat(2, 1fr);
			gap: 1rem;
		}

		.repos-container {
			grid-template-columns: 1fr;
		}

		.contribute-grid {
			grid-template-columns: 1fr;
		}

		.cta-box {
			padding: 2rem;
		}

		.cta-box h2 {
			font-size: 1.5rem;
		}

		.cta-buttons {
			flex-direction: column;
		}

		.cta-button {
			width: 100%;
		}
	}
</style>
