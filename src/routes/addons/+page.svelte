<script lang="ts">
	import { onMount } from 'svelte';
	import MatrixBackground from '$lib/components/MatrixBackground.svelte';

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

	const allAddons: AddOn[] = [
		{
			id: '1',
			name: 'Custom Chat System',
			description: 'Advanced chat with colored messages and custom formatting',
			author: 'Lunorbis Team',
			downloads: 2543,
			rating: 4.8,
			icon: '',
			category: 'Chat'
		},
		{
			id: '2',
			name: 'Economy System',
			description: 'Full-featured economy with shops, trading, and currency management',
			author: 'Community Dev',
			downloads: 1876,
			rating: 4.6,
			icon: '',
			category: 'Economy'
		},
		{
			id: '3',
			name: 'Advanced Teleport',
			description: 'Waypoints, homes, and warp system with advanced permissions',
			author: 'Lunorbis Team',
			downloads: 3124,
			rating: 4.9,
			icon: '',
			category: 'Teleport'
		},
		{
			id: '4',
			name: 'Quest System',
			description: 'Create and manage dynamic quests with rewards and progression',
			author: 'Creator Hub',
			downloads: 956,
			rating: 4.5,
			icon: '',
			category: 'Gameplay'
		},
		{
			id: '5',
			name: 'Custom Crafting',
			description: 'Define custom recipes and crafting mechanics with ease',
			author: 'Lunorbis Team',
			downloads: 2187,
			rating: 4.7,
			icon: '',
			category: 'Crafting'
		},
		{
			id: '6',
			name: 'Admin Tools Suite',
			description: 'Comprehensive administration tools and command systems',
			author: 'Server Admins',
			downloads: 1645,
			rating: 4.8,
			icon: '',
			category: 'Admin'
		},
		{
			id: '7',
			name: 'Auction House',
			description: 'Player-driven marketplace system with bidding functionality',
			author: 'Community Dev',
			downloads: 1234,
			rating: 4.4,
			icon: '',
			category: 'Economy'
		},
		{
			id: '8',
			name: 'Land Protection',
			description: 'Claim and protect your land with custom regions',
			author: 'Lunorbis Team',
			downloads: 2876,
			rating: 4.7,
			icon: '',
			category: 'Protection'
		},
		{
			id: '9',
			name: 'Pet System',
			description: 'Tame and customize unique pets with special abilities',
			author: 'Creator Hub',
			downloads: 1567,
			rating: 4.6,
			icon: '',
			category: 'Gameplay'
		}
	];

	let currentPage = $state(1);
	const addonsPerPage = 6;

	let paginatedAddons = $derived(
		allAddons.slice((currentPage - 1) * addonsPerPage, currentPage * addonsPerPage)
	);

	let totalPages = $derived(Math.ceil(allAddons.length / addonsPerPage));

	function goToPage(page: number) {
		if (page >= 1 && page <= totalPages) {
			currentPage = page;
			window.scrollTo({ top: 0, behavior: 'smooth' });
		}
	}



	onMount(() => {
		currentPage = 1;
	});
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

	<MatrixBackground count={50} />

	<main class="content">
		<section class="hero">
			<div class="hero-content">
				<h1 class="page-title">Minecraft Bedrock Add-ons</h1>
				<p class="page-subtitle">
					Extend your server's functionality with powerful, community-created add-ons
					built with the Lunorbis V8 runtime
				</p>
			</div>
		</section>

		<section class="addons-section">
			<div class="addons-container">
				{#each paginatedAddons as addon (addon.id)}
					<div class="addon-card">
						<div class="addon-header">
							{#if addon.icon}
								<div class="addon-icon">
									<img src={addon.icon} alt={addon.name} />
								</div>
							{/if}
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
									<span class="stat-icon">Downloads:</span>
									<span class="stat-text">{addon.downloads.toLocaleString()}</span>
								</div>
								<div class="stat">
									<span class="stat-icon">Rating:</span>
									<span class="stat-text">{addon.rating.toFixed(1)}</span>
								</div>
							</div>
							<button class="download-button">Download</button>
						</div>
					</div>
				{/each}
			</div>

			{#if totalPages > 1}
				<div class="pagination">
					<button
						class="pagination-btn"
						disabled={currentPage === 1}
						onclick={() => goToPage(currentPage - 1)}
					>
						Previous
					</button>

					{#each Array(totalPages) as _, i}
						{@const pageNum = i + 1}
						<button
							class="pagination-btn"
							class:active={currentPage === pageNum}
							onclick={() => goToPage(pageNum)}
						>
							{pageNum}
						</button>
					{/each}

					<button
						class="pagination-btn"
						disabled={currentPage === totalPages}
						onclick={() => goToPage(currentPage + 1)}
					>
						Next
					</button>
				</div>
			{/if}
		</section>

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
		min-height: 30vh;
		display: flex;
		align-items: center;
		justify-content: center;
		margin-bottom: 3rem;
	}

	.hero-content {
		text-align: center;
		width: 100%;
		max-width: 900px;
		padding: 0 1rem;
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
		max-width: 800px;
		margin: 0 auto;
		line-height: 1.6;
	}

	.addons-section {
		margin-bottom: 5rem;
	}

	.addons-container {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
		gap: 2rem;
		margin-bottom: 3rem;
	}

	.addon-card {
		background: rgba(60, 60, 70, 0.4);
		border: 1px solid rgba(255, 255, 255, 0.1);
		border-radius: 15px;
		padding: 1.5rem;
		transition: all 0.3s ease;
		display: flex;
		flex-direction: column;
		gap: 1rem;
	}

	.addon-card:hover {
		background: rgba(70, 70, 80, 0.5);
		border-color: rgba(0, 255, 207, 0.2);
		box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5);
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
		flex-shrink: 0;
		width: 50px;
		height: 50px;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.addon-icon img {
		width: 100%;
		height: 100%;
		object-fit: contain;
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
		display: inline;
	}

	.stat-text {
		color: var(--accent);
		font-weight: bold;
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

	.pagination {
		display: flex;
		justify-content: center;
		gap: 0.5rem;
		flex-wrap: wrap;
		margin-top: 3rem;
	}

	.pagination-btn {
		padding: 0.6rem 1rem;
		background: rgba(60, 60, 70, 0.4);
		color: #999;
		border: 1px solid rgba(255, 255, 255, 0.1);
		border-radius: 8px;
		font-family: 'Monocraft', monospace;
		cursor: pointer;
		transition: all 0.2s ease;
		font-size: 0.9rem;
	}

	.pagination-btn:hover:not(:disabled) {
		background: rgba(70, 70, 80, 0.5);
		color: var(--accent);
		border-color: rgba(0, 255, 207, 0.3);
	}

	.pagination-btn.active {
		background: var(--accent);
		color: #000;
		border-color: var(--accent);
	}

	.pagination-btn:disabled {
		opacity: 0.5;
		cursor: not-allowed;
	}

	.cta-section {
		margin-bottom: 3rem;
	}

	.cta-box {
		background: rgba(255, 255, 255, 0.03);
		backdrop-filter: blur(20px) saturate(180%) contrast(70%);
		-webkit-backdrop-filter: blur(20px) saturate(180%);
		border: 1px solid rgba(0, 255, 207, 0.2);
		border-radius: 20px;
		padding: 3rem;
		text-align: center;
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
			padding: 1.5rem 1rem;
		}

		.hero {
			margin-bottom: 2rem;
			min-height: 25vh;
		}

		.page-title {
			font-size: clamp(1.5rem, 6vw, 3rem);
		}

		.page-subtitle {
			font-size: 1rem;
		}

		.addons-container {
			grid-template-columns: 1fr;
			gap: 1.5rem;
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

		.addon-card {
			padding: 1.25rem;
		}

		.addon-name {
			font-size: 1.1rem;
		}

		.addon-footer {
			flex-direction: column;
			gap: 1rem;
			align-items: stretch;
		}

		.addon-stats {
			flex-direction: column;
			gap: 0.5rem;
		}

		.download-button {
			width: 100%;
		}

		.pagination {
			gap: 0.25rem;
		}

		.pagination-btn {
			padding: 0.5rem 0.75rem;
			font-size: 0.8rem;
		}
	}

	@media (max-width: 480px) {
		.content {
			padding: 1rem 0.75rem;
		}

		.hero {
			min-height: 20vh;
			margin-bottom: 1.5rem;
		}

		.page-title {
			font-size: clamp(1.25rem, 5vw, 2rem);
			letter-spacing: 1px;
		}

		.page-subtitle {
			font-size: 0.9rem;
		}

		.addons-container {
			gap: 1rem;
		}

		.addon-card {
			padding: 1rem;
			gap: 0.75rem;
		}

		.addon-icon {
			width: 40px;
			height: 40px;
		}

		.addon-name {
			font-size: 1rem;
		}

		.addon-author {
			font-size: 0.75rem;
		}

		.category-badge {
			font-size: 0.7rem;
			padding: 0.3rem 0.6rem;
		}

		.addon-description {
			font-size: 0.85rem;
		}

		.stat {
			font-size: 0.8rem;
		}

		.download-button {
			padding: 0.5rem 1rem;
			font-size: 0.8rem;
		}

		.cta-box {
			padding: 1.5rem;
		}

		.cta-box h2 {
			font-size: 1.25rem;
			margin-bottom: 0.75rem;
		}

		.cta-box p {
			font-size: 0.95rem;
		}

		.cta-button {
			padding: 0.8rem 2rem;
			font-size: 0.9rem;
		}
	}
</style>
