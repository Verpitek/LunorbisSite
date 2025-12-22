<script lang="ts">
	import lunorbisLogo from '$lib/assets/lunorbis.svg';

	let { currentPath = '/' } = $props();
</script>

<nav class="navbar">
	<div class="navbar-content">
		<div class="navbar-brand">
			<a href="/" class="brand-link">
				<img src={lunorbisLogo} alt="Lunorbis" class="brand-logo" />
				<span class="brand-name">LUNORBIS</span>
			</a>
		</div>

		<ul class="navbar-menu">
			<li>
				<a href="/" class:active={currentPath === '/'}>Home</a>
			</li>
			<li>
				<a href="/servers" class:active={currentPath === '/servers'}>Servers</a>
			</li>
			<li>
				<a href="/addons" class:active={currentPath === '/addons'}>Add-ons</a>
			</li>
			<li>
				<a href="/github" class:active={currentPath === '/github'}>GitHub</a>
			</li>
		</ul>

		<div class="navbar-end">
			<a href="https://discord.gg/" target="_blank" rel="noopener noreferrer" class="discord-link">
				Discord
			</a>
		</div>
	</div>
</nav>

<style>
	:root {
		--accent: #00ffcf;
		--accent-rgb: 0, 255, 207;
		--bg-deep: #050606;
	}

	.navbar {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		z-index: 1000;
		background: rgba(255, 255, 255, 0.03);
		backdrop-filter: blur(20px) saturate(180%) contrast(70%);
		-webkit-backdrop-filter: blur(20px) saturate(180%);
		border-bottom: 1px solid rgba(255, 255, 255, 0.15);
		padding: 0;
	}

	.navbar-content {
		max-width: 1400px;
		margin: 0 auto;
		padding: 1rem 2rem;
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 2rem;
	}

	.navbar-brand {
		flex-shrink: 0;
	}

	.brand-link {
		display: flex;
		align-items: center;
		gap: 0.75rem;
		text-decoration: none;
		color: var(--accent);
		transition: opacity 0.2s ease;
	}

	.brand-link:hover {
		opacity: 0.8;
	}

	.brand-logo {
		width: 40px;
		height: 40px;
		filter: drop-shadow(0 0 10px rgba(0, 255, 207, 0.2));
	}

	.brand-name {
		font-size: 1.1rem;
		font-weight: bold;
		letter-spacing: 2px;
	}

	.navbar-menu {
		list-style: none;
		margin: 0;
		padding: 0;
		display: flex;
		gap: 2rem;
		flex: 1;
	}

	.navbar-menu a {
		color: #999;
		text-decoration: none;
		font-size: 0.95rem;
		letter-spacing: 0.5px;
		transition: color 0.2s ease;
		position: relative;
	}

	.navbar-menu a:hover {
		color: var(--accent);
	}

	.navbar-menu a.active {
		color: var(--accent);
	}

	.navbar-menu a.active::after {
		content: '';
		position: absolute;
		bottom: -8px;
		left: 0;
		right: 0;
		height: 2px;
		background: var(--accent);
	}

	.navbar-end {
		flex-shrink: 0;
	}

	.discord-link {
		display: inline-block;
		padding: 0.6rem 1.5rem;
		background: linear-gradient(135deg, rgba(88, 101, 242, 0.2), rgba(88, 101, 242, 0.1));
		border: 1px solid rgba(88, 101, 242, 0.3);
		color: #fff;
		text-decoration: none;
		border-radius: 20px;
		font-size: 0.9rem;
		font-weight: bold;
		transition: all 0.2s ease;
	}

	.discord-link:hover {
		background: linear-gradient(135deg, rgba(88, 101, 242, 0.3), rgba(88, 101, 242, 0.2));
		border-color: rgba(88, 101, 242, 0.5);
	}

	@media (max-width: 768px) {
		.navbar-content {
			padding: 0.75rem 1rem;
			gap: 1rem;
		}

		.brand-logo {
			width: 32px;
			height: 32px;
		}

		.brand-name {
			font-size: 1rem;
		}

		.navbar-menu {
			gap: 1rem;
			font-size: 0.85rem;
		}

		.discord-link {
			padding: 0.5rem 1rem;
			font-size: 0.8rem;
		}
	}

	@media (max-width: 480px) {
		.navbar-menu {
			gap: 0.75rem;
		}

		.navbar-menu a {
			font-size: 0.8rem;
		}
	}
</style>
