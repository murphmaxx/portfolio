# Apex Homepage — Design System

<!-- impeccable:design-schema 1 -->

## World

A high-energy, evidence-led technical portfolio. The interface feels like an authored inspection instrument: midnight aubergine stage, acid chartreuse signals, parchment reading surfaces, coral editorial interruptions, contour paths, hard-edged media stages, and forceful condensed typography.

## Palette

- `--canvas`: `#120D19` — midnight aubergine stage
- `--surface`: `#1D1429` — primary elevated field
- `--surface-2`: `#2B1C3B` — dense project field
- `--paper`: `#F3EDDC` — warm readable surface and foreground
- `--ink`: `#17101E` — text on bright fields
- `--signal`: `#D7FF45` — acid chartreuse action, focus, and active state
- `--signal-dark`: `#91AB24` — chartreuse support role
- `--coral`: `#FF765F` — writing/editorial field
- `--muted`: `#B9AFC5` — secondary text on dark surfaces
- `--line`: translucent parchment — structural rules

## Typography

- Barlow Condensed — display voice, oversized and compressed
- Archivo — body and interface voice
- DM Mono — telemetry, metadata, state, and evidence labels

## Composition

- Full-screen first viewport.
- Left-anchored statement rather than centered résumé copy.
- Compact fixed utility navigation.
- Strong field changes between sections.
- Project work presented as a pinned sequence rather than equal cards.
- Media stages are structural and large; chrome remains sparse.

## Button system

Adapted from the 21st.dev Origin UI animated-arrow button anatomy:

- pill-shaped text and circular arrow well
- action fill travels across the capsule on hover/focus
- arrow translates and rotates to acknowledge intent
- shared `.button`, `.button--compact`, and `.button--ghost` variants
- minimum 44px target
- explicit focus ring
- motion toggle uses the same component language

## Motion grammar

- The focal motion is scroll-coupled inspection: contour paths rotate and translate as the visitor enters the work.
- Project media frames uncover as they approach, while trace nodes move along a line.
- Buttons provide bounded action feedback.
- Only the scroll cue loops, and it stops for reduced motion or manual motion-off.
- The cursor ring is desktop-only and decorative.
- No content begins hidden; failed scripts preserve the full experience.
- Motion has manual off and `prefers-reduced-motion` states.

## Responsive rules

- Mobile turns split compositions into one reading column.
- Sticky cards use a compact shared top offset and remain readable.
- Cursor interaction disappears on coarse pointers.
- Navigation retains essential work through the button while secondary text links collapse.
- Display type scales fluidly.

## Current boundary

This system describes the refined prototype. Final copy, imagery, video, and routes still require evidence review. Real media should replace abstract stages without changing this composition or interaction grammar.
