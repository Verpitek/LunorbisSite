<script lang="ts">
    import { onMount } from "svelte";
    import lunorbisLogo from "$lib/assets/lunorbis.svg";
    import MatrixBackground from "$lib/components/MatrixBackground.svelte";
    import Glass from "$lib/components/Glass.svelte";

    let currentQuote = "";
    let currentBlockIndex = 0;

    const blocks = [
        {
            title: "LUNORBIS",
            subtitle: "High-Performance Bedrock Server Runtime",
            buttonPrimary: "Install Now!",
            buttonSecondary: "Docs"
        },
        {
            title: "FEATURES",
            subtitle: "Lightning-fast performance and stability",
            buttonPrimary: "Learn More",
            buttonSecondary: "API Docs"
        },
        {
            title: "COMMUNITY",
            subtitle: "Join thousands of developers",
            buttonPrimary: "Join Now",
            buttonSecondary: "Discord"
        }
    ];

    const quotes = [
        // JavaScript Classics
        "Undefined is not a function!",
        "V8 goes BRRRRRR",
        "Now with 50% more [object Object]",
        "0.1 + 0.2 === 0.30000000000000004",
        "It works on my machine!",
        "Successfully ignored 1,429 warnings",
        "Wait, where did the heap go?",
        "Garbage Collection is my only friend",
        "Compiling... still compiling...",
        "Is it a feature or a bug? Yes.",
        "Moving the bug to the documentation",
        "Null is my favorite value",
        "Optimized for 1 FPS (if you try hard)",
        "JIT: Just In Time (to crash)",
        "V8 Runtime: Because QuickJS was too slow for my cat",
        "JSON is my love language.",
        "System.ready(but-not-really)",

        // More JavaScript Quirks
        "typeof NaN === 'number'... true!",
        "[] + {} = '[object Object]'",
        "{} + [] = 0",
        "undefined == null (but not ===)",
        "var hoisting: the silent killer",
        "async/await: now with more promise!",
        "Callback hell? More like pyramid of doom!",
        "Promises, promises, promises...",
        "Closure: I don't know what I expected",
        "this is undefined (in strict mode)",
        "NaN is the loneliest number",
        "Infinity > 999999999999999999999",
        "parseInt('10', 2) = 2 (not 10!)",
        "'5' + 3 = '53' (string wins!)",
        "try { } finally { always runs }",
        "Prototypal inheritance? More like prototype chain confusion!",
        "WeakMap: existence is hard to detect",
        "Symbol: the misunderstood primitive",
        "Proxy: meta-programming made confusing",
        "Reflect: reflection for the confused",
        "Generator functions: pause my execution please!",
        "Destructuring: elegance meets confusion",
        "Spread operator: three dots of power",
        "Template literals: finally, string interpolation!",
        "Arrow functions: no 'this' binding drama",
        "Object.freeze(): I'm immutable now!",
        "Const: not really constant",
        "Let: block scope for the win",
        "Minceraft!",
        "90% Bug Free!",
        "Does contain peanuts!",
        "Technoblade never dies!",
        "Also try Paper!",
        "Also try Endstone!",
        "Also try Spigot!",
        "Also try Geyser!",
        "Designed by people who for some reason decided to fight for this game :P",
        ":3c",
        "Also try LeviLamina!",
        "Words cannot describe how silly the devs are :3",
        "Something something java something something bedrock bad",
        "Nukkit is pronounced NukeIt, not Nukkit (im loosing my mind)",
        "Also try PNX!",
        "Yeah uhh dont try the vanilla BDS...",
        "Also try Terraria!",
        "Splash text #241!",
        "Slightly better than dirt!",
        "Follow the train, CJ!",
        "100% pure software!",
        "Don't tell my mom!",
        "Creeper, aw man!",
        "Don't dig straight down!",
        "Diamonds found! (Nevermind, it's lapis)",
        "Pigs can fly!",
        "Ouch! That hurt.",
        "Herobrine was here.",
        "You cannot sleep now, monsters are nearby.",
        "Hrmmm... (Villager noises)",
        "3 Emeralds for 1 Piece of Dirt? Deal!",
        "Wandering Trader? More like Free Leads.",
        "Punching wood for a living.",
        "MLG Water Bucket (failed)!",
        "Enderman says hi.",
        "Steve is looking at you.",
        "Inventory full! Throwing out diamonds...",
        "Wait, where did I put my base?",
        "Bypassing the limits!",
        "Bye-bye Scripting lag!",
        "The Bedrock Revolution",
        "Tick speed: LIGHTSPEED.",
        "Data-driven everything!",
        "Parsed in record time.",
        "Maximum entity counts!",
        "Add-ons on steroids!",
        "Wait, why is the sky purple?",
        "Updating 1 block... updating the whole world.",
        "Performance is our middle name!",
        "Render distance: how far can you see?",
        "Cross-platform chaos!",
        "100% no hacking, I promise!",
        "setTimeout(() => setImmediate(() => Promise.resolve()))!",
        "Event loop: one callback to rule them all!",
        "Memoization: remember what I did!",
        "Currying: function partial application!",
        "Composition: function upon function!",
        "Pure functions: no side effects allowed!",
        "Immutability: Object.freeze() the world!",
        "Functional programming in JavaScript!",
        "Monads: just monads... trust me!",
        "Optional chaining: ?.?.?",
        "Nullish coalescing: ?? solves everything!",
        "BigInt: numbers bigger than numbers!",
        "Regex: write once, understand never!",
    ];

    let glassPane: HTMLElement | null = null;
    let rotateX = 0;
    let rotateY = 0;

    const nextBlock = () => {
        currentBlockIndex = (currentBlockIndex + 1) % blocks.length;
    };

    const prevBlock = () => {
        currentBlockIndex = (currentBlockIndex - 1 + blocks.length) % blocks.length;
    };

    onMount(() => {
        currentQuote = quotes[Math.floor(Math.random() * quotes.length)];
        
        glassPane = document.querySelector('.glass-pane');
        if (!glassPane) return;

        const handleMouseMove = (e: MouseEvent) => {
            if (!glassPane) return;
            const rect = glassPane.getBoundingClientRect();
            const centerX = rect.left + rect.width / 2;
            const centerY = rect.top + rect.height / 2;
            
            const distX = (e.clientX - centerX) / (rect.width / 2);
            const distY = (e.clientY - centerY) / (rect.height / 2);
            
            rotateX = Math.max(-1, Math.min(1, distY)) * 8;
            rotateY = Math.max(-1, Math.min(1, distX)) * -8;
        };

        const handleMouseLeave = () => {
            rotateX = 0;
            rotateY = 0;
        };

        window.addEventListener('mousemove', handleMouseMove);
        glassPane.addEventListener('mouseleave', handleMouseLeave);

        return () => {
            window.removeEventListener('mousemove', handleMouseMove);
            glassPane?.removeEventListener('mouseleave', handleMouseLeave);
        };
    });
