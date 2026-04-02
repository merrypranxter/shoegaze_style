# GLSL Notes for Shoegaze

Shoegaze look = 3-stage minimum:
1) soft diffusion (blur/bilateral)
2) bloom/halation (thresholded blur add)
3) texture memory (grain + dust + paper)

Optional 4) interference math:
- moire via overlaying rotated/scaled grids
- phase warp via sin-based UV perturb
- alias shimmer via quantized sampling + dither (subtle!)

Rule: interference must live INSIDE haze, not on top as crisp UI.

---

## Shoegaze Pedalboard (shader mental model)

### Pedals (order matters)
1. Diffusion (softness)
2. Bloom / Halation (bloom)
3. Memory Texture (grain + dust + paper)
4. Color Bleed (chroma aberration)
5. Interference (moire/phase warp) [optional]
6. Vignette (gentle)

### Rule
If you can toggle only 3 things:
- diffusion
- halation
- grain
…you still have shoegaze.

### A/B
- Gentle gaze: low interference, high diffusion
- Heavy gaze: higher bloom + grain, moderate interference
- Total wall: strong diffusion + bloom + grain + interference

---

## Stage 1: Soft Diffusion

```glsl
// Gaussian blur pass (softness knob drives radius)
// bilateralSigma: preserve edges slightly but not sharply
vec4 softDiffuse(sampler2D tex, vec2 uv, float radius) {
  // standard separable gaussian
  // radius controlled by knob: 0.35 (gentle) → 0.70 (total_wall)
}
```

Notes:
- Use bilateral filter if you want to preserve one focal anchor (eyes, streetlight)
- Gaussian blur alone is fine for total_wall where nothing needs to stay sharp

---

## Stage 2: Bloom / Halation

```glsl
// Threshold highlight extraction → blur → additive blend
// bloomThreshold: ~0.65 (cut out midtones)
// bloomIntensity: 0.40–0.78
// Halation: use a slightly warm (orange-red) tint on the bloom layer
//   to mimic film emulsion overspill
vec4 halationBloom(sampler2D tex, vec2 uv, float threshold, float intensity) {
  vec4 c = texture(tex, uv);
  float lum = dot(c.rgb, vec3(0.299, 0.587, 0.114));
  float extracted = max(0.0, lum - threshold);
  // blur extracted → add back with warm tint
}
```

Notes:
- Halation tint: multiply bloom by vec3(1.0, 0.85, 0.65) for warm film look
- Bloom radius should be large relative to image size (10–20% width)

---

## Stage 3: Texture Memory (grain + dust + paper)

```glsl
// Film grain: animated or static noise
// grain scale: 0.45–0.85 (filmGrainAmount knob)
float filmGrain(vec2 uv, float time, float amount) {
  // Hash-based or texture-based noise
  // Apply in luminance channel for authenticity
  float n = fract(sin(dot(uv * 1000.0 + time, vec2(12.9898, 78.233))) * 43758.5453);
  return (n - 0.5) * amount;
}
// Add to final color luminance, not RGB separately
```

Notes:
- Dust/scratches: overlay a pre-made texture (tileable matte paper or film scan)
- Matte paper fiber: low-frequency noise overlay at low opacity (3–8%)

---

## Stage 4 (optional): Interference Math

```glsl
// Moire: overlay two slightly offset/rotated grid patterns
// moireStrength: 0.10 (subtle shimmer) → 0.45 (total_wall)
float moire(vec2 uv, float strength) {
  float a = sin(uv.x * 80.0 + uv.y * 60.0);
  float b = sin(uv.x * 82.0 + uv.y * 58.0); // slight offset
  return (a * b) * strength;
}

// Phase warp: sin-based UV perturbation
vec2 phaseWarp(vec2 uv, float phaseWarpAmount) {
  float wx = sin(uv.y * 12.0) * phaseWarpAmount;
  float wy = cos(uv.x * 12.0) * phaseWarpAmount;
  return uv + vec2(wx, wy);
}
```

Critical rule: Apply interference BEFORE the diffusion/bloom pass (or blend gently after),
so it gets "dissolved" into the haze. Interference on top = op-art sticker (wrong).

---

## Stage 5: Color Bleed (Chromatic Aberration)

```glsl
// Offset R/G/B channels slightly on UV
// chromaticAberration: 0.12–0.35
vec4 colorBleed(sampler2D tex, vec2 uv, float amount) {
  float r = texture(tex, uv + vec2(amount, 0.0)).r;
  float g = texture(tex, uv).g;
  float b = texture(tex, uv - vec2(amount, 0.0)).b;
  return vec4(r, g, b, 1.0);
}
```

---

## Stage 6: Vignette

```glsl
// Gentle radial darkening
// vignetteAmount: 0.18–0.40
float vignette(vec2 uv, float amount) {
  vec2 d = uv - 0.5;
  return 1.0 - dot(d, d) * amount * 2.0;
}
```

---

## Full shoegaze pass order

```
input
  → [optional] phase warp UV (interference prep)
  → diffusion blur
  → bloom/halation extraction + blur + additive blend
  → film grain + dust overlay
  → [optional] moire overlay (fused, not crisp)
  → color bleed (chroma aberration)
  → tone curve (low contrast rolloff)
  → vignette
output
```

---

## Anti-patterns to avoid in GLSL

- Sharpen filter at any stage (kills the vibe instantly)
- High-frequency noise without blur (looks like static, not grain)
- Moire at full contrast without pre-blur (becomes op-art, not shoegaze)
- Vignette radius too tight (looks like a bad Instagram filter)
- Bloom with no halation tint (too clean / modern)
