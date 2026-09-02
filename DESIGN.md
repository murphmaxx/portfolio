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

## Media panes
- The card's right pane is a DEMO RENDER, never text: a live canvas diagram of the project's real mechanism, in-palette, seeded, scrubbed by scroll, idling gently. Honest diagrams only — no fake screenshots, no invented numbers; every labeled element corresponds to something the project actually does. Replaceable by real captured media without layout change.
- Text (description + claim readout) lives in the left column. Readout stays at 7 claim rows max.
- Pane motion grammar (Owen, 2026-09-01): the ouros TUI pane LOOPS on its own clock (GIF grammar — typing, gate, response). Transcript panes (crucible, eyeofrah) are SCROLL-SCRUBBED — a loop was tried for them and reverted same day; do not re-loop them.

## Motion grammar

- Camera: cursor parallax + scroll dolly, spring-damped (k=14, zeta=0.9). Every layer of the world shifts perspective together — this, not any single effect, is the basement feel.
- Card tilt (DOM, unchanged): keel/Codrops split, glide 0.16/frame in AND out — release is the same exponential settle, no rebound.
- The eye is a scene object with a STATION model (2026-08-31, user direction): whichever card covers the most viewport owns the eye (the hero owns it near the top). No blended in-between positions — the eye holds its station on lazy springs (k≈10–16, softly riding the card), and when majority ownership flips (hysteresis: challenger must beat the incumbent by 8% coverage, or the incumbent has left the screen) it DARTS: a ~220ms glance toward the destination, a gaze-evoked blink 75% of the time, then flight on a continuously blended stiffness (hold k 10–16 ↔ dart k 70–82, damping near-critical) that lands with one slight bounce (~8px, single cycle) and settles — no mode-switch snap. Stations are the cards' larger side gaps, sized to fit, clamped on-screen. The closing section is the final station: the eye centers in the field strip above the titanium plane, drops cursor-following, looks at the viewer (camera), one deliberate blink — then the plane covers it.
- Gaze: the whole eye assembly rotates toward the cursor's world point (quaternion slerp 0.055/frame). Idle saccades offset the look target on a 2.6–5.2s clock after 3.5s of pointer stillness. Iris revolves once per ~4 minutes; the eye bobs ±0.35 units on a 7.5s sine.
- Blink: two half-disc shutters in front of the socket; close 80ms, hold 110ms, open 170ms; random 4–9s cadence, 22% double.
- Self-protection: a frame-time watchdog degrades the live scene to the static fallback after ~3s under 25fps (post-warmup), flipping the masthead chip to 'Field / static'.
- Motion off / reduced motion: the main script broadcasts a `motionchange` event; the scene freezes on a clean frame and idle clocks skip. The DOM fallback keeps its own identical behavior set for non-live contexts.

## Wayfinding

A fixed record rail on the left edge (desktop only): entries 01–06, each an anchor to its card, lit by the same viewport-majority rule that owns the eye — the instrument and the index agree about where you are. Hidden in the hero and the closing (no majority owner).

## Controls

Rectangular actions with separate arrow cells. No pills. The control language is an instrument panel, not a marketing button.

## Responsive rules

Desktop uses offsets, scroll parallax, and pointer tilt. ≤900px collapses records to one column, kills tilt and inner drift (`transform:none !important` on `.record` and children), keeps scroll shift. ≤620px tightens type. `html.motion-off` freezes tilt and drift and preserves layout offsets.

## Content boundary

The approved tagline is “Systems that show their work.” (supersedes “Controls for consequential AI.”, 2026-08-31).

**Voice rule (Owen, 2026-09-02): NO EM-DASHES in shipped copy.** Periods, commas, colons, or the middot the instrument language already uses. Card descriptions read the way Owen writes: short sentences against long ones, contractions, plain words, a concrete claim rather than a polished summary, and first person where it belongs (it is his work). The two places an em-dash still appears are the captured panes, where the text is real output from ouros and crucible themselves, and the source comments. Never edit captured pane text to satisfy this rule; fix the tool and re-capture, or leave it.

Card content is REAL as of 2026-08-31 — every number measured from the repos on that date (LOC via `git grep -c ''`, test counts via `git grep -c '#[test]'`, descriptions distilled from each repo's README, paper terms from `ouros-mono/docs/paper/DRAFT.md`). The media panes are instrument readouts of those measurements, each with a `Surveyed <date>` tag — re-survey when the numbers drift. Public repos (grounded, eyeofrah, crucible → github.com/murphmaxx) link directly; private ones (ouros, canopy) and the paper draft route to mailto:omurphy@ourosproject.com. The client name behind grounded's first deployment and the red-team vendor's name stay OFF the site.
