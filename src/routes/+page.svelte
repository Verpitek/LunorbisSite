<script lang="ts">
    import { onMount } from "svelte";
    import lunorbisLogo from "$lib/assets/lunorbis.svg";
    import MatrixBackground from "$lib/components/MatrixBackground.svelte";
    import Glass from "$lib/components/Glass.svelte";
    import TypeWriter from "$lib/components/TypeWriter.svelte";

    let currentQuote = "";

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

    onMount(() => {
        currentQuote = quotes[Math.floor(Math.random() * quotes.length)];
    });
</script>

<div class="page terminal-theme">
    <div class="moving-stripes"></div>
    <div class="crt-vignette"></div>
    <div class="scanlines"></div>

    <MatrixBackground count={25} />

    <section class="hero" data-collision-box>
         <div class="glass-pane">
             <Glass />
             
             <div class="prism-edge"></div>
             <div class="glass-glare"></div>

             <div class="glass-content">
                <div class="logo-container">
                    <img src={lunorbisLogo} alt="Logo" class="logo" />
                </div>

                <div class="title-wrapper">
                    <h1 class="hero-title">
                        <TypeWriter text="LUNORBIS" speed={80} delay={500} showCursor={false} />
                    </h1>
                    {#if currentQuote}
                        <div class="splash-text">
                            <TypeWriter text={currentQuote} speed={40} delay={500} showCursor={true} />
                        </div>
                    {/if}
                </div>

                <p class="hero-subtitle">
                    <TypeWriter text="High-Performance Bedrock Server Runtime" speed={50} delay={500} showCursor={false} />
                </p>

                <div class="cta-buttons">
                    <button class="cta-primary">Install Now!</button>
                    <button class="cta-secondary">Docs</button>
                </div>
            </div>
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
        background: none;
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

    /* Glass glare stripe animation */
    .glass-glare {
        position: absolute;
        top: 0;
        left: -150%;
        width: 100%;
        height: 100%;
        background: linear-gradient(
            90deg,
            transparent,
            rgba(255, 255, 255, 0.08) 45%,
            rgba(255, 255, 255, 0.15) 50%,
            rgba(255, 255, 255, 0.08) 55%,
            transparent
        );
        transform: skewX(-25deg);
        pointer-events: none;
        animation: glare-sweep 2.5s ease-in-out forwards;
        animation-delay: 0.8s;
    }

    @keyframes glare-sweep {
        0% {
            left: -150%;
        }
        100% {
            left: 150%;
        }
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

    @keyframes bob {
        0%, 100% {
            transform: translateY(0px);
        }
        50% {
            transform: translateY(-15px);
        }
    }

    .scroll-indicator {
        position: absolute;
        bottom: 2rem;
        left: 50%;
        transform: translateX(-50%);
        z-index: 20;
        font-size: 2rem;
        color: var(--accent);
        animation: bob 1.5s ease-in-out infinite;
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

    .blocks-section {
        position: relative;
        z-index: 10;
        padding: 4rem 1rem;
        background: var(--bg-deep);
    }

    .blocks-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
        gap: 2rem;
        max-width: 1200px;
        margin: 0 auto;
        padding: 0 1rem;
    }

    .block-card {
        display: flex;
        align-items: stretch;
    }

    .block-title {
        font-size: clamp(1.5rem, 5vw, 2.5rem);
        margin: 0 0 1rem 0;
        color: var(--accent);
        letter-spacing: 5px;
    }

    .block-subtitle {
        color: #aaa;
        margin-bottom: 2rem;
        font-size: 1rem;
        letter-spacing: 1px;
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
        overflow: hidden;
        box-shadow:
            /* Close shadow for depth */
            0 20px 40px rgba(0, 0, 0, 0.4),
            /* Medium shadow for realism */
            0 40px 80px rgba(0, 0, 0, 0.6),
            /* Far shadow for atmosphere */
            0 80px 150px rgba(0, 0, 0, 0.7),
            /* Inner depth */
            inset 0 0 40px rgba(255, 255, 255, 0.02);
        max-width: 900px;
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        animation: undissolve 3s ease-out forwards;
    }

    @keyframes undissolve {
        0% {
            opacity: 0;
            filter: blur(20px);
        }
        100% {
            opacity: 1;
            filter: blur(0);
        }
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