</script>

<div class="page terminal-theme">
    <div class="moving-stripes"></div>
    <div class="crt-vignette"></div>
    <div class="scanlines"></div>

    <MatrixBackground count={25} />

    <section class="hero carousel-section" data-collision-box>
        <div class="carousel-container">
            {#each blocks as block, index (index)}
                <div class="carousel-block" class:active={index === currentBlockIndex}>
                    <div class="glass-pane" style="transform: perspective(1200px) rotateX({index === currentBlockIndex ? rotateX : 0}deg) rotateY({index === currentBlockIndex ? rotateY : 0}deg); transition: transform 0.1s ease-out;">
                        <Glass />
                        
                        <div class="prism-edge"></div>
        
                        <div class="glass-content">
                            <div class="logo-container">
                                <img src={lunorbisLogo} alt="Logo" class="logo" />
                            </div>
        
                            <div class="title-wrapper">
                                <h1 class="hero-title">{block.title}</h1>
                                {#if currentQuote && index === 0}
                                    <div class="splash-text">{currentQuote}</div>
                                {/if}
                            </div>
        
                            <p class="hero-subtitle">{block.subtitle}</p>
        
                            <div class="cta-buttons">
                                <button class="cta-primary">{block.buttonPrimary}</button>
                                <button class="cta-secondary">{block.buttonSecondary}</button>
                            </div>
                        </div>
                    </div>
                </div>
            {/each}
        </div>

        <!-- Carousel Navigation -->
        <button class="carousel-nav carousel-prev" on:click={prevBlock}>←</button>
        <button class="carousel-nav carousel-next" on:click={nextBlock}>→</button>

        <!-- Carousel Indicators -->
        <div class="carousel-indicators">
            {#each blocks as _, index}
                <button 
                    class="indicator" 
                    class:active={index === currentBlockIndex}
                    on:click={() => currentBlockIndex = index}
                    aria-label="Go to block {index + 1}"
                ></button>
            {/each}
        </div>
    </section>
</div>

<style>
    :root {
        --accent: #00ffcf;
        --accent-rgb: 0, 255, 207;
        --minecraft-yellow: #ffff00;
        --bg-deep: #050606;
        --bg-stripe: #0a0d0d;
    }

    :global(html, body) {
        margin: 0;
        padding: 0;
        background: var(--bg-deep);
        font-family: "Monocraft", monospace;
        color: white;
        /* Changed overflow to allow vertical scrolling on small heights */
        overflow-x: hidden;
        width: 100%;
    }



    /* This adds a rainbow "prism" effect to the edge of the glass */
    .prism-edge {
        position: absolute;
        inset: 0;
        pointer-events: none;
        border: 2px solid transparent;
        background: linear-gradient(
                135deg,
                rgba(255, 0, 0, 0.1),
                rgba(0, 255, 255, 0.1),
                rgba(0, 0, 255, 0.1)
            )
            border-box;
        -webkit-mask:
            linear-gradient(#fff 0 0) padding-box,
            linear-gradient(#fff 0 0);
        mask:
            linear-gradient(#fff 0 0) padding-box,
            linear-gradient(#fff 0 0);
        -webkit-mask-composite: destination-out;
        mask-composite: exclude;
        opacity: 0.5;
    }

    .moving-stripes {
        position: fixed;
        inset: -100px;
        z-index: 0;
        background: repeating-linear-gradient(
            -45deg,
            var(--bg-deep),
            var(--bg-deep) 30px,
            var(--bg-stripe) 30px,
            var(--bg-stripe) 60px
        );
        background-size: 84.85px 84.85px;
        animation: stripe-move 20s linear infinite;
    }

    @keyframes stripe-move {
        from {
            background-position: 0 0;
        }
        to {
            background-position: 84.85px 84.85px;
        }
    }

    .hero {
        position: relative;
        z-index: 10;
        min-height: 100vh; /* Changed height to min-height */
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 1rem;
    }

    .carousel-section {
        overflow: hidden;
        position: relative;
    }

    .carousel-container {
        display: flex;
        position: relative;
        width: 100%;
        height: 100%;
    }

    .carousel-block {
        position: absolute;
        width: 100%;
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: center;
        left: 100%;
        opacity: 0;
        transition: left 0.6s cubic-bezier(0.4, 0, 0.2, 1), opacity 0.6s ease-in-out;
        pointer-events: none;
    }

    .carousel-block.active {
        left: 0;
        opacity: 1;
        pointer-events: auto;
    }

    .carousel-block:nth-child(1).active {
        left: 0;
    }

    .carousel-block:nth-child(2).active {
        left: 0;
    }

    .carousel-block:nth-child(3).active {
        left: 0;
    }

    /* Navigation buttons */
    .carousel-nav {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        z-index: 30;
        background: rgba(0, 255, 207, 0.2);
        border: 2px solid rgba(0, 255, 207, 0.5);
        color: var(--accent);
        font-size: 1.5rem;
        width: 50px;
        height: 50px;
        border-radius: 50%;
        cursor: pointer;
        transition: all 0.3s ease;
        font-family: "Monocraft", monospace;
        font-weight: bold;
    }

    .carousel-nav:hover {
        background: rgba(0, 255, 207, 0.4);
        border-color: var(--accent);
        box-shadow: 0 0 20px rgba(0, 255, 207, 0.5);
    }

    .carousel-prev {
        left: 2rem;
    }

    .carousel-next {
        right: 2rem;
    }

    /* Carousel indicators */
    .carousel-indicators {
        position: absolute;
        bottom: 2rem;
        left: 50%;
        transform: translateX(-50%);
        display: flex;
        gap: 1rem;
        z-index: 30;
    }

    .indicator {
        width: 12px;
        height: 12px;
        border-radius: 50%;
        border: 2px solid rgba(0, 255, 207, 0.5);
        background: transparent;
        cursor: pointer;
        transition: all 0.3s ease;
    }

    .indicator.active {
        background: var(--accent);
        box-shadow: 0 0 15px rgba(0, 255, 207, 0.6);
    }

    .indicator:hover {
        border-color: var(--accent);
        box-shadow: 0 0 10px rgba(0, 255, 207, 0.3);
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
        border-radius: 40px;
        padding: 5rem 7rem;
        overflow: visible;
        box-shadow:
            0 50px 100px rgba(0, 0, 0, 0.8),
            inset 0 0 40px rgba(255, 255, 255, 0.02);
        max-width: 900px;
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
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
        text-align: center;
        user-select: none;
    }

    .title-wrapper {
        position: relative;
        margin-top: -1rem;
        margin-bottom: 5rem;
    }

    .hero-title {
        font-size: clamp(2.5rem, 10vw, 5.5rem);
        margin: 0;
        color: var(--accent);
        letter-spacing: 10px;
        text-shadow: 8px 8px 0px rgba(0, 0, 0, 0.9);
    }

    .splash-text {
        position: absolute;
        right: -70px;
        bottom: -15px;
        color: var(--minecraft-yellow);
        font-size: clamp(0.7rem, 1.8vw, 1.25rem);
        transform: rotate(-20deg);
        text-shadow: 3px 3px 0px #3f3f00;
        white-space: normal;
        max-width: 250px;
        line-height: 1.2;
        text-align: center;
        animation: splash-pulse 0.5s ease-in-out infinite alternate;
        z-index: 20;
    }

    @keyframes splash-pulse {
        from {
            transform: rotate(-20deg) scale(0.95);
        }
        to {
            transform: rotate(-20deg) scale(1.1);
        }
    }

    .crt-vignette {
        position: fixed;
        inset: 0;
        background: radial-gradient(
            circle,
            transparent 40%,
            rgba(0, 0, 0, 0.95) 100%
        );
        pointer-events: none;
        z-index: 100;
    }

    .scanlines {
        position: fixed;
        inset: 0;
        background: linear-gradient(
            to bottom,
            rgba(255, 255, 255, 0.02) 50%,
            transparent 50%
        );
        background-size: 100% 4px;
        pointer-events: none;
        z-index: 101;
    }

    .logo {
        width: 160px;
        margin-bottom: 2rem;
        filter: drop-shadow(0 0 25px rgba(0, 255, 207, 0.3));
    }

    .hero-subtitle {
        color: #aaa;
        margin-bottom: 4rem;
        font-size: 1.3rem;
        letter-spacing: 1px;
    }

    .cta-buttons {
        display: flex;
        justify-content: center;
        gap: 1rem;
    }

    .cta-primary {
        background: var(--accent);
        color: #000;
        border: none;
        padding: 1.2rem 3.5rem;
        font-family: "Monocraft";
        font-weight: bold;
        font-size: 1.1rem;
        cursor: pointer;
        border-radius: 40px;
        transition:
            transform 0.2s,
            box-shadow 0.2s;
    }

    .cta-primary:hover {
        transform: translateY(-5px);
        box-shadow: 0 0 40px var(--accent);
    }

    .cta-secondary {
        background: rgba(255, 255, 255, 0.05);
        color: #fff;
        border: 1px solid rgba(255, 255, 255, 0.2);
        padding: 1.1rem 2.5rem;
        font-family: "Monocraft";
        cursor: pointer;
        border-radius: 40px;
    }

    /* --- TABLET OVERRIDES --- */
    @media (max-width: 1024px) {
        .glass-pane {
            padding: 4rem 5rem;
        }
    }

    /* --- MOBILE OVERRIDES --- */
    @media (max-width: 768px) {
        :global(html, body) {
            overflow-y: auto;
        }

        .glass-pane {
            padding: 2.5rem 1.5rem;
            border-radius: 20px;
            margin: 1rem;
            width: auto;
        }

        .hero {
            padding: 0.5rem;
        }

        .hero-title {
            letter-spacing: 2px;
        }

        .splash-text {
            right: 0;
            bottom: -50px;
            max-width: 180px;
            font-size: 0.85rem;
        }

        .title-wrapper {
            margin-bottom: 4.5rem;
        }

        .hero-subtitle {
            font-size: 1rem;
            margin-bottom: 2.5rem;
            padding: 0 1rem;
        }

        .logo {
            width: 100px;
            margin-bottom: 1rem;
        }

        .cta-buttons {
            flex-direction: column;
            align-items: center;
            width: 100%;
            gap: 0.75rem;
        }

        .cta-primary,
        .cta-secondary {
            width: 100%;
            margin: 0;
            padding: 0.9rem;
            font-size: 1rem;
        }
    }

    /* --- SMALL MOBILE OVERRIDES --- */
    @media (max-width: 480px) {
        .glass-pane {
            padding: 2rem 1.25rem;
            border-radius: 15px;
            margin: 0.75rem;
        }

        .hero {
            min-height: 80vh;
            padding: 0.5rem;
        }

        .hero-title {
            font-size: clamp(1.75rem, 8vw, 3.5rem);
            letter-spacing: 1px;
            text-shadow: 4px 4px 0px rgba(0, 0, 0, 0.9);
        }

        .splash-text {
            max-width: 150px;
            font-size: 0.75rem;
            bottom: -45px;
        }

        .hero-subtitle {
            font-size: 0.9rem;
            margin-bottom: 2rem;
        }

        .logo {
            width: 80px;
            margin-bottom: 0.75rem;
        }

        .cta-primary,
        .cta-secondary {
            padding: 0.75rem;
            font-size: 0.9rem;
        }
    }
</style>
