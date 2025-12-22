<script lang="ts">
	import './layout.css';
	import lunorbisLogo from '$lib/assets/lunorbis.svg';
	import Navbar from '$lib/components/Navbar.svelte';

	let { children } = $props();

	function createParticleBurst(e: MouseEvent) {
		const x = e.clientX;
		const y = e.clientY;

		for (let i = 0; i < 12; i++) {
			const particle = document.createElement('div');
			particle.className = 'particle';
			particle.textContent = Math.random() > 0.5 ? '0' : '1';

			const angle = (i / 12) * Math.PI * 2 + (Math.random() - 0.5) * 0.5;
			const velocity = 4 + Math.random() * 6;
			const vx = Math.cos(angle) * velocity;
			const vy = Math.sin(angle) * velocity;
			const distance = 200 + Math.random() * 150;
			const duration = 0.8 + Math.random() * 0.6;
			const rotX = (Math.random() - 0.5) * 1080;
			const rotY = (Math.random() - 0.5) * 1080;
			const rotZ = (Math.random() - 0.5) * 1080;

			particle.style.setProperty('--vx', String(vx));
			particle.style.setProperty('--vy', String(vy));
			particle.style.setProperty('--distance', String(distance));
			particle.style.setProperty('--duration', `${duration}s`);
			particle.style.setProperty('--rotX', `${rotX}deg`);
			particle.style.setProperty('--rotY', `${rotY}deg`);
			particle.style.setProperty('--rotZ', `${rotZ}deg`);
			particle.style.left = x + 'px';
			particle.style.top = y + 'px';
			particle.style.pointerEvents = 'none';

			document.body.appendChild(particle);

			setTimeout(() => particle.remove(), duration * 1000);
		}
	}

	if (typeof window !== 'undefined') {
		window.addEventListener('mousedown', createParticleBurst);
	}
</script>

<svelte:head>
	<link rel="icon" href={lunorbisLogo} />
	<title>Lunorbis - High-Performance Minecraft Bedrock Server Runtime</title>
	<meta name="description" content="Lunorbis replaces QuickJS with V8 runtime for Minecraft Bedrock Servers, providing JIT compilation, filesystem access, and external networking." />
</svelte:head>

<Navbar />
<main class="layout-main">
	{@render children()}
</main>
