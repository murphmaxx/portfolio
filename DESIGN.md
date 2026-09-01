# Technical portfolio — visual system

<!-- impeccable:design-schema 2 -->

## World

An expensive defense-industrial field interface over a real rendered terrain. Carbon graphite is the environment. Signal orange is the measured instrument. Titanium is the quiet closing plane. Project information travels through the field as technical records that tilt toward the pointer for inspection.

## Palette

- `--carbon`: `#0A0C0E` — persistent background field
- `--panel`: `#12161B` — project record base (used translucent over the render)
- `--panel-2`: `#161C22` — elevated record
- `--titanium`: `#C2C5C7` — closing/document surface
- `--white`: `#ECEEF0` — foreground
- `--muted`: `#98A1A8` — secondary text
- `--line`: `#333C44` — structure
- `--signal`: `#C97435` — action and verification signal
- `--signal-2`: `#E0965A` — small signal accents on dark
- `--signal-dark`: `#7D4A20` — signal on titanium
- `--ink`: `#101418` — text on titanium

No neon, purple, cyan, pills, glows, or playful color fields. Signal orange is rare: actions, measured points, verification.

## Background

The field is a real render v2: `site/assets/field-render.jpg`, a seeded deterministic three.js scene — two ridge systems framing a valley that opens to a warm horizon, elevation-graded wireframe (crests bright steel, floors dark), soft round dust motes with signal embers, survey posts. Generator archived at `motion/render-field-generator.html`; re-render via headless Chromium at 2560×1440. The old CSS mesh/trace/marker field and `motion/field-background.*` are retired.

Above the terrain sits the Eye v2 — pure 3D, no flourishes (the Ra teardrop, tail strokes, reticle, brow, lashes, and the specular glint are all gone). Two passes from one camera (`motion/render-eye-generator.html`): `site/assets/eye-frame.png` (thick machined lid tubes with groove lines, canthus caps with signal dots, concave lathe socket bowl, housing ring) and `site/assets/eye-iris.png` (domed 64-blade turbine in a barrel, orange pupil rim, glow ring, graduations). Both PNGs overlay at identical full size, pixel-aligned.

## Composition

The hero is tall; its rendered field stays fixed while the document scrolls. Project boxes alternate modest x/y offsets to create depth while preserving reading order. The closing settles onto the titanium plane.

## Motion grammar

- Card tilt is the keel/Codrops TiltFx model: the outer `.project-box` never rotates — it owns layout offset, scroll shift, perspective, and the pointer listeners, so hit geometry stays stable; the inner `.record` rotates (±6° X, ±10° Y). The pointer sets a linear target; the card glides toward it (lerp 0.16/frame, ~200 ms settle) so crossing an edge never snaps, then tracks 1:1.
- Inner planes (`.project-info`, `.project-data`, `.media-field`) drift a few px in 2D against the tilt so the record comes apart in depth. No translateZ on children.
- Release is a JS elastic tween (~900 ms) back to flat. No CSS transition on transform anywhere in that pipeline.
- Scroll writes only `--shift` (cards) and `--bg-y`/`--bg-scale` (render drift); the tilt handler writes only `--rx/--ry/--px/--py`.
- The Eye's iris follows the cursor anywhere on the page: direction is the vector from the eye's center to the pointer, deflection saturates ~420px out, travel ≤3.2% of the eye box plus ≤9°/7° swivel, gliding at 0.06/frame (heavier than the cards — it is an eyeball). The frame layer never moves; scroll drifts the whole eye slower than the terrain.
- Idle life: after ~3.5s without pointer movement the eye saccades to a random nearby point every 2.6–5.2s (runs on touch devices too); the iris rotates once every 4 minutes (CSS `iris-spin`); the whole eye bobs ±7px over 7.5s (CSS `eye-bob` on `.eye-inner`).
- Blink: real lids — the top lid does most of the travel (64%/42% heights), close .08s ease-in, open .16s ease-out, held ~140ms, at a random 4–9s cadence with a 22% double-blink. Layer order inside `.eye-inner`: frame img → `.iris-gaze` (cursor transform) → iris img (spin) → `.lids`.
- Scroll-weave: the eye rides the open space beside the passing card. Each card's larger side gap (measured from its live rect — never a static table; `.stage-heading` shifts nth-of-type indices) is the target: the eye centers in that gap at the card's height, scaled to fit it (clamped 0.24–0.62, always fully on-screen), blended by squared card-proximity weights with the hero pulling toward the home spot. Deterministic and scroll-linked; desktop only (>900px).
- Coarse pointers and reduced motion get no tilt and a centered gaze; reduced motion starts with the motion toggle off.

## Controls

Rectangular actions with separate arrow cells. No pills. The control language is an instrument panel, not a marketing button.

## Responsive rules

Desktop uses offsets, scroll parallax, and pointer tilt. ≤900px collapses records to one column, kills tilt and inner drift (`transform:none !important` on `.record` and children), keeps scroll shift. ≤620px tightens type. `html.motion-off` freezes tilt and drift and preserves layout offsets.

## Content boundary

The approved tagline is “Systems that show their work.” (supersedes “Controls for consequential AI.”, 2026-08-31). Project descriptions and evidence labels remain provisional until real source material is reviewed.
