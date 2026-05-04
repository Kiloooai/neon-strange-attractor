# 🌀 Neon Strange Attractor

*Watch chaotic systems paint their signature shapes in glowing neon. Lorenz's butterfly, Rossler's twisted band — adjust the underlying equations in real time and see the attractor morph. Click to add more trajectories. Color cycling, adjustable simulation speed, trail width. Pure mathematical beauty.*

---

## What is this?

A strange attractor is a set toward which a chaotic system evolves over time. The trajectory never repeats, yet it stays confined to a fractal structure. Classic examples include the Lorenz attractor (butterfly shape) and the Rossler attractor (twisted band). This interactive visualizer simulates these ordinary differential equations and renders the path with neon glow, color cycling, and persistent trails.

---

## Features

- **Two attractor systems:**
  - **Lorenz** — classic weather model producing the iconic butterfly wings
  - **Rossler** — a simpler three-dimensional system yielding a twisted band
- **Real-time parameter adjustment:** Change the ODE constants (σ, ρ, β for Lorenz; a, b, c for Rossler) and watch the attractor reshape itself on the fly
- **Multiple trajectories:** Click anywhere to spawn additional particles; each draws its own path, filling the structure faster
- **Neon glow** with HSL color cycling based on time and per-trajectory hue offsets
- **Adjustable simulation speed** — speed up or slow down the numerical integration
- **Trail width control** (1–4 px)
- **Pause/Resume**, **Clear** (wipe canvas and restart), **Randomize** (pick random attractor type and random parameters)
- **Stats overlay** — particle count, FPS
- **Single HTML file** — no dependencies

---

## How to Use

1. Open `index.html`
2. A single particle starts near the origin and traces the attractor's path. The trail accumulates, revealing the strange attractor's shape.
3. **Click** anywhere to inject a new particle at that screen location; it will trace its own trajectory (slightly different due to floating-point and starting point).
4. Use the controls:
   - **Attractor Type** — switch between Lorenz and Rossler
   - **Three parameter sliders** — labels change based on type. Adjust to see how the system reacts:
     - *Lorenz*: σ (sigma) controls the coupling between variables; ρ (rho) is the Rayleigh number (driving force); β (beta) is a damping factor. Classic chaotic values: σ=10, ρ=28, β≈2.6667.
     - *Rossler*: a, b, c control the system's nonlinearities. Typical: a=0.2, b=0.2, c=5.7.
   - **Sim Speed** — multiplies the integration timestep, making the particle move faster along the attractor (doesn't change shape, just drawing speed)
   - **Color Cycle** — how quickly the global hue rotates
   - **Trail Width** — thickness of drawn lines
5. Press **Randomize** to pick a random attractor type and random parameter values within useful ranges; the canvas clears and restarts.
6. **Pause** to freeze the simulation; **Clear** to wipe the drawing and reset particles to the origin

---

## Technical Details

- **Numerical integration:** 1st-order Euler with fixed timestep `dt = 0.01` (in simulation time), scaled by the Sim Speed multiplier.
- **Coordinate system:** World coordinates (x, y, z) are mapped to screen with a scaling factor based on the smaller canvas dimension and a y-flip (so up is up). Origin at screen center.
- **Rendering:** A persistent offscreen canvas (`trailCanvas`) accumulates the path as line segments. Each segment is drawn with `shadowBlur` for neon glow. The main canvas copies the offscreen buffer each frame and overlays the current particle positions as glowing dots.
- **Particle management:** Each particle tracks its own (x,y,z) state and previous screen position. New particles from clicks are converted from screen to world coordinates. Particles that diverge to infinity (NaN or huge values) are automatically reset near the origin.
- **Performance:** O(P) per frame for P particles. The drawing load grows with total segments but Canvas handles thousands of lines easily.

---

## The Real Story

Strange attractors are the fingerprints of chaos. They look complicated, but they're deterministic — given the same initial conditions, you'll get the same infinite, non-repeating curve. Tweaking even one parameter can dramatically reshape the attractor: the Lorenz butterfly can shrink, split, or dissolve into chaos. Watching the neon trails build up in real time is mesmerizing; you see the structure emerge, layer by layer. Adding more trajectories fills out the attractor faster, creating a dense, glowing lace of mathematics.

---

*Made with 🌀 and differential equations.*

**Repo:** https://github.com/Kiloooai/neon-strange-attractor
