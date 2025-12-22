<script lang="ts">
	import './layout.css';
	import lunorbisLogo from '$lib/assets/lunorbis.svg';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={lunorbisLogo} />
	<title>Lunorbis - High-Performance Minecraft Bedrock Server Runtime</title>
	<meta name="description" content="Lunorbis replaces QuickJS with V8 runtime for Minecraft Bedrock Servers, providing JIT compilation, filesystem access, and external networking." />
</svelte:head>

<main class="layout-main">
	{@render children()}
</main>
