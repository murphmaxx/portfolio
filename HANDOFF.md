# Portfolio Handoff

Updated 2026-08-31. Supersedes the previous handoff (the tilt bug, the retired CSS background, and the old hero/palette are all resolved below).

## State

**LIVE SCENE (2026-08-31, basement.studio direction):** the background is now an in-page three.js world (terrain + 3D eye + cursor-parallax camera), not a static render. The user explored basement.studio ("the site is a place") and asked for that mechanism. Key architecture:

- Scene script sits BEFORE the main script in `site/index.html`, gated to desktop fine-pointer >900px + WebGL; on boot it sets `window.__sceneLive` and `.field.live` (hides static layers). Everything else (mobile/coarse/no-WebGL/JS-off) falls back to the pre-rendered stills + DOM eye behaviors, which are kept intact and guarded by `!window.__sceneLive`.
- The main script broadcasts motion toggles via a `motionchange` CustomEvent; the scene listens (initial state synced because setMotion always fires once at load).
- Eye movement is a STATION model (user: "majority of the screen shows a certain card → eye in a certain position", plus "make it feel alive"): pickStation() runs per frame — viewport-coverage majority with hysteresis (+8% to dethrone, or incumbent <4%) — and the eye COMMITS to one station's gap point (unprojected to z=14 through the current parallaxed camera). Station change triggers a dart: glance-toward-destination (~220ms, faster slerp), 75% gaze-evoked blink, stiff springs (k 70/84) for ~550ms flight with ~1% overshoot, then lazy hold springs (k 10–16). Never blend station targets — blending was tried first and read as lifeless hovering between screens (user caught it). Motion profile verified by 90ms-interval trace.
- The eye renders as a SECOND PASS with the depth buffer cleared (own THREE.Scene + own light rig, same camera): terrain can never clip it — user hit half-buried-eye at gap positions where the world position lands inside the ridge walls (fixed 2026-08-31, by construction). Boot cross-fades canvas over the stills (.9s) after the first rendered frame; the masthead chip flips to 'Field / live'.
- Blink = two half-disc shutter meshes (scale.y state machine). Gaze = whole-assembly quaternion slerp toward the cursor ray. Iris spin/bob/saccades in-scene.
- Debug/verification API: `window.__scene` — `eye()` (projected screen pos, scale, rotY/rotX), `cam()`, `blinkCount()`, `spin()`, `shut()`. The harness asserts against this, not CSS vars, in live mode.
- Terrain/eye geometry duplicated from the archived generators in `motion/` — keep them in sync when art-directing.

`site/index.html` is the whole site. As of this revision:

