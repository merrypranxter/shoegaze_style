# Golden Notes (Shoegaze Style)

These are the canonical reference prompts and drift-prevention notes.
Do not edit the Golden Prompts casually — they are anchors for style consistency.

---

## Golden Prompts

### G1: Harmonic Ladder Portrait
portrait implied by harmonic ladders, face emerging from banded frequency architecture, shoegaze aesthetic, halation glow, film grain veil, edges dissolving into haze, palette:haze_pastel

### G2: Granular Cloud Dancer
a dancer implied by granular particle swarm, micro-event glitter fog, dreamy diffusion bloom, tactile noise, gentle vignette, palette:nocturne_neon

### G3: Reich Phasing Cover
album cover design, minimal subject implied by phasing process, moire-from-time shimmer inside haze, matte sleeve texture, typography ghost, palette:cd_iridescent

### G4: Convolution Cathedral
echo cathedral formed by impulse-response trails, temporal smears stacked into arches, fog volume, halation, dust and scratches, palette:milkglass

---

## Drift Checklist (run whenever you add tokens)

- Does the style still pass the Shoegaze Test? (blur it slightly; still works)
- Are edges dissolving, not outlined?
- Is texture leading, not accessory?
- Is there at least one memory material (film/paper/signal)?
- If interference is present: is it fused into haze (not crisp overlay)?
- Negatives still remove "clinical HDR / ultra sharp" vibes?

---

## Style Linter

A prompt passes if:
- Contains at least 1 core token: "shoegaze aesthetic" OR "wall of texture" OR "edges dissolving into haze"
- Contains at least 1 light token: halation / bloom / leaks
- Contains at least 1 texture token: grain / dust / paper
- Contains at least 1 dissolve/composition behavior: field over subject / negative space / dissolve
- Does NOT contain infographic terms when using sound_math engine (diagram / axes / labels)

Optional but recommended:
- Includes a palette token
- Includes one memory material (film / paper / signal)
- Includes a single focal anchor

Scoring (0–2 per item):
- 10–12: perfect
- 7–9: good, tweak 1–2 areas
- <7: missing a layer or too clean/noisy

---

## Style Fingerprint (must-haves and must-avoids)

### Must-have tokens (at least one must appear in every compiled prompt)
- shoegaze aesthetic
- wall of texture
- edges dissolving into haze
- dreamy diffusion bloom
- halation glow
- film grain clumps
- field over subject

### Must-avoid tokens (these signal the style has drifted)
- diagram
- axes
- labeled chart
- ultra sharp
- clinical HDR
- clean vector art

---

## Common Failure Modes and Fixes

### Too crisp / modern editorial
Symptoms: sharp edges everywhere, clean studio light, looks like a tech ad.
Fix: add haze veil layers + low contrast rolloff + film grain clumps + halation glow.
Add negatives: ultra sharp, clinical HDR, crisp outlines.

### Glitch looks like a vector overlay
Symptoms: moire is too clean, reads like op-art sticker.
Fix: fuse interference into haze: add "grain veil", "fog volume", "smudged highlights", "soft focus lens".
Rule: interference must be *inside* atmosphere.

### Texture everywhere, no focal anchor
Symptoms: it's just noise, nothing to feel.
Fix: "single sharp detail" rule: eyes, a streetlight, one highlight edge — everything else dissolves.

### Too brown / muddy
Symptoms: flat mud, no shimmer.
Fix: add chromatics: milky highlights, subtle color bleed, pastel wash OR neon bleed.

### Interference looks like an infographic
Add negative group: diagram, axes, labels, UI overlay, chart.
Add: "natural phenomenon", "embedded in atmosphere".

---

## Shoegaze Test

If you blur the image slightly and it *still works*, you're in shoegaze territory.
If blurring it makes it worse, something is wrong — the image is relying on sharp detail.
