<script lang="ts">
	import DiscordButton from './DiscordButton.svelte';
	import lunorbisLogo from '$lib/assets/lunorbis.svg';

	export let discordUrl: string = 'https://discord.gg/';
</script>

<footer class="footer">
	<div class="footer-content">
		<!-- Navigation Section -->
		<nav class="footer-nav">
			<div class="nav-column">
				<h4 class="nav-heading">Project</h4>
				<ul class="nav-list">
					<li><a href="/">Home</a></li>
					<li><a href="/servers">Servers</a></li>
					<li><a href="/addons">Add-ons</a></li>
					<li><a href="/github">GitHub</a></li>
				</ul>
			</div>

			<div class="nav-column">
				<h4 class="nav-heading">Resources</h4>
				<ul class="nav-list">
					<li><a href="https://docs.lunorbis.dev" target="_blank" rel="noopener noreferrer">Documentation</a></li>
					<li><a href="https://github.com/lunorbis" target="_blank" rel="noopener noreferrer">Source Code</a></li>
					<li><a href="/api">API</a></li>
					<li><a href="/support">Support</a></li>
				</ul>
			</div>

			<div class="nav-column">
				<h4 class="nav-heading">Community</h4>
				<ul class="nav-list">
					<li><a href="/forum">Forum</a></li>
					<li><a href="/wiki">Wiki</a></li>
					<li><a href="/showcase">Showcase</a></li>
					<li><a href="/contribute">Contribute</a></li>
				</ul>
			</div>

			<div class="nav-column">
				<h4 class="nav-heading">Legal</h4>
				<ul class="nav-list">
					<li><a href="/privacy">Privacy Policy</a></li>
					<li><a href="/terms">Terms of Service</a></li>
					<li><a href="/license">License</a></li>
					<li><a href="/contact">Contact</a></li>
				</ul>
			</div>
		</nav>

		<!-- Divider -->
		<div class="footer-divider"></div>

		<!-- Bottom Section -->
		<div class="footer-bottom">
			<div class="footer-brand">
				<img src={lunorbisLogo} alt="Lunorbis Logo" class="footer-logo" />
				<div class="brand-text">
					<h3 class="brand-title">LUNORBIS</h3>
					<p class="brand-subtitle">High-Performance Bedrock Server Runtime</p>
				</div>
			</div>

			<div class="footer-actions">
				<DiscordButton href={discordUrl} label="Join Community" size="small" />
			</div>

			<div class="footer-meta">
				<p class="copyright">
					&copy; 2024 Lunorbis. All rights reserved.
				</p>
				<p class="tagline">Powering the next generation of Minecraft Bedrock servers.</p>
			</div>
		</div>
	</div>
</footer>

<style>
	:root {
		--accent: #00ffcf;
		--accent-rgb: 0, 255, 207;
		--bg-deep: #050606;
	}

	.footer {
		position: relative;
		background: linear-gradient(180deg, rgba(255, 255, 255, 0.02), rgba(255, 255, 255, 0.01));
		backdrop-filter: blur(10px);
		-webkit-backdrop-filter: blur(10px);
		border-top: 1px solid rgba(255, 255, 255, 0.1);
		padding: 3rem 1rem;
		margin-top: 5rem;
	}

	.footer-content {
		max-width: 1400px;
		margin: 0 auto;
	}

	.footer-nav {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
		gap: 3rem;
		margin-bottom: 3rem;
	}

	.nav-column {
		display: flex;
		flex-direction: column;
		gap: 1rem;
	}

	.nav-heading {
		margin: 0;
		color: var(--accent);
		font-size: 0.95rem;
		letter-spacing: 1px;
		text-transform: uppercase;
	}

	.nav-list {
		list-style: none;
		margin: 0;
		padding: 0;
		display: flex;
		flex-direction: column;
		gap: 0.6rem;
	}

	.nav-list a {
		color: #999;
		text-decoration: none;
		font-size: 0.85rem;
		transition: color 0.2s ease, text-shadow 0.2s ease;
	}

	.nav-list a:hover {
		color: var(--accent);
		text-shadow: 0 0 10px rgba(var(--accent-rgb), 0.4);
	}

	.footer-divider {
		height: 1px;
		background: linear-gradient(
			90deg,
			transparent,
			rgba(255, 255, 255, 0.1) 20%,
			rgba(255, 255, 255, 0.1) 80%,
			transparent
		);
		margin: 2rem 0;
	}

	.footer-bottom {
		display: flex;
		flex-direction: column;
		gap: 2rem;
		align-items: center;
		text-align: center;
	}

	.footer-brand {
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 1rem;
	}

	.footer-logo {
		width: 60px;
		height: 60px;
		filter: drop-shadow(0 0 15px rgba(0, 255, 207, 0.2));
	}

	.brand-text {
		display: flex;
		flex-direction: column;
		gap: 0.25rem;
	}

	.brand-title {
		margin: 0;
		color: var(--accent);
		font-size: 1.2rem;
		letter-spacing: 2px;
	}

	.brand-subtitle {
		margin: 0;
		color: #666;
		font-size: 0.85rem;
		letter-spacing: 0.5px;
	}

	.footer-actions {
		display: flex;
		justify-content: center;
		gap: 1rem;
	}

	.footer-meta {
		display: flex;
		flex-direction: column;
		gap: 0.5rem;
	}

	.copyright {
		margin: 0;
		color: #666;
		font-size: 0.8rem;
	}

	.tagline {
		margin: 0;
		color: #555;
		font-size: 0.75rem;
		letter-spacing: 0.5px;
	}

	@media (max-width: 768px) {
		.footer {
			padding: 2rem 1rem;
			margin-top: 3rem;
		}

		.footer-nav {
			grid-template-columns: repeat(2, 1fr);
			gap: 2rem;
		}

		.nav-heading {
			font-size: 0.85rem;
		}

		.nav-list a {
			font-size: 0.8rem;
		}

		.footer-bottom {
			gap: 1.5rem;
		}

		.footer-logo {
			width: 50px;
			height: 50px;
		}

		.brand-title {
			font-size: 1rem;
		}

		.brand-subtitle {
			font-size: 0.75rem;
		}
	}

	@media (max-width: 480px) {
		.footer-nav {
			grid-template-columns: 1fr;
			gap: 1.5rem;
		}
	}
</style>
