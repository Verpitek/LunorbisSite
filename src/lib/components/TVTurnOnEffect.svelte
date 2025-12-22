<script lang="ts">
	import { onMount } from 'svelte';
	import { isInitialLoad } from '$lib/stores';

	let showEffect = false;

	onMount(() => {
		// Only show effect on initial page load
		if ($isInitialLoad) {
			showEffect = true;
			isInitialLoad.set(false);

			// Remove effect after animation completes
			const timer = setTimeout(() => {
				showEffect = false;
			}, 2500);

			return () => clearTimeout(timer);
		}
	});
</script>

{#if showEffect}
	<div class="tv-effect-wrapper">
		<!-- CRT scan lines going down -->
		<div class="tv-scanlines"></div>

		<!-- Black curtain from top -->
		<div class="tv-curtain tv-curtain-top"></div>

		<!-- Black curtain from bottom -->
		<div class="tv-curtain tv-curtain-bottom"></div>

		<!-- Power-on glow flash -->
		<div class="tv-power-flash"></div>

		<!-- Static noise (optional) -->
		<div class="tv-static"></div>
	</div>
{/if}

<style>
	.tv-effect-wrapper {
		position: fixed;
		inset: 0;
		z-index: 9999;
		pointer-events: none;
		overflow: hidden;
	}

	/* Scan lines that sweep down from top */
	.tv-scanlines {
		position: absolute;
		top: -100%;
		left: 0;
		width: 100%;
		height: 60px;
		background: repeating-linear-gradient(
			to bottom,
			rgba(255, 255, 255, 0.15) 0px,
			rgba(255, 255, 255, 0.15) 2px,
			rgba(0, 0, 0, 0.4) 2px,
			rgba(0, 0, 0, 0.4) 4px
		);
		box-shadow: 0 0 30px rgba(255, 255, 255, 0.3), 0 0 60px rgba(0, 255, 207, 0.2);
		animation: tv-scanline-sweep 1.2s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
	}

	/* Curtains closing from top and bottom */
	.tv-curtain {
		position: absolute;
		left: 0;
		width: 100%;
		background: #000;
		animation-duration: 0.8s;
		animation-timing-function: cubic-bezier(0.34, 1.56, 0.64, 1);
		animation-fill-mode: forwards;
	}

	.tv-curtain-top {
		top: 0;
		height: 0;
		animation-name: tv-curtain-down;
	}

	.tv-curtain-bottom {
		bottom: 0;
		height: 0;
		animation-name: tv-curtain-up;
	}

	/* Power on glow */
	.tv-power-flash {
		position: absolute;
		inset: 0;
		background: radial-gradient(
			circle at center,
			rgba(0, 255, 207, 0.5) 0%,
			rgba(0, 255, 207, 0.2) 30%,
			transparent 70%
		);
		animation: tv-power-flash 0.6s ease-out forwards;
		animation-delay: 0.3s;
	}

	/* Static noise effect */
	.tv-static {
		position: absolute;
		inset: 0;
		background-image: url("data:image/svg+xml,%3Csvg width='100' height='100' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' /%3E%3C/filter%3E%3Crect width='100' height='100' fill='white' filter='url(%23noise)' opacity='0.3'/%3E%3C/svg%3E");
		background-size: 100px 100px;
		opacity: 0;
		animation: tv-static-fade 0.8s ease-out forwards;
		animation-delay: 0.2s;
	}

	/* --- ANIMATIONS --- */

	@keyframes tv-scanline-sweep {
		from {
			top: -100%;
		}
		to {
			top: 100%;
		}
	}

	@keyframes tv-curtain-down {
		from {
			height: 50%;
		}
		to {
			height: 0;
		}
	}

	@keyframes tv-curtain-up {
		from {
			height: 50%;
		}
		to {
			height: 0;
		}
	}

	@keyframes tv-power-flash {
		0% {
			opacity: 1;
		}
		100% {
			opacity: 0;
		}
	}

	@keyframes tv-static-fade {
		0% {
			opacity: 0.6;
		}
		100% {
			opacity: 0;
		}
	}
</style>
