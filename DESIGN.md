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

The field is a real render: `site/assets/field-render.jpg`, a seeded deterministic three.js scene (machined graphite terrain, steel survey wireframe, warm signal rake light, survey posts). Generator archived at `motion/render-field-generator.html`; re-render via headless Chromium at 2560×1440. The old CSS mesh/trace/marker field and `motion/field-background.*` are retired.

## Composition

The hero is tall; its rendered field stays fixed while the document scrolls. Project boxes alternate modest x/y offsets to create depth while preserving reading order. The closing settles onto the titanium plane.

## Motion grammar

- Card tilt is the keel/Codrops TiltFx model: the outer `.project-box` never rotates — it owns layout offset, scroll shift, perspective, and the pointer listeners, so hit geometry stays stable; the inner `.record` rotates (±6° X, ±10° Y), a linear function of pointer position across the whole card.
- Inner planes (`.project-info`, `.project-data`, `.media-field`) drift a few px in 2D against the tilt so the record comes apart in depth. No translateZ on children.
- Release is a JS elastic tween (~900 ms) back to flat. No CSS transition on transform anywhere in that pipeline.
- Scroll writes only `--shift` (cards) and `--bg-y`/`--bg-scale` (render drift); the tilt handler writes only `--rx/--ry/--px/--py`.
- Coarse pointers and reduced motion get no tilt; reduced motion starts with the motion toggle off.

## Controls

Rectangular actions with separate arrow cells. No pills. The control language is an instrument panel, not a marketing button.

## Responsive rules

Desktop uses offsets, scroll parallax, and pointer tilt. ≤900px collapses records to one column, kills tilt and inner drift (`transform:none !important` on `.record` and children), keeps scroll shift. ≤620px tightens type. `html.motion-off` freezes tilt and drift and preserves layout offsets.

## Content boundary

The approved tagline is “Systems that show their work.” (supersedes “Controls for consequential AI.”, 2026-08-31). Project descriptions and evidence labels remain provisional until real source material is reviewed.
