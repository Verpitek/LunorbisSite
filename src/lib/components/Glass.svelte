<script lang="ts">
    import { onMount } from "svelte";

    let canvas: HTMLCanvasElement;
    let gl: WebGLRenderingContext;
    let program: WebGLProgram;
    let animationFrame: number;

    const vs = `
        attribute vec2 position;
        void main() {
            gl_Position = vec4(position, 0.0, 1.0);
        }
    `;

    const fs = `
        precision highp float;
        uniform float u_time;
        uniform vec2 u_resolution;

        // Function to create "glassy" noise
        float hash(vec2 p) { return fract(sin(dot(p, vec2(127.1, 311.7))) * 43758.5453123); }
        
        void main() {
            vec2 uv = gl_FragCoord.xy / u_resolution.xy;
            float time = u_time * 0.5;
            
            // Simulated refraction logic
            vec2 shift = vec2(
                sin(uv.y * 10.0 + time), 
                cos(uv.x * 10.0 + time)
            ) * 0.01;

            // Chromatic Aberration (Refraction)
            float r = fract(sin(dot(uv + shift, vec2(12.9898, 78.233))) * 43758.5453);
            vec3 color;
            color.r = texture2D(u_resolution, uv + shift * 1.1).r; // Mocking refraction
            color.g = texture2D(u_resolution, uv + shift).g;
            color.b = texture2D(u_resolution, uv + shift * 0.9).b;

            // Generate "Light Beams"
            float light = 0.0;
            light += sin(uv.x * 10.0 + time) * 0.5 + 0.5;
            light *= cos(uv.y * 5.0 - time * 0.3) * 0.5 + 0.5;
            
            vec3 glassColor = vec3(0.1, 0.15, 0.18); // Tint
            vec3 highlights = vec3(0.0, 1.0, 0.8) * pow(light, 10.0) * 0.3; // Cyan refractions
            
            gl_FragColor = vec4(glassColor + highlights, 0.4);
        }
    `;

    onMount(() => {
        gl = canvas.getContext("webgl")!;
        const createShader = (type: number, source: string) => {
            const s = gl.createShader(type)!;
            gl.shaderSource(s, source);
            gl.compileShader(s);
            return s;
        };

        program = gl.createProgram()!;
        gl.attachShader(program, createShader(gl.VERTEX_SHADER, vs));
        gl.attachShader(program, createShader(gl.FRAGMENT_SHADER, fs));
        gl.linkProgram(program);
        gl.useProgram(program);

        const buffer = gl.createBuffer();
        gl.bindBuffer(gl.ARRAY_BUFFER, buffer);
        gl.bufferData(gl.ARRAY_BUFFER, new Float32Array([-1,-1, 1,-1, -1,1, -1,1, 1,-1, 1,1]), gl.STATIC_DRAW);

        const pos = gl.getAttribLocation(program, "position");
        gl.enableVertexAttribArray(pos);
        gl.vertexAttribPointer(pos, 2, gl.FLOAT, false, 0, 0);

        const timeLoc = gl.getUniformLocation(program, "u_time");
        const resLoc = gl.getUniformLocation(program, "u_resolution");

        function render(t: number) {
            gl.viewport(0, 0, canvas.width, canvas.height);
            gl.uniform1f(timeLoc, t / 1000);
            gl.uniform2f(resLoc, canvas.width, canvas.height);
            gl.drawArrays(gl.TRIANGLES, 0, 6);
            animationFrame = requestAnimationFrame(render);
        }
        render(0);

        return () => cancelAnimationFrame(animationFrame);
    });
</script>

<canvas bind:this={canvas} class="webgl-canvas"></canvas>

<style>
    .webgl-canvas {
        position: absolute;
        inset: 0;
        width: 100%;
        height: 100%;
        pointer-events: none;
        opacity: 0.6;
        z-index: 0;
    }
</style>