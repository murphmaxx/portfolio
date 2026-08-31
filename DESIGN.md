# Technical portfolio — visual system

<!-- impeccable:design-schema 1 -->

## World

An expensive defense-industrial field interface with a continuous spatial substrate. British racing green is the environment. Bronze alloy is the measured signal. Nardo grey is the quiet closing plane. Project information travels through the field as technical records.

## Palette

- `--racing`: `#07130F` — persistent background field
- `--green`: `#0D2118` — project information boxes
- `--green-2`: `#153326` — elevated project field
- `--nardo`: `#B7B9B4` — closing/document surface
- `--white`: `#E8EBE6` — foreground
- `--muted`: `#A5AEA8` — secondary text
- `--line`: `#50665A` — structure
- `--bronze`: `#A8794D` — action and verification signal
- `--bronze-dark`: `#725333` — dark bronze on Nardo

## Composition

The hero is intentionally tall rather than a self-contained section. Its field remains fixed while the document scrolls. The first project box appears after the opening and travels through the same field. Project boxes alternate modest x/y offsets and rotations to create depth while preserving a stable reading order.

## Controls

Rectangular actions with separate arrow cells. No pills. Hover/focus changes the field and shifts the arrow a small distance. The control language is closer to an instrument panel than a marketing button.

## Motion grammar

- Focal moment: the first project record crossing from the hero into the persistent field.
- Continuity: one fixed background field across hero and project run.
- Feedback: project media trace resolves on hover/focus.
- Budget: one requestAnimationFrame scroll loop and CSS transforms only.
- Reduced motion: freeze field and present records without spatial transforms.

## Responsive rules

Desktop uses layered parallax planes and generous offsets. Tablet reduces offsets. Mobile collapses boxes into one column, removes rotation, retains the background field, and keeps every project action in normal document order.

## Content boundary

The approved tagline remains “Controls for consequential AI.” The previous label above the hero is removed entirely. Project descriptions and evidence labels remain clearly provisional until real source material is reviewed.
