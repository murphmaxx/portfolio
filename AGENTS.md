# AGENTS.md — portfolio

## What This Is

Owen Murphy's technical portfolio. A single static page with a live three.js
field behind it. Published to GitHub Pages from `site/`, served at
`/portfolio/`.

`site/index.html` is the whole site.

## Plan & State

**Read `PLAN/STATE.md` at session start.** It is the live snapshot: branch,
what builds, what is broken, what is next. It is committed with the code, so it
cannot drift from the repo the way an external note can.

- `PLAN/STATE.md` — current snapshot
- `PLAN/DECISIONS.md` — architectural decisions, with the why

## Setup Commands

No build step. Open `site/index.html`, or serve the directory:

```bash
python3 -m http.server -d site 8000
```

Verification is visual: load the page and screenshot rendered pixels. In live
mode the scene exposes `window.__scene` — `eye()`, `cam()`, `blinkCount()`,
`spin()`, `shut()` — and a harness asserts against that API rather than CSS
variables.

## Layout

| Path | What it owns |
|---|---|
| `site/index.html` | The entire site: markup, styles, scene script, main script. |
| `site/assets/` | Images and static assets. |
| `DESIGN.md` | The visual contract: world, palette, tokens, rules. |
| `PRODUCT.md` | What the site is for. |
| `motion/` | Archived terrain and eye generators. Keep in sync when art-directing. |
| `content/`, `designs/`, `docs/` | Source material and notes. |

## Laws

1. **`site/` is the published root.** Pages builds from it via workflow, not the
   legacy branch build. Files outside `site/` are not served.

2. **The scene is progressive enhancement, and the fallback must stay intact.**
   The scene script runs before the main script, gated to desktop fine-pointer
   above 900px with WebGL. On boot it sets `window.__sceneLive` and `.field.live`
   to hide the static layers. Mobile, coarse-pointer, no-WebGL and JS-off all
   fall back to pre-rendered stills plus DOM eye behaviour, guarded by
   `!window.__sceneLive`. Do not remove a fallback path to simplify the scene.

3. **The eye commits to one station; it never blends between them.** Blending
   was tried first and read as lifeless hovering between screens. `pickStation()`
   picks a viewport-coverage majority with hysteresis, then the eye darts to that
   station's gap point. Never average two station targets.

4. **The eye renders as a second pass with the depth buffer cleared** — its own
   scene and light rig, the same camera. This is why terrain can never clip it.
   Rendering it in the main pass reintroduces the half-buried-eye bug by
   construction.

5. **Site copy carries no em-dashes.** This applies to prose the site ships, not
   to `DESIGN.md` or other repo documents, which use them freely. Never rewrite
   captured pane text to satisfy the rule.

## Retrieval

- **Where does X live** — this file, then `PLAN/STATE.md`. Free.
- **Known string** — search it. WARNING: the shell `grep` is a function routing
  to `ugrep -I`; one NUL byte makes it skip a file SILENTLY (empty output,
  exit 1, indistinguishable from a real no-match). Re-check negatives with
  `/usr/bin/grep`.
- **Intent-shaped question** — `mon`, which returns ranked anchors with a
  graph-derived reason instead of a match dump.

## Don't

- Don't publish from anywhere but `site/`.
- Don't remove a non-WebGL fallback path.
- Don't blend eye station targets.
- Don't put an em-dash in shipped site copy.
