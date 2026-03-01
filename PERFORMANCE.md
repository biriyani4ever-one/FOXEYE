

---

# 🌍 Geopolitical Intelligence Dashboard
## Dell G7 Performance-Optimized UI Blueprint

Goal:
Deliver cinematic visuals while maintaining 50–60 FPS on:
- GTX 1050 / 1060 / 1650 class GPUs
- 8–16GB RAM
- Laptop thermally constrained CPU

This blueprint aggressively prioritizes stability over visual excess.

---

# 1. PERFORMANCE TARGETS

## Frame Targets
- Ideal: 60 FPS
- Minimum acceptable: 45 FPS
- Absolute floor: 30 FPS (with auto quality reduction)

## VRAM Budget
- Max 1.2–1.5GB usage
- No 4K textures
- No excessive shadow maps

---

# 2. CORE RENDERING OPTIMIZATION

## 2.1 Globe Configuration (Low-Overhead Mode)

Disable:
- Real-time shadows
- Dynamic atmospheric scattering
- High-frequency terrain detail

Enable:
- FXAA only (NO MSAA)
- Tile LOD reduction at distance
- Max screen space error: increased for performance

Cesium settings:
```js
viewer.scene.fxaa = true;
viewer.scene.postProcessStages.fxaa.enabled = true;
viewer.scene.globe.maximumScreenSpaceError = 4;
viewer.scene.shadowMap.enabled = false;


---

3. CAMERA OPTIMIZATION

3.1 Smooth but Lightweight Transitions

Duration capped at 1.5 seconds

Disable motion blur

No real-time depth-of-field


Use easing:

Quadratic in/out only

Avoid heavy cubic bezier calculations



---

4. SHADER SYSTEM (LOW GPU MODE)

Heavy shaders destroy laptop GPUs. So we implement tiered quality modes.


---

4.1 Quality Modes

Ultra (Manual Only)

Bloom

LUT

Thermal ramp

Grain

Scanlines


Balanced (Default for Dell G7)

Bloom reduced

No chromatic aberration

No dynamic grain

Static LUT


Performance Mode (Auto-trigger below 40 FPS)

Disable bloom

Disable scanlines

Disable noise overlays

Thermal simplified to color tint only



---

4.2 Thermal Mode Optimization

Instead of per-pixel dynamic heat mapping:

Use:

Precomputed country heat textures

Single gradient shader

No animated heat diffusion



---

5. SATELLITE & FLIGHT LIMITS

Unbounded live entities will melt your GPU.

Satellite Cap

Max visible: 120

Orbit path simplified to low-poly

Hide orbit trails when zoomed out


Flight Cap

Max visible: 200 global

Only render in camera frustum

Disable path history after 20 seconds


Use spatial filtering:

if (!viewer.camera.computeViewRectangle()) skipRender();


---

6. TRAFFIC PARTICLE SYSTEM (CRITICAL FIX)

Particles are dangerous for laptops.

Rules:

Max 5,000 particles total

GPU instancing only

No physics engine

No collision detection

Speed variation via shader, not CPU


Density scaling:

Zoomed out → 30% density

Zoomed in → 100%



---

7. CCTV PROJECTION SIMPLIFICATION

NO live video textures at 60 FPS.

Instead:

1 FPS refresh rate

720p cap

Pause projection when off-screen

Disable projection when FPS < 40



---

8. HEATMAP OPTIMIZATION

Country resilience layer:

Use single GeoJSON layer

Precomputed color values

No animated transitions

No per-frame recalculation


Opacity slider must not trigger re-render of geometry.


---

9. CRISIS CASCADE VISUAL

Keep it 2D overlay.

Do NOT:

Animate globe geometry

Add ripple mesh distortion


Use:

D3 SVG overlay

CSS transitions

Canvas 2D



---

10. RIGHT SIDEBAR OPTIMIZATION

Virtualized list (React Window)

No re-render on each feed update

Throttle updates to 2 per second

Collapse inactive panels automatically



---

11. BOTTOM TICKER OPTIMIZATION

CSS transform animation (GPU accelerated)

No JS-driven scroll loops

Timer updated once per second only



---

12. GLOBAL RISK INDICATOR

Simple radial SVG gauge. No WebGL. No 3D pulsing mesh.

Pulse effect:

CSS opacity animation only



---

13. AUTO PERFORMANCE MONITOR

Implement FPS monitor.

If FPS < 40 for 5 seconds:

Auto switch to:

Performance Mode

Reduce satellite count

Reduce flight count

Disable bloom


If FPS < 30:

Disable traffic particles

Disable thermal mode



---

14. MEMORY SAFETY RULES

Dispose unused Cesium entities

Remove old flight paths every 30 seconds

Clear satellite trail history

Limit cached GeoJSON size

Use Redis TTL for backend caching



---

15. ANIMATION BUDGET

Allowed:

Opacity fade

Scale pulse

Camera movement


Forbidden:

Mesh morphing

Per-frame geometry rebuild

High-frequency shader noise



---

16. VISUAL STYLE (LIGHTWEIGHT)

Keep the aesthetic strong but efficient:

Dark matte background

Cyan accent lines

Orange highlight for flagged aircraft

Magenta flash for crisis trigger

Subtle bloom only on UI, not globe



---

17. FINAL TARGET EXPERIENCE

On a Dell G7, the system should:

Boot in under 5 seconds

Hold steady 55–60 FPS

Never spike CPU to 100%

Avoid thermal throttling

Remain responsive during camera travel

Maintain stable RAM footprint


The experience should feel: Smooth. Controlled. Responsive. Cinematic without overheating the machine.

---
