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

**The field is live** (basement.studio direction, 2026-08-31): a three.js world rendered in-page on a fixed canvas behind the document — the v2 valley terrain (ridged noise, elevation-graded wireframe, horizon glow, drifting motes, survey posts) and the machined 3D eye as a real object floating over it. The camera parallaxes with the cursor (springs, ±7 world units) and dollies gently with scroll: the page is a place.

Fallback: the pre-rendered stills remain in the DOM (`site/assets/field-render.jpg` + the two eye PNGs with all their CSS-var behaviors) and are what mobile, coarse pointers, ≤900px, and no-WebGL browsers get. When the scene boots it adds `.live` to `.field`, hiding the static layers. Generators stay archived in `motion/` — the scene code is the same geometry, kept in sync by hand.

## Composition

The hero is tall; its rendered field stays fixed while the document scrolls. Project boxes alternate modest x/y offsets to create depth while preserving reading order. The closing settles onto the titanium plane.

## Motion grammar

- Camera: cursor parallax + scroll dolly, spring-damped (k=14, zeta=0.9). Every layer of the world shifts perspective together — this, not any single effect, is the basement feel.
- Card tilt (DOM, unchanged): keel/Codrops split, glide 0.16/frame, elastic release.
- The eye is a scene object. Position/scale ride springs (x k=22 zeta=0.80, y k=30 zeta=0.85, scale critically damped) toward screen-space targets computed by the same gap logic as the fallback: hero home upper-right; past the hero it weaves into each passing card's larger side gap, at the card's height, sized to fit, clamped on-screen. Underdamped x vs y gives curved, organic travel.
- Gaze: the whole eye assembly rotates toward the cursor's world point (quaternion slerp 0.055/frame). Idle saccades offset the look target on a 2.6–5.2s clock after 3.5s of pointer stillness. Iris revolves once per ~4 minutes; the eye bobs ±0.35 units on a 7.5s sine.
- Blink: two half-disc shutters in front of the socket; close 80ms, hold 110ms, open 170ms; random 4–9s cadence, 22% double.
- Motion off / reduced motion: the main script broadcasts a `motionchange` event; the scene freezes on a clean frame and idle clocks skip. The DOM fallback keeps its own identical behavior set for non-live contexts.

## Controls

Rectangular actions with separate arrow cells. No pills. The control language is an instrument panel, not a marketing button.

## Responsive rules

Desktop uses offsets, scroll parallax, and pointer tilt. ≤900px collapses records to one column, kills tilt and inner drift (`transform:none !important` on `.record` and children), keeps scroll shift. ≤620px tightens type. `html.motion-off` freezes tilt and drift and preserves layout offsets.

## Content boundary

The approved tagline is “Systems that show their work.” (supersedes “Controls for consequential AI.”, 2026-08-31). Project descriptions and evidence labels remain provisional until real source material is reviewed.
