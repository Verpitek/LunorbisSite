<script lang="ts">
	export let count: number = 50;

	let matrixChars = '01';
	const trailSegments = 10;

	function getRandom(min: number, max: number) {
		return Math.random() * (max - min) + min;
	}

	function generateSnakeHead() {
		return {
			startX: getRandom(0, 100),
			startY: getRandom(0, 100),
			moveX: getRandom(-40, 40),
			moveY: getRandom(-40, 40),
			duration: getRandom(15, 25),
			delay: getRandom(-20, 0),
			scale: getRandom(0.7, 1.1),
			rotation: getRandom(90, 360),
			opacity: getRandom(0.2, 0.4),
			char:
				Math.random() < 0.05
					? '2'
					: matrixChars[Math.floor(Math.random() * matrixChars.length)]
		};
	}
</script>

<div class="matrix-background">
	{#each Array(count) as _, i (i)}
		{@const head = generateSnakeHead()}
		<div class="snake-group">
			{#each Array(trailSegments) as _, j}
				<div
					class="matrix-char"
					style="
						left: {head.startX}%;
						top: {head.startY}%;
						--move-x: {head.moveX}vw;
						--move-y: {head.moveY}vh;
						--rot: {head.rotation}deg;
						--dur: {head.duration}s;
						--del: {head.delay - j * 0.12}s;
						--op: {head.opacity * (1 - j / trailSegments)};
						--sc: {head.scale * (1 - j / (trailSegments * 2))};
					"
				>
					{head.char}
				</div>
			{/each}
		</div>
	{/each}
</div>

<style>
	:root {
		--accent: #00ffcf;
		--accent-rgb: 0, 255, 207;
	}

	.matrix-background {
		position: fixed;
		inset: 0;
		z-index: 1;
		pointer-events: none;
	}

	.matrix-char {
		position: absolute;
		color: var(--accent);
		font-size: 1.5rem;
		opacity: 0;
		animation: snake-follow var(--dur) linear infinite;
		animation-delay: var(--del);
		text-shadow: 0 0 8px rgba(var(--accent-rgb), 0.5);
	}

	@keyframes snake-follow {
		0% {
			transform: translate(0, 0) rotate(0deg) scale(var(--sc));
			opacity: 0;
		}
		10% {
			opacity: var(--op);
		}
		90% {
			opacity: var(--op);
		}
		100% {
			transform: translate(var(--move-x), var(--move-y)) rotate(var(--rot))
				scale(var(--sc));
			opacity: 0;
		}
	}
</style>
