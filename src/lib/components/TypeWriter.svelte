<script lang="ts">
	import { onMount } from 'svelte';

	export let text: string = '';
	export let speed: number = 50; // milliseconds per character
	export let delay: number = 0; // delay before starting animation
	export let showCursor: boolean = true;

	let displayedText = '';
	let isAnimating = true;

	onMount(() => {
		let currentIndex = 0;
		let timeoutId: NodeJS.Timeout;

		const animate = () => {
			if (currentIndex <= text.length) {
				displayedText = text.slice(0, currentIndex);
				currentIndex++;
				timeoutId = setTimeout(animate, speed);
			} else {
				isAnimating = false;
			}
		};

		const startAnimation = setTimeout(() => {
			animate();
		}, delay);

		return () => {
			clearTimeout(startAnimation);
			clearTimeout(timeoutId);
		};
	});
</script>

<span class="typewriter" class:animating={isAnimating}>
	{displayedText}
	{#if showCursor && isAnimating}
		<span class="cursor">▌</span>
	{/if}
</span>

<style>
	.typewriter {
		display: inline;
		font-family: 'Monocraft', monospace;
	}

	.cursor {
		animation: blink 1s infinite;
		color: inherit;
		margin-left: 2px;
	}

	@keyframes blink {
		0%,
		49% {
			opacity: 1;
		}
		50%,
		100% {
			opacity: 0;
		}
	}
</style>
