<script lang="ts">
	import TypeWriter from './TypeWriter.svelte';
	
	export let title: string = '';
	export let icon: string = '';
	export let iconType: 'text' | 'image' = 'text';
	export let isGlassmorphic: boolean = false;
	export let enableTypeWriter: boolean = true;
</script>

<div class="description-block" class:glassmorphic={isGlassmorphic}>
	<div class="content-pane" class:glass={isGlassmorphic}>
		<div class="reflection-glint" class:hidden={!isGlassmorphic}></div>

		<div class="content-inner">
			{#if icon}
				<div class="icon-container">
					{#if iconType === 'image'}
						<img src={icon} alt={title} class="icon-image" />
					{:else}
						<span class="icon-text">{icon}</span>
					{/if}
				</div>
			{/if}

		{#if title}
			<h3 class="block-title">
				{#if enableTypeWriter}
					<TypeWriter text={title} speed={50} delay={200} showCursor={false} />
				{:else}
					{title}
				{/if}
			</h3>
		{/if}

		<div class="content-text">
			<slot />
		</div>
		</div>
	</div>
</div>

<style>
	:root {
		--accent: #00ffcf;
		--accent-rgb: 0, 255, 207;
	}

	.description-block {
		position: relative;
		width: 100%;
		height: 100%;
	}

	.content-pane {
		position: relative;
		background: rgba(255, 255, 255, 0.03);
		border-top: 2px solid rgba(255, 255, 255, 0.2);
		border-left: 2px solid rgba(255, 255, 255, 0.15);
		border-right: 1px solid rgba(0, 0, 0, 0.3);
		border-bottom: 1px solid rgba(0, 0, 0, 0.4);
		border-radius: 20px;
		padding: 2.5rem 2rem;
		overflow: hidden;
		box-shadow:
			0 20px 50px rgba(0, 0, 0, 0.6),
			inset 0 0 30px rgba(255, 255, 255, 0.02);
		transition: all 0.3s ease;
		height: 100%;
		display: flex;
		flex-direction: column;
	}

	.content-pane.glass {
		background: rgba(255, 255, 255, 0.03);
		backdrop-filter: blur(35px) saturate(200%) contrast(90%);
		-webkit-backdrop-filter: blur(35px) saturate(200%);
	}

	.description-block:not(.glassmorphic) .content-pane {
		background: rgba(60, 60, 70, 0.4);
		border: 1px solid rgba(255, 255, 255, 0.1);
		backdrop-filter: none;
		-webkit-backdrop-filter: none;
	}

	.content-pane:hover {
		background: rgba(255, 255, 255, 0.05);
		box-shadow:
			0 30px 70px rgba(0, 0, 0, 0.7),
			inset 0 0 40px rgba(255, 255, 255, 0.03),
			0 0 30px rgba(0, 255, 207, 0.1);
	}

	.description-block:not(.glassmorphic) .content-pane:hover {
		background: rgba(70, 70, 80, 0.5);
		box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5);
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

	.reflection-glint.hidden {
		display: none;
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

	.content-inner {
		position: relative;
		z-index: 2;
		display: flex;
		flex-direction: column;
		gap: 1rem;
		flex: 1;
	}

	.icon-container {
		display: flex;
		justify-content: center;
		margin-bottom: 0.5rem;
	}

	.icon-text {
		font-size: 2.5rem;
		color: var(--accent);
		text-shadow: 0 0 15px rgba(var(--accent-rgb), 0.6);
		display: inline-block;
	}

	.icon-image {
		width: 60px;
		height: 60px;
		object-fit: contain;
	}

	.block-title {
		margin: 0;
		color: var(--accent);
		font-size: 1.5rem;
		letter-spacing: 2px;
		text-align: center;
	}

	.content-text {
		color: #aaa;
		font-size: 0.95rem;
		line-height: 1.6;
		text-align: center;
	}

	@media (max-width: 768px) {
		.content-pane {
			padding: 1.5rem;
			border-radius: 15px;
		}

		.icon-text {
			font-size: 2rem;
		}

		.icon-image {
			width: 50px;
			height: 50px;
		}

		.block-title {
			font-size: 1.25rem;
			letter-spacing: 1px;
		}

		.content-text {
			font-size: 0.9rem;
		}
	}
</style>
