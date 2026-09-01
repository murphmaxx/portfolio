# Portfolio Handoff

Updated 2026-08-31. Supersedes the previous handoff (the tilt bug, the retired CSS background, and the old hero/palette are all resolved below).

## State

**LIVE SCENE (2026-08-31, basement.studio direction):** the background is now an in-page three.js world (terrain + 3D eye + cursor-parallax camera), not a static render. The user explored basement.studio ("the site is a place") and asked for that mechanism. Key architecture:

- Scene script sits BEFORE the main script in `site/index.html`, gated to desktop fine-pointer >900px + WebGL; on boot it sets `window.__sceneLive` and `.field.live` (hides static layers). Everything else (mobile/coarse/no-WebGL/JS-off) falls back to the pre-rendered stills + DOM eye behaviors, which are kept intact and guarded by `!window.__sceneLive`.
- The main script broadcasts motion toggles via a `motionchange` CustomEvent; the scene listens (initial state synced because setMotion always fires once at load).
- Eye targets are computed in screen space (same gap-weave logic as the DOM fallback) then unprojected onto the eye's depth plane (z=14) through the CURRENT parallaxed camera each frame; springs smooth world position/scale (underdamped x vs y = curved organic travel — the user asked for "more organic").
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

25/25 checks (live-scene edition): load, flat at rest, eye layers load, gaze looks toward cursor on both sides + centers under motion-off, scene boots, camera parallax follows cursor (±5 world units), eye rotates bodily toward cursor, iris spins, idle saccades, blink shutters close fully, world-space scroll-weave (eye in the gaps at card height, home at top), scene freezes under motion-off, four corners at settled linear values (±5.64°/±9.4° at 3% inset), entry-glide/no-snap (2 frames after edge crossing = ~40% of settled tilt), full-body sweep incl. text and media areas, children translate-only (no text stretch), elastic return to 0 after leave, scroll-while-hovering preserves tilt and updates shift, motion toggle off/on, reduced-motion starts off, coarse pointer gets no tilt, no console errors. Screenshots reviewed at desktop and 390px mobile. Harness lived in the session job dir (not committed); it drove real `page.mouse.move` across card geometry and read back the CSS vars.

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

- Project links (`Inspect` actions) still point at `#`; real repository/demo URLs pending.
- Contact action target pending.
- Project descriptions/evidence labels remain provisional until real source material is reviewed.
- Publishing (GitHub Pages) awaits the user's go.

## Git discipline

Do not push unless the user asks. Before any commit: `git diff --check`, and `node --check` on the extracted inline script. Never claim browser verification from source inspection alone.
