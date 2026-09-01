# Portfolio Handoff

Updated 2026-08-31. Supersedes the previous handoff (the tilt bug, the retired CSS background, and the old hero/palette are all resolved below).

## State

`site/index.html` is the whole site. As of this revision:

- **Hero tagline:** “Systems that show their work.” (replaced “Controls for consequential AI.” at the user's request, 2026-08-31).
- **Color scheme:** carbon graphite / steel / signal orange / titanium closing plane (replaced British racing green + bronze + Nardo). Tokens and rules in `DESIGN.md`.
- **Background:** a real render at `site/assets/field-render.jpg` — seeded deterministic three.js terrain, generator archived at `motion/render-field-generator.html` (open in headless Chromium at 2560×1440, screenshot, `sips` to JPEG). The CSS mesh/trace/marker field is gone; `motion/field-background.svg/.webp` stay retired and unreferenced.
- **The Eye (2026-08-31):** a cyber Eye of Ra over the terrain whose iris follows the cursor. Two renders from one camera in `motion/render-eye-generator.html` — `site/assets/eye-frame.png` (static: lids, dark socket, Ra marks, reticle) and `site/assets/eye-iris.png` (machined turbine iris, transparent) — overlaid at identical size in `.field .eye`. A window-level pointermove maps the eye-center→cursor vector to iris translate (≤3.2% of the box) + rotateY/rotateX swivel, gliding at 0.09/frame; motion-off/reduced/coarse center it. Do NOT size the iris img to the iris' drawn fraction — both PNGs share the full canvas; sizing must stay 100% or the iris shrinks quadratically (made and fixed 2026-08-31). On ≤900px the eye moves to ~46vh so it doesn't sit behind the headline.
- **Card tilt:** works across the entire card. Model is keel/Codrops TiltFx: stationary `.project-box` (layout offset + scroll shift + perspective + pointer listeners) wrapping a rotating `.record` (±6°/±10°). The pointer sets a linear TARGET; a rAF loop glides the card toward it (GLIDE=0.16/frame) so entering at an edge never snaps (user-reported 2026-08-31, fixed same day), then tracks 1:1. 2D counter-drift on inner planes, elastic JS release (~900 ms), no CSS transform transition. The root cause of the old “stuck at top left” class of bug: the rotation lived on the same element that supplied `getBoundingClientRect` for pointer math, so the projected rect warped as the card tilted. Keep rotation and pointer geometry on separate elements.

## Verified 2026-08-31 (real browser, headless Chromium 152 via puppeteer-core)

21/21 checks: load, flat at rest, eye layers load, gaze looks toward cursor on both sides + centers under motion-off, four corners at settled linear values (±5.64°/±9.4° at 3% inset), entry-glide/no-snap (2 frames after edge crossing = ~40% of settled tilt), full-body sweep incl. text and media areas, children translate-only (no text stretch), elastic return to 0 after leave, scroll-while-hovering preserves tilt and updates shift, motion toggle off/on, reduced-motion starts off, coarse pointer gets no tilt, no console errors. Screenshots reviewed at desktop and 390px mobile. Harness lived in the session job dir (not committed); it drove real `page.mouse.move` across card geometry and read back the CSS vars.

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
