<script lang="ts">
	export let title: string = '';
	export let icon: string = '';
	export let isHighlight: boolean = false;
</script>

<div class="information-block" class:highlight={isHighlight}>
	<div class="glass-pane">
		<div class="reflection-glint"></div>

		<div class="glass-content">
			{#if icon}
				<div class="icon-container">
					<span class="icon">{icon}</span>
				</div>
			{/if}

			{#if title}
				<h3 class="info-title">{title}</h3>
			{/if}

			<div class="info-content">
				<slot />
			</div>
		</div>
	</div>
</div>

<style>
	:root {
		--accent: #00ffcf;
		--accent-rgb: 0, 255, 207;
		--minecraft-yellow: #ffff00;
	}

	.information-block {
		position: relative;
		width: 100%;
		height: 100%;
	}

	.glass-pane {
		position: relative;
		background: rgba(255, 255, 255, 0.03);
		backdrop-filter: blur(35px) saturate(200%) contrast(90%);
		-webkit-backdrop-filter: blur(35px) saturate(200%);
		border-top: 2px solid rgba(255, 255, 255, 0.2);
		border-left: 2px solid rgba(255, 255, 255, 0.15);
		border-right: 1px solid rgba(0, 0, 0, 0.3);
		border-bottom: 1px solid rgba(0, 0, 0, 0.4);
		border-radius: 20px;
		padding: 2rem;
		overflow: hidden;
		box-shadow:
			0 20px 50px rgba(0, 0, 0, 0.6),
			inset 0 0 30px rgba(255, 255, 255, 0.02);
		transition: all 0.3s ease;
		height: 100%;
		display: flex;
		flex-direction: column;
	}

	.glass-pane:hover {
		background: rgba(255, 255, 255, 0.05);
		box-shadow:
			0 30px 70px rgba(0, 0, 0, 0.7),
			inset 0 0 40px rgba(255, 255, 255, 0.03),
			0 0 30px rgba(0, 255, 207, 0.1);
	}

	.highlight .glass-pane {
		background: rgba(255, 255, 0, 0.02);
		border-top: 2px solid rgba(255, 255, 0, 0.3);
		border-left: 2px solid rgba(255, 255, 0, 0.25);
		box-shadow:
			0 20px 50px rgba(0, 0, 0, 0.6),
			inset 0 0 30px rgba(255, 255, 0, 0.02),
			0 0 20px rgba(255, 255, 0, 0.15);
	}

	.highlight .glass-pane:hover {
		box-shadow:
			0 30px 70px rgba(0, 0, 0, 0.7),
			inset 0 0 40px rgba(255, 255, 0, 0.03),
			0 0 40px rgba(255, 255, 0, 0.25);
	}

	.highlight .icon {
		color: var(--minecraft-yellow);
		text-shadow: 0 0 15px rgba(255, 255, 0, 0.6);
	}

	.highlight .info-title {
		color: var(--minecraft-yellow);
	}

	.reflection-glint {
		position: absolute;
		top: 0;
		left: -150%;
		width: 100%;
		height: 100%;
		background: linear-gradient(
			90deg,
			transparent,
			rgba(255, 255, 255, 0.05) 45%,
			rgba(255, 255, 255, 0.12) 50%,
			rgba(255, 255, 255, 0.05) 55%,
			transparent
		);
		transform: skewX(-25deg);
		animation: glint-sweep 8s ease-in-out infinite;
		pointer-events: none;
	}

	@keyframes glint-sweep {
		0% {
			left: -150%;
		}
		20% {
			left: 150%;
		}
		100% {
			left: 150%;
		}
	}

	.glass-content {
		position: relative;
		z-index: 2;
		display: flex;
		flex-direction: column;
		gap: 0.8rem;
		flex: 1;
	}

	.icon-container {
		display: flex;
		justify-content: center;
		margin-bottom: 0.25rem;
	}

	.icon {
		font-size: 2.2rem;
		color: var(--accent);
		text-shadow: 0 0 15px rgba(var(--accent-rgb), 0.6);
		display: inline-block;
	}

	.info-title {
		margin: 0;
		color: var(--accent);
		font-size: 1.25rem;
		letter-spacing: 1px;
		text-align: center;
	}

	.info-content {
		color: #999;
		font-size: 0.9rem;
		line-height: 1.5;
		text-align: center;
	}

	@media (max-width: 768px) {
		.glass-pane {
			padding: 1.25rem;
			border-radius: 15px;
		}

		.icon {
			font-size: 1.8rem;
		}

		.info-title {
			font-size: 1.1rem;
			letter-spacing: 0.5px;
		}

		.info-content {
			font-size: 0.85rem;
		}
	}
</style>
