# PLAN/STATE.md — portfolio

**The live snapshot.** Branch, what builds, what is broken, what is next.
Committed with the code, so it cannot drift the way an external note can.

Migrated out of global agent memory on 2026-09-02. Everything below was written
in a working session and reflects what was true when written — verify against
the code before acting on it. Dates are absolute.

---


## portfolio-site-state

<!-- migrated from ~/.claude/.../memory/portfolio-site-state.md -->

---
name: portfolio-site-state
description: "Owen's portfolio site (~/Developer/portfolio) — read HANDOFF.md in-repo first; NO-EM-DASH voice rule + the /portfolio/ URL fix pending merge; keel-tilt lesson lives here too"
metadata: 
  node_type: memory
  type: project
  originSessionId: 88c6d1b8-1915-42a0-bc49-76d81d188ee2
  modified: 2026-09-02T17:38:53.087Z
---

Owen's public portfolio is **LIVE at https://murphmaxx.github.io/portfolio/**. Repo `/Users/murph/Developer/portfolio`, remote murphmaxx/portfolio. The in-repo `HANDOFF.md` is the live state doc, read it before working there; `DESIGN.md` is the visual contract (pane motion grammar: ouros TUI pane LOOPS, transcript panes SCRUB, a loop for those was tried and reverted). Shipped: live three.js field + station-committed eye w/ closing send-off, six cards whose media panes all carry REAL captured evidence.

**VOICE RULE (Owen, 2026-09-02): no em-dashes in shipped copy, and the copy reads the way he writes.** Now in DESIGN.md's content boundary. Applied across the site (31 replacements: meta/title/og, hero, stage sub, all six card descriptions rewritten, readout values, evidence lines, pane tags, mobile note, footer, 3 canvas labels). The 31 em-dashes still in `site/index.html` are source comments plus **real captured output from ouros and crucible themselves** (ouros' boot banner, crucible's "P3 size (statements — the baseline)"). Those are evidence behind a "Real session, replayed" tag: NEVER edit pane text to satisfy the style rule. To lose them, fix the string upstream in ouros/crucible and re-capture (crucible is cheap and deterministic; ouros is the pty ritual in HANDOFF).

**SHIPPED 2026-09-02.** main = a7302a3, pushed, deploy green. `https://murphmaxx.github.io/portfolio/` now returns 200 with **zero redirects**; old `/portfolio/site/index.html` is 404. The 21-check browser harness passes against the production URL. Review board: https://claude.ai/code/artifact/08be1644-7948-4494-afb5-3d389cc93a03

**Pages is now `build_type: workflow` (GitHub Actions), not the legacy branch build.** The legacy build serves the repo root regardless of what the workflow uploads, so it had to be flipped via `gh api -X PUT repos/murphmaxx/portfolio/pages -f build_type=workflow`. Flip FIRST then push: the last Actions artifact still holds the old root during the flip, so there is no 404 window.

The URL fix: the address bar read `/portfolio/site/index.html` because the repo root held a meta-refresh redirect into `site/`. Fixed by publishing `site/` AS the Pages root (`pages.yml` uploads `path: site`, root `index.html` deleted, `.nojekyll` moved into `site/`, og:image absolute URL dropped its `/site` segment). Side effect: `designs/`, `docs/`, `motion/` and HANDOFF stop being served at the portfolio URL. Preview command changed accordingly: serve `.../portfolio/site` and open `/`.

Transferable lesson: for pointer-tilt cards, never rotate the element that supplies `getBoundingClientRect` for the pointer math, the projected rect warps as it tilts and the effect collapses toward one corner. Keel/Codrops split: stationary listener wrapper, rotating inner stage. Reference implementation: `~/Developer/development/keel/site/proto/dual-tilt.html`.

Browser QA: Chrome stable is gone from the Mac and the chrome-devtools MCP fails to launch. `npm i puppeteer-core` into a scratch dir + the cached Chrome for Testing at `~/.cache/puppeteer/chrome/mac_arm-152.../Google Chrome for Testing.app/...` works; launch with `--use-angle=swiftshader --enable-unsafe-swiftshader` for the WebGL scene. Under swiftshader the site's frame-time watchdog correctly degrades the scene to 'Field / static' partway through a long run: that is the designed self-protection, not a regression. [[human-voice-writing-directive]] [[mac-clean-slate-wipe-plan]] [[keel-umbrella-org]]


---