- **Hero tagline:** “Systems that show their work.” (replaced “Controls for consequential AI.” at the user's request, 2026-08-31).
- **Color scheme:** carbon graphite / steel / signal orange / titanium closing plane (replaced British racing green + bronze + Nardo). Tokens and rules in `DESIGN.md`.
- **Background (v2, 2026-08-31):** a real render at `site/assets/field-render.jpg` — seeded three.js valley between two ridge systems, warm horizon, elevation-graded wireframe, round dust motes. Generator archived at `motion/render-field-generator.html` (headless Chromium 2560×1440, screenshot, `sips` to JPEG). The CSS mesh/trace/marker field is gone; `motion/field-background.svg/.webp` stay retired and unreferenced.
- **The Eye (v2, 2026-08-31, revised same day):** pure 3D, flourishes removed (no Ra marks/reticle/brow/lashes; the glint pass was tried and CUT — user verdict). TWO renders from one camera in `motion/render-eye-generator.html` — `site/assets/eye-frame.png` (thick machined lids, canthus caps, concave socket bowl — mind the lathe orientation: `rotation.x=+Math.PI/2` and DoubleSide, or the bowl renders convex and occludes the iris) and `site/assets/eye-iris.png` (domed turbine barrel) — overlaid at identical size in `.field .eye`. Blink is real lids again (a canthus-to-canthus horizontal sweep was tried and CUT — reads as a wipe, not a blink): asymmetric top/bottom close, `.lids.closed`, ~140ms hold. Scroll-WEAVE (the user's actual intent for "moves with you"): the eye slides left/right into the open space beside the passing card — side derived from each card's LIVE rect (never a static index table; `.stage-heading` makes nth-of-type(N) hit card N−1), centered in the gap at the card's height, gap-fitted scale clamped 0.24–0.62 and always fully on-screen, squared proximity-weight blend, hero pulls home. Desktop only. A window-level pointermove maps the eye-center→cursor vector to iris translate (≤3.2% of the box) + rotateY/rotateX swivel, gliding at 0.06/frame; motion-off/reduced/coarse center it. Idle life (2026-08-31): random saccades after 3.5s of pointer stillness (also on touch), a 4-minute CSS iris spin + 7.5s bob, and a randomized 4–9s mechanical-shutter blink (`.lids`, two steel-edged halves over the socket; forced-closed screenshot verified). DOM inside `.eye-inner`: frame img → `.iris-gaze` (gaze transform lives here, NOT on the img — the img carries the spin animation, and spinning inside the gaze keeps saccade directions in screen space) → `.lids`. Do NOT size the iris img to the iris' drawn fraction — both PNGs share the full canvas; sizing must stay 100% or the iris shrinks quadratically (made and fixed 2026-08-31). On ≤900px the eye moves to ~46vh so it doesn't sit behind the headline.
- **Card tilt:** works across the entire card. Model is keel/Codrops TiltFx: stationary `.project-box` (layout offset + scroll shift + perspective + pointer listeners) wrapping a rotating `.record` (±6°/±10°). The pointer sets a linear TARGET; a rAF loop glides the card toward it (GLIDE=0.16/frame) so entering at an edge never snaps (user-reported 2026-08-31, fixed same day), then tracks 1:1. 2D counter-drift on inner planes, elastic JS release (~900 ms), no CSS transform transition. The root cause of the old “stuck at top left” class of bug: the rotation lived on the same element that supplied `getBoundingClientRect` for pointer math, so the projected rect warped as the card tilted. Keep rotation and pointer geometry on separate elements.

## Verified 2026-08-31 (real browser, headless Chromium 152 via puppeteer-core)

27/27 checks (live-scene edition): load, flat at rest, eye layers load, gaze looks toward cursor on both sides + centers under motion-off, scene boots, camera parallax follows cursor (±5 world units), eye rotates bodily toward cursor, iris spins, idle saccades, blink shutters close fully, world-space scroll-weave (eye in the gaps at card height, home at top), station commitment at the 50/50 boundary between cards (eye AT a station, never midway), record rail shows exactly one lit entry under a majority owner, scene freezes under motion-off, four corners at settled linear values (±5.64°/±9.4° at 3% inset), entry-glide/no-snap (2 frames after edge crossing = ~40% of settled tilt), full-body sweep incl. text and media areas, children translate-only (no text stretch), elastic return to 0 after leave, scroll-while-hovering preserves tilt and updates shift, motion toggle off/on, reduced-motion starts off, coarse pointer gets no tilt, no console errors. Screenshots reviewed at desktop and 390px mobile. Harness lived in the session job dir (not committed); it drove real `page.mouse.move` across card geometry and read back the CSS vars.

## Preview

```
python3 -m http.server 4174 --bind 127.0.0.1 --directory /Users/murph/Developer/portfolio
http://127.0.0.1:4174/site/index.html
```

Kill stale servers on 4174 first (`lsof -nP -i :4174`) — a hung old instance returning empty responses has burned sessions before.

## Repository

- Local: `/Users/murph/Developer/portfolio` · Remote: `https://github.com/murphmaxx/portfolio` · Branch: `main`
- GitHub Pages intentionally not enabled yet.
- Chrome (stable) is not installed on this machine; use the puppeteer-cached Chrome for Testing at `~/.cache/puppeteer/chrome/` for any browser QA.

## Open items

- CONTENT IS REAL (2026-08-31): descriptions from the repos' own READMEs, media panes are measured readouts (LOC/tests/commits surveyed that day — see DESIGN.md content boundary for the measurement method), public repos linked (murphmaxx/grounded·eyeofrah·crucible), private ones (ouros, canopy) + the Cost of Asking draft route to omurphy@ourosproject.com mailtos. Card geometry changed to `min(100% - 10vw, 1240px)` with offsets capped ±5vw — the old full-width+offset cards silently overflowed the viewport at 1440 and truncated the new readout values.
- READOUT ROW RULE (user, 2026-08-31, 3rd pass — supersedes the "fuller" pass): every row must state a GUARANTEE, a MEASUREMENT, or a DESIGN DECISION WITH A CONSEQUENCE that an outside reader can evaluate. No inventory rows (module lists, file names, "App / glass", "Docs / …") — the user called those information filler, and they were. Current sets are 7–9 rows each, phrased as claims ("no audit record, no effect", "zero egress — nothing leaves", "3 dependencies, total"), still every one verified against the repos.
- 2026-08-31 enrichment (2nd pass, superseded): readouts were full spec sheets — 10–12 verified rows each (ouros: PDP/Cedar/Merkle/egress/class-A/delegation/AIVS/docs; canopy: 6 named crates + canopyd daemon + canopy-viz scanner + glass app; grounded: all 10 engine modules + harness; eyeofrah: module map + tooling; crucible: 3 deps + syn AST + spans + MIT; paper: prior-art regime + both signs + threshold). Values wrap on narrow panes (flex-wrap). Earlier pass: closing blurb under "Inspect the work. Then decide." removed; left-edge RECORD RAIL added (01–06, lit by the same viewport-majority rule as the eye, anchors to #rec-N card ids, hidden ≤900px, runs independent of the motion toggle); meta description + OpenGraph tags (og:image points at https://murphmaxx.github.io/portfolio/... — FIX if the published domain differs); orange-eye SVG favicon; instrument-styled scrollbar.
- 2026-08-31 motion polish: card release rebound REMOVED (release now rides the same 0.16 glide as entry — the elastic tween is gone); dart arrival smoothed (spring stiffness blends on a continuous mode factor 10↔70, damping near-critical 0.94/0.97 — no hard dart/hold switch, no overshoot; re-traced monotonic). Closing gained the identity line (Owen Murphy · github.com/murphmaxx · email); footer left span is now the show-its-work link to this public repo.
- Remaining: media panes could later carry real imagery/demos on top of the readouts; wide-viewport (1512/2560) screenshot pass; per-project detail pages if ever wanted; the closing section's eye send-off; a frame-time watchdog that drops to the static fallback on weak GPUs.
- Publishing (GitHub Pages) awaits the user's go.

## Git discipline

Do not push unless the user asks. Before any commit: `git diff --check`, and `node --check` on the extracted inline script. Never claim browser verification from source inspection alone.
