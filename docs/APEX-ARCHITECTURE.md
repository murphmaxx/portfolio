# Apex Site Architecture

## Surface model

Experience-first portfolio with a single cinematic entry, then a scroll-controlled sequence of work, research, and contact. It is not a conventional résumé grid.

## Route model

- `/` — kinetic landing sequence and selected work index
- `/projects/<slug>` — full project case file with hero media, system anatomy, evidence, limitations, repository, and demo
- `/writing/<slug>` — research artifact and paper reading surface
- `/contact` — concise contact and external links

## Homepage sequence

1. **Drive** — full-screen kinetic thesis, orbit/trace field, work counter, scroll cue.
2. **Signal** — a short statement of the technical territory, with one concrete system visualization.
3. **Project run** — pinned/sticky project sequence. Each project owns one large media frame and one compact evidence rail.
4. **Trace** — relationship view connecting execution governance, control surface, local inference, interpretability, and measurement.
5. **Writing** — paper/artifact treatment with a large cover or typographic frame.
6. **Contact** — a strong final field, not a form-heavy footer.

## Interaction primitives

- Magnetic or proximity-responsive display type, desktop only and disabled for reduced motion.
- Orbit/trace canvas or SVG field tied to scroll progress.
- Scroll-pinned project frames with synchronized text and media.
- Shared-element expansion from project frame to case-file route.
- Horizontal marquee for technology/evidence tags only where it improves scanning.
- Keyboard-accessible project controls and URL-addressable states.
- Touch layouts become vertical sequences; no interaction is hover-dependent.

## 21st.dev candidates to adapt

- Quordix Work Hero: full-screen hero, magnetic letters, orbit rings, scroll fade.
- Interactive Video Portfolio Scroller: synchronized vertical video and typography.
- Immersive Scroll Gallery: depth through scroll scaling.
- Stacking Cards / Scroll Cards: pinned project progression.
- Infinite Moving Cards / Marquee: controlled evidence or tool rails.
- Cursor Driven Particles Typography: optional hero experiment, only if performance and reduced-motion fallback remain excellent.
- Hero Carousel: possible project-media filmstrip on detail routes, not the primary homepage structure.

## Implementation boundary

The first production implementation should use Astro or static HTML/CSS/JS with a small client-side motion layer. Use CSS and SVG before WebGL. Use Motion/Framer Motion only if the project moves to React/Astro islands and the interaction earns the dependency. Keep the portfolio statically deployable.

## Media strategy

Project media is authored from real software captures. Motion graphics may frame or explain a real behavior but may not imply an unbuilt capability. Every video has a poster, caption/transcript path, reduced-motion still, source project, and render metadata.
