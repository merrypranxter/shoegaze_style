# Before / After: Shoegaze Style Transformations

These examples show how to convert a plain prompt into a shoegaze-aesthetic prompt.
Each pair demonstrates the "before" (generic/neutral) and "after" (shoegaze-treated) version.

---

## Example 1: Street Portrait

**Before** (generic):
```
A portrait of a woman under a streetlight at night. Sharp focus, detailed face, clear background.
```

**After** (shoegaze — gentle_gaze preset, haze_pastel):
```
portrait of a woman, face partially implied by haze, gauze diffusion, soft focus lens,
shoegaze aesthetic, nostalgic grain, highlight bloom, chromatic aberration,
background melts into texture field, haze_pastel
--no sharp pores, overdefined anatomy, hard rim light
```

**What changed:**
- Subject becomes *implied*, not declared
- Background actively dissolves rather than being described
- Memory materials added (gauze diffusion, nostalgic grain)
- Explicit negatives prevent the generation from snapping to editorial clarity

---

## Example 2: Album Cover

**Before** (generic):
```
Album cover with a centered person, white background, clear bold title text at the top.
```

**After** (shoegaze — zine_haze preset, sepia_zine):
```
album cover design, centered minimal subject dissolving into texture field,
shoegaze aesthetic, matte paper fiber, washed midtones, soft blur, subtle typography ghost,
large negative space, matte sleeve texture, faded liner-note fragments, sepia_zine
--no big readable text, no clean vector poster look
```

**What changed:**
- Typography becomes a "ghost" (present but not readable)
- Texture materials replace clean background (paper fiber, sleeve texture)
- Negative space is emphasized, not filled with content
- Print memory materials ground it in physical/analog nostalgia

---

## Example 3: Abstract / Sound-as-Image

**Before** (generic):
```
A visualization of sound waves. Clean geometric sine curves on a dark background.
```

**After** (shoegaze — total_wall preset, cd_iridescent):
```
implied form emerging from interference, beat-frequency bands,
moire shimmer, standing-wave ripples, phase drift, shoegaze texture field,
oil-slick iridescence, grain veil, atmospheric depth, cd_iridescent
--no clean vector lines, perfect symmetry, diagram, axes, labeled chart
```

**What changed:**
- "Sound waves" becomes *implied geometry* inside haze, not diagrammatic curves
- Interference math (moire, phase drift, beat-frequency) replaces clean sine curves
- Oil-slick iridescence adds material depth
- Strong negatives prevent infographic/schematic rendering

---

## Example 4: Environment / Landscape

**Before** (generic):
```
A rainy city street at night. Neon signs reflected in puddles. Sharp, HDR look.
```

**After** (shoegaze — heavy_gaze preset, nocturne_neon):
```
rainy night street, wet asphalt reflections, sodium glow, fog volume, film grain clumps,
neon bleed, wall of texture, strong halation, heavy grain clumps,
subtle chromatic aberration, edges dissolve into haze, nocturne_neon, moire shimmer
--no tack sharp, hard rim light, hyper-detailed, clinical HDR
```

**What changed:**
- "Sharp HDR" is explicitly reversed with negatives and low-clarity tokens
- Fog volume and neon bleed replace clarity with atmosphere
- "Edges dissolve into haze" explicitly instructs boundary dissolution
- Grain and halation stack over the neon to prevent it from reading as clean 3D render

---

## Example 5: Portrait — Before/After Failure Fix

**Drifted output problem:**
Generation came out too sharp — plastic skin, crisp hair, beauty-ad lighting.

**Patch tokens to add:**
```
foreground haze veil, low contrast rolloff, film grain clumps, halation glow,
face partially implied by haze, gauze diffusion fabric
```

**Negatives to add:**
```
ultra sharp, clinical HDR, crisp outlines, overdefined pores, hard edge rim light
```

**Rule:** One anchor detail only (eyes or a highlight edge) — everything else dissolves.

---

## Preset Quick-Reference

| Preset              | Softness | Grain | Bloom | Interference | Use For                        |
|---------------------|----------|-------|-------|--------------|-------------------------------|
| `gentle_gaze`       | 0.72     | 0.55  | 0.60  | 0.20         | Portraits, soft scenes         |
| `heavy_gaze`        | 0.86     | 0.76  | 0.82  | 0.55         | Nocturne, neon, rainy streets  |
| `total_wall`        | 0.92     | 0.88  | 0.90  | 0.74         | Abstract, interference, covers |
| `zine_haze`         | mid      | mid   | mid   | low          | Print memory, album covers     |
| `crt_reverb`        | mid      | mid   | mid   | mid          | Signal memory, CRT, motion     |
| `pastel_wash`       | high     | low   | high  | none         | Dream-pop, airy softness       |
| `sodium_melancholy` | high     | mid   | high  | low          | Streetlights, night weather    |

---

## The 4 Invariants (non-negotiable rules)

1. **Field > Subject** — Texture and atmosphere lead; subject can be partially lost.
2. **Soft Boundaries** — Edges melt. Sharpness is localized (if at all), never global.
3. **Layer Stack** — Minimum three layers: haze/veil + bloom/halation + grain/texture.
4. **Memory Materials** — Image should feel "recorded" not "rendered": film, paper, xerox, CRT/VHS.
