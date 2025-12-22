<script lang="ts">
  import { onMount } from 'svelte';

  // State: 'wait' -> 'dot' -> 'line' -> 'open' -> 'gone'
  let phase = 'wait';
  let isAlive = true;

  onMount(() => {
    setTimeout(() => phase = 'dot', 100);
    setTimeout(() => phase = 'line', 500);
    setTimeout(() => phase = 'open', 1100);
    // Remove from DOM entirely so it doesn't interfere with your site
    setTimeout(() => isAlive = false, 2500);
  });
</script>

{#if isAlive}
  <div class="crt-overlay {phase}">
    
    <div class="block top">
      <div class="edge"></div>
    </div>

    {#if phase === 'dot' || phase === 'line'}
      <div class="beam {phase}"></div>
    {/if}

    <div class="block bottom">
      <div class="edge"></div>
    </div>

    <div class="scanlines"></div>
  </div>
{/if}

<style>
  :root {
    --accent: #00ffcf;
  }

  .crt-overlay {
    position: fixed;
    inset: 0;
    z-index: 9999999;
    display: flex;
    flex-direction: column;
    pointer-events: none;
    overflow: hidden;
    background: transparent;
  }

  /* --- THE BLOCKS --- */
  .block {
    flex: 1;
    background: #000;
    position: relative;
    z-index: 10;
    /* High-torque mechanical easing */
    transition: transform 0.8s cubic-bezier(0.8, 0, 0.2, 1);
  }

  /* Movement: Opera Opening */
  .open .block.top { transform: translateY(-100%); }
  .open .block.bottom { transform: translateY(100%); }

  /* --- THE BEAM --- */
  .beam {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background: #fff;
    box-shadow: 
      0 0 10px #fff, 
      0 0 30px var(--accent), 
      0 0 60px var(--accent);
    z-index: 20;
    transition: all 0.3s ease-in-out;
  }

  .beam.dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
  }

  .beam.line {
    width: 100vw;
    height: 2px;
    border-radius: 0;
  }

  /* --- THE GLOWING EDGES --- */
  .edge {
    position: absolute;
    left: 0;
    width: 100%;
    height: 2px;
    background: var(--accent);
    box-shadow: 0 0 15px var(--accent);
    opacity: 0;
    transition: opacity 0.2s;
  }

  .block.top .edge { bottom: 0; }
  .block.bottom .edge { top: 0; }

  /* Show the glow edge as soon as the curtains start moving */
  .open .edge { opacity: 1; }

  /* --- TEXTURE --- */
  .scanlines {
    position: absolute;
    inset: 0;
    z-index: 30;
    background: linear-gradient(
      rgba(18, 16, 16, 0) 50%, 
      rgba(0, 0, 0, 0.2) 50%
    );
    background-size: 100% 4px;
    opacity: 0.4;
  }
</style>