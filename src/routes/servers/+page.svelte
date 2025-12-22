<script lang="ts">
	import { onMount } from 'svelte';
	import InformationBlock from '$lib/components/InformationBlock.svelte';
	import MatrixBackground from '$lib/components/MatrixBackground.svelte';

	interface Server {
		id: string;
		name: string;
		description: string;
		players: number;
		maxPlayers: number;
		icon: string;
		status: 'online' | 'offline';
	}

	const allServers: Server[] = [
		{
			id: '1',
			name: 'Creative Server',
			description: 'Build anything your imagination allows with unlimited resources',
			players: 124,
			maxPlayers: 200,
			icon: '',
			status: 'online'
		},
		{
			id: '2',
			name: 'Survival Server',
			description: 'Classic survival experience with custom plugins and modifications',
			players: 87,
			maxPlayers: 150,
			icon: '',
			status: 'online'
		},
		{
			id: '3',
			name: 'PvP Arena',
			description: 'Competitive player-versus-player combat on custom maps',
			players: 45,
			maxPlayers: 100,
			icon: '',
			status: 'online'
		},
		{
			id: '4',
			name: 'Skyblock',
			description: 'Survive on islands floating in the sky with limited resources',
			players: 92,
			maxPlayers: 175,
			icon: '',
			status: 'online'
		},
		{
			id: '5',
			name: 'Parkour Challenge',
			description: 'Test your skills in challenging parkour courses and obstacles',
			players: 28,
			maxPlayers: 80,
			icon: '',
			status: 'offline'
		},
		{
			id: '6',
			name: 'Minigames Hub',
			description: 'Fast-paced mini-games with friends and players worldwide',
			players: 156,
			maxPlayers: 250,
			icon: '',
			status: 'online'
		},
		{
			id: '7',
			name: 'Adventure World',
			description: 'Epic story-driven adventure with quests and dungeons',
			players: 67,
			maxPlayers: 120,
			icon: '',
			status: 'online'
		},
		{
			id: '8',
			name: 'Roleplay Server',
			description: 'Immersive roleplay experience with custom economy and jobs',
			players: 102,
			maxPlayers: 180,
			icon: '',
			status: 'online'
		},
		{
			id: '9',
			name: 'Prison Break',
			description: 'Escape from prison and earn your freedom through missions',
			players: 34,
			maxPlayers: 100,
			icon: '',
			status: 'offline'
		}
	];

	let currentPage = $state(1);
	const serversPerPage = 6;

	let paginatedServers = $derived(
		allServers.slice(
			(currentPage - 1) * serversPerPage,
			currentPage * serversPerPage
		)
	);

	let totalPages = $derived(Math.ceil(allServers.length / serversPerPage));

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
	<title>Servers - Lunorbis</title>
	<meta name="description" content="Explore Lunorbis-powered Minecraft Bedrock servers" />
</svelte:head>

<div class="page servers-page">
	<div class="background-effects">
		<div class="moving-stripes"></div>
		<div class="crt-vignette"></div>
		<div class="scanlines"></div>
	</div>

	<MatrixBackground count={50} />

	<main class="content">
		<section class="hero">
			<div class="hero-content">
				<h1 class="page-title">Server Network</h1>
				<p class="page-subtitle">
					Discover Lunorbis-powered Minecraft Bedrock servers with enhanced performance
					and extended scripting capabilities
				</p>
			</div>
		</section>

		<section class="servers-section">
			<div class="servers-container">
				{#each paginatedServers as server (server.id)}
					<div class="server-card">
						<InformationBlock title={server.name} icon={server.icon} iconType="image">
							<p>{server.description}</p>
							<div class="server-stats">
								<div class="stat">
									<span class="stat-label">Players</span>
									<span class="stat-value">{server.players}/{server.maxPlayers}</span>
								</div>
								<div class="stat">
									<span class="stat-label">Status</span>
									<span class="stat-value" class:offline={server.status === 'offline'}>
										{server.status === 'online' ? '[ONLINE]' : '[OFFLINE]'}
									</span>
								</div>
							</div>
							<button class="connect-button">
								{server.status === 'online' ? 'Connect Now' : 'Coming Soon'}
							</button>
						</InformationBlock>
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

	.servers-section {
		margin-bottom: 4rem;
	}

	.servers-container {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
		gap: 2rem;
		margin-bottom: 3rem;
	}

	.server-card {
		min-height: 350px;
	}

	.server-stats {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 1rem;
		margin: 1.5rem 0;
		padding: 1rem 0;
		border-top: 1px solid rgba(255, 255, 255, 0.1);
		border-bottom: 1px solid rgba(255, 255, 255, 0.1);
	}

	.stat {
		display: flex;
		flex-direction: column;
		gap: 0.25rem;
	}

	.stat-label {
		color: #666;
		font-size: 0.75rem;
		text-transform: uppercase;
		letter-spacing: 1px;
	}

	.stat-value {
		color: var(--accent);
		font-size: 1rem;
		font-weight: bold;
	}

	.stat-value.offline {
		color: #ff6b6b;
	}

	.connect-button {
		width: 100%;
		padding: 0.8rem;
		margin-top: 1rem;
		background: linear-gradient(135deg, var(--accent), rgba(0, 255, 207, 0.8));
		color: #000;
		border: none;
		border-radius: 8px;
		font-family: 'Monocraft', monospace;
		font-weight: bold;
		cursor: pointer;
		transition: all 0.3s ease;
		font-size: 0.95rem;
	}

	.connect-button:hover {
		transform: translateY(-2px);
		box-shadow: 0 0 20px rgba(var(--accent-rgb), 0.5);
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

		.servers-container {
			grid-template-columns: 1fr;
			gap: 1.5rem;
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

		.servers-container {
			gap: 1rem;
		}

		.server-card {
			min-height: auto;
		}

		.connect-button {
			padding: 0.6rem;
			font-size: 0.85rem;
		}
	}
</style>
