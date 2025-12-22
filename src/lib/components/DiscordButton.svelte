<script lang="ts">
	export let href: string = 'https://discord.gg/';
	export let label: string = 'Join Discord';
	export let size: 'small' | 'medium' | 'large' = 'medium';
</script>

<a {href} target="_blank" rel="noopener noreferrer" class="discord-button" class:size>
	<svg
		xmlns="http://www.w3.org/2000/svg"
		viewBox="0 0 127.14 96.36"
		class="discord-icon"
	>
		<path
			fill="currentColor"
			d="M107.7,8.07A105.15,105.15,0,0,0,81.47,0a72.06,72.06,0,0,0-3.36,6.83A99.89,99.89,0,0,0,49,6.83,72.37,72.37,0,0,0,45.64,0A105.89,105.89,0,0,0,19.39,8.09C2.79,32.65-1.71,56.6.54,80.21h0A105.73,105.73,0,0,0,32.71,96.36,77.7,77.7,0,0,0,39.6,85.25a68.42,68.42,0,0,1-10.85-5.18c.91-.66,1.8-1.34,2.66-2a77.15,77.15,0,0,0,64.32,0c.87.71,1.76,1.39,2.66,2a68.68,68.68,0,0,1-10.87,5.19,77,77,0,0,0,6.89,11.1A105.25,105.25,0,0,0,126.6,80.22h0C129.24,52.84,122.09,29.11,107.7,8.07ZM42.45,65.69C36.18,65.69,31,60.55,31,53.88s5-11.75,11.45-11.75S54,47.16,53.89,53.88,48.84,65.69,42.45,65.69Zm42.24,0C78.41,65.69,73.25,60.55,73.25,53.88s5-11.75,11.45-11.75S96.19,47.16,96.12,53.88,91.13,65.69,84.69,65.69Z"
		/>
	</svg>
	<span class="label">{label}</span>
</a>

<style>
	:root {
		--accent: #00ffcf;
		--accent-rgb: 0, 255, 207;
	}

	.discord-button {
		display: inline-flex;
		align-items: center;
		gap: 0.75rem;
		padding: 0.9rem 1.8rem;
		background: linear-gradient(135deg, rgba(88, 101, 242, 0.15), rgba(88, 101, 242, 0.05));
		border: 1.5px solid rgba(88, 101, 242, 0.4);
		border-radius: 25px;
		color: #fff;
		text-decoration: none;
		font-family: 'Monocraft', monospace;
		font-size: 1rem;
		font-weight: bold;
		cursor: pointer;
		transition: all 0.3s ease;
		box-shadow: 0 0 20px rgba(88, 101, 242, 0.1);
		letter-spacing: 0.5px;
	}

	.discord-button:hover {
		background: linear-gradient(135deg, rgba(88, 101, 242, 0.25), rgba(88, 101, 242, 0.15));
		border-color: rgba(88, 101, 242, 0.6);
		box-shadow:
			0 0 30px rgba(88, 101, 242, 0.3),
			0 0 50px rgba(88, 101, 242, 0.15);
		transform: translateY(-2px);
	}

	.discord-button:active {
		transform: translateY(0);
	}

	.discord-icon {
		width: 1.2rem;
		height: 1.2rem;
		color: #5865f2;
		transition: filter 0.3s ease;
	}

	.discord-button:hover .discord-icon {
		filter: drop-shadow(0 0 8px rgba(88, 101, 242, 0.6));
	}

	.label {
		display: inline;
	}

	/* Size variants */
	:global(.size.small) {
		padding: 0.6rem 1.2rem;
		font-size: 0.9rem;
	}

	:global(.size.small) .discord-icon {
		width: 1rem;
		height: 1rem;
	}

	:global(.size.large) {
		padding: 1.2rem 2.5rem;
		font-size: 1.2rem;
	}

	:global(.size.large) .discord-icon {
		width: 1.5rem;
		height: 1.5rem;
	}

	@media (max-width: 768px) {
		.discord-button {
			padding: 0.8rem 1.5rem;
			font-size: 0.95rem;
		}

		.discord-icon {
			width: 1.1rem;
			height: 1.1rem;
		}
	}
</style>
