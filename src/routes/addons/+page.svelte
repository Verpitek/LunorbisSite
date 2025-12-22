<script lang="ts">
	import DescriptionBlock from '$lib/components/DescriptionBlock.svelte';
	import Footer from '$lib/components/Footer.svelte';

	interface AddOn {
		id: string;
		name: string;
		description: string;
		author: string;
		downloads: number;
		rating: number;
		icon: string;
		category: string;
	}

	const addons: AddOn[] = [
		{
			id: '1',
			name: 'Custom Chat System',
			description: 'Advanced chat with colored messages, emojis, and custom formatting',
			author: 'Lunorbis Team',
			downloads: 2543,
			rating: 4.8,
			icon: '💬',
			category: 'Chat'
		},
		{
			id: '2',
			name: 'Economy System',
			description: 'Full-featured economy with shops, trading, and currency management',
			author: 'Community Dev',
			downloads: 1876,
			rating: 4.6,
			icon: '💰',
			category: 'Economy'
		},
		{
			id: '3',
			name: 'Advanced Teleport',
			description: 'Waypoints, homes, and warp system with advanced permissions',
			author: 'Lunorbis Team',
			downloads: 3124,
			rating: 4.9,
			icon: '🌍',
			category: 'Teleport'
		},
		{
			id: '4',
			name: 'Quest System',
			description: 'Create and manage dynamic quests with rewards and progression',
			author: 'Creator Hub',
			downloads: 956,
			rating: 4.5,
			icon: '📜',
			category: 'Gameplay'
		},
		{
			id: '5',
			name: 'Custom Crafting',
			description: 'Define custom recipes and crafting mechanics with ease',
			author: 'Lunorbis Team',
			downloads: 2187,
			rating: 4.7,
			icon: '🔨',
			category: 'Crafting'
		},
		{
			id: '6',
			name: 'Admin Tools Suite',
			description: 'Comprehensive administration tools and command systems',
			author: 'Server Admins',
			downloads: 1645,
			rating: 4.8,
			icon: '🔧',
			category: 'Admin'
		}
	];

	function getStarRating(rating: number) {
		return '⭐'.repeat(Math.floor(rating)) + (rating % 1 >= 0.5 ? '✨' : '');
	}
</script>

<svelte:head>
	<title>Add-ons - Lunorbis</title>
	<meta name="description" content="Discover Minecraft Bedrock add-ons powered by Lunorbis runtime" />
</svelte:head>

