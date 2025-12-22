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

			const angle = (i / 12) * Math.PI * 2;
			const velocity = 3 + Math.random() * 4;
			const vx = Math.cos(angle) * velocity;
			const vy = Math.sin(angle) * velocity;
			const distance = 150 + Math.random() * 100;
			const duration = 0.6 + Math.random() * 0.4;
			const rotX = (Math.random() - 0.5) * 720;
			const rotY = (Math.random() - 0.5) * 720;
			const rotZ = (Math.random() - 0.5) * 720;

			particle.style.setProperty('--vx', String(vx));
			particle.style.setProperty('--vy', String(vy));
			particle.style.setProperty('--distance', String(distance));
			particle.style.setProperty('--duration', `${duration}s`);
			particle.style.setProperty('--rotX', `${rotX}deg`);
			particle.style.setProperty('--rotY', `${rotY}deg`);
			particle.style.setProperty('--rotZ', `${rotZ}deg`);
			particle.style.left = x + 'px';
			particle.style.top = y + 'px';

			document.body.appendChild(particle);

			setTimeout(() => particle.remove(), duration * 1000);
		}
	}

	if (typeof window !== 'undefined') {
		window.addEventListener('click', createParticleBurst);
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