<div class="page addons-page">
	<div class="background-effects">
		<div class="moving-stripes"></div>
		<div class="crt-vignette"></div>
		<div class="scanlines"></div>
	</div>

	<main class="content">
		<!-- Hero Section -->
		<section class="hero">
			<div class="hero-content">
				<h1 class="page-title">Minecraft Bedrock Add-ons</h1>
				<p class="page-subtitle">
					Extend your server's functionality with powerful, community-created add-ons
					built with the Lunorbis V8 runtime
				</p>
			</div>
		</section>

		<!-- Features Overview -->
		<section class="features-section">
			<h2 class="section-title">Why Use Lunorbis Add-ons?</h2>
			<div class="features-grid">
				<div class="feature-card">
					<DescriptionBlock icon="⚡" title="High Performance">
						V8 JIT compilation delivers near-native performance for script execution
					</DescriptionBlock>
				</div>
				<div class="feature-card">
					<DescriptionBlock icon="📁" title="File System Access">
						Read and write files directly with extended filesystem APIs
					</DescriptionBlock>
				</div>
				<div class="feature-card">
					<DescriptionBlock icon="🌐" title="Network Enabled">
						Make external HTTP requests and connect to external services
					</DescriptionBlock>
				</div>
				<div class="feature-card">
					<DescriptionBlock icon="🧩" title="Modular Design">
						Build reusable components and libraries for easier development
					</DescriptionBlock>
				</div>
			</div>
		</section>

		<!-- Add-ons Showcase -->
		<section class="addons-section">
			<h2 class="section-title">Featured Add-ons</h2>
			<div class="addons-container">
				{#each addons as addon (addon.id)}
					<div class="addon-card">
						<div class="addon-header">
							<div class="addon-icon">{addon.icon}</div>
							<div class="addon-info">
								<h3 class="addon-name">{addon.name}</h3>
								<p class="addon-author">by {addon.author}</p>
							</div>
							<div class="addon-category">
								<span class="category-badge">{addon.category}</span>
							</div>
						</div>

						<p class="addon-description">{addon.description}</p>

						<div class="addon-footer">
							<div class="addon-stats">
								<div class="stat">
									<span class="stat-icon">📥</span>
									<span class="stat-text">{addon.downloads.toLocaleString()}</span>
								</div>
								<div class="stat">
									<span class="stat-icon">{getStarRating(addon.rating)}</span>
									<span class="stat-text">{addon.rating.toFixed(1)}</span>
								</div>
							</div>
							<button class="download-button">Download</button>
						</div>
					</div>
				{/each}
			</div>
		</section>

		<!-- CTA Section -->
		<section class="cta-section">
			<div class="cta-box">
				<h2>Create Your Own Add-on</h2>
				<p>
					Use our comprehensive API and documentation to build powerful add-ons for
					Minecraft Bedrock servers powered by Lunorbis
				</p>
				<button class="cta-button">View Developer Docs</button>
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

	.features-section {
		margin-bottom: 5rem;
	}

	.features-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
		gap: 2rem;
	}

	.feature-card {
		min-height: 250px;
	}

	.addons-section {
		margin-bottom: 5rem;
	}

	.addons-container {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
		gap: 2rem;
	}

	.addon-card {
		background: rgba(255, 255, 255, 0.02);
		backdrop-filter: blur(10px);
		border: 1px solid rgba(255, 255, 255, 0.1);
		border-radius: 15px;
		padding: 1.5rem;
		transition: all 0.3s ease;
		display: flex;
		flex-direction: column;
		gap: 1rem;
	}

	.addon-card:hover {
		background: rgba(255, 255, 255, 0.05);
		border-color: rgba(0, 255, 207, 0.2);
		box-shadow: 0 0 30px rgba(0, 255, 207, 0.1);
		transform: translateY(-3px);
	}

	.addon-header {
		display: flex;
		align-items: flex-start;
		gap: 1rem;
		padding-bottom: 1rem;
		border-bottom: 1px solid rgba(255, 255, 255, 0.1);
	}

	.addon-icon {
		font-size: 2.5rem;
		flex-shrink: 0;
	}

	.addon-info {
		flex: 1;
	}

	.addon-name {
		margin: 0;
		color: var(--accent);
		font-size: 1.2rem;
		letter-spacing: 0.5px;
	}

	.addon-author {
		margin: 0.25rem 0 0 0;
		color: #666;
		font-size: 0.85rem;
	}

	.addon-category {
		flex-shrink: 0;
	}

	.category-badge {
		display: inline-block;
		padding: 0.4rem 0.8rem;
		background: rgba(0, 255, 207, 0.1);
		border: 1px solid rgba(0, 255, 207, 0.3);
		color: var(--accent);
		border-radius: 20px;
		font-size: 0.75rem;
		font-weight: bold;
		letter-spacing: 0.5px;
	}

	.addon-description {
		margin: 0;
		color: #999;
		font-size: 0.95rem;
		line-height: 1.5;
		flex: 1;
	}

	.addon-footer {
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding-top: 1rem;
		border-top: 1px solid rgba(255, 255, 255, 0.1);
	}

	.addon-stats {
		display: flex;
		gap: 1.5rem;
	}

	.stat {
		display: flex;
		align-items: center;
		gap: 0.5rem;
		color: #999;
		font-size: 0.85rem;
	}

	.stat-icon {
		display: inline-block;
		font-size: 1rem;
	}

	.stat-text {
		display: inline;
	}

	.download-button {
		padding: 0.6rem 1.5rem;
		background: linear-gradient(135deg, var(--accent), rgba(0, 255, 207, 0.8));
		color: #000;
		border: none;
		border-radius: 8px;
		font-family: 'Monocraft', monospace;
		font-weight: bold;
		cursor: pointer;
		transition: all 0.3s ease;
		font-size: 0.9rem;
	}

	.download-button:hover {
		transform: translateY(-2px);
		box-shadow: 0 0 15px rgba(var(--accent-rgb), 0.5);
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
		max-width: 600px;
		margin-left: auto;
		margin-right: auto;
	}

	.cta-button {
		padding: 1rem 2.5rem;
		background: var(--accent);
		color: #000;
		border: none;
		border-radius: 8px;
		font-family: 'Monocraft', monospace;
		font-weight: bold;
		cursor: pointer;
		transition: all 0.3s ease;
		font-size: 1rem;
		letter-spacing: 0.5px;
	}

	.cta-button:hover {
		transform: translateY(-3px);
		box-shadow: 0 0 30px rgba(var(--accent-rgb), 0.5);
	}

	@media (max-width: 768px) {
		.content {
			padding: 1.5rem 0.75rem;
		}

		.hero {
			margin-bottom: 2rem;
			min-height: 30vh;
		}

		.features-grid {
			grid-template-columns: 1fr;
		}

		.addons-container {
			grid-template-columns: 1fr;
		}

		.cta-box {
			padding: 2rem;
		}

		.cta-box h2 {
			font-size: 1.5rem;
		}

		.addon-header {
			flex-direction: column;
			gap: 0.5rem;
		}

		.addon-category {
			flex: 1;
		}
	}
</style>
