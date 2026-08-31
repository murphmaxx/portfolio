# Technical Portfolio — Design System

<!-- impeccable:design-schema 1 -->

## World

An expensive, direct defense-industrial technical dossier. The portfolio communicates engineering seriousness through restraint, precision, documentary media, and explicit system boundaries. It avoids consumer-tech playfulness, decorative futurism, neon, glass, pill-heavy interfaces, and campaign effects that obscure technical evaluation.

## Palette

- `--carbon`: `#0C0F10` — primary background
- `--steel`: `#151A1C` — technical field
- `--steel-2`: `#1D2325` — raised section field
- `--fog`: `#E7E9E5` — primary foreground
- `--paper`: `#F3F3EF` — capability and document surface
- `--ink`: `#151819` — dark ink on paper
- `--muted`: `#9DA4A1` — secondary technical text
- `--line`: `#41494A` — structural linework
- `--bronze`: `#AA8963` — selected action and evidence signal
- `--bronze-dark`: `#6E5941` — paper-surface accent
- `--danger`: `#A65145` — reserved semantic warning

## Typography

- Barlow Condensed — restrained technical display, weights 500–700
- Archivo — body and interface text
- DM Mono — system labels, state, identifiers, and evidence metadata

Display weights and sizes are reduced from the prior campaign-style direction. Body text stays at 15–16px with extended line height and controlled measure.

## Composition

- Restrained 72px masthead on a strict grid.
- Two-part opening: direct positioning statement and large technical system field.
- Capabilities use a procurement-readable matrix.
- Projects use full-width technical records rather than floating or sticky cards.
- Writing is treated as a formal document artifact.
- Contact is one direct close.

## Controls

- Rectangular bordered actions with separate arrow cells.
- No capsule or pill buttons.
- No traveling fills, bounce, magnetic behavior, or decorative cursor.
- Hover inverts the action field; arrow moves two pixels to confirm direction.
- Minimum 44px targets and explicit focus outlines.

## Motion grammar

Motion is almost absent. Scroll changes only two explanatory diagrams:

- the hero system ring expands by at most 7%;
- project evidence traces resolve horizontally as records enter the viewport.

All movement is transform-based, requestAnimationFrame-throttled, manually disableable, and removed for reduced-motion preference. No looping decorative animation remains.

## Responsive rules

- Hero moves from two columns to one at tablet width.
- Capability matrix becomes two columns, then one.
- Project records preserve number, title, media, and action order.
- Navigation removes lower-priority links only at narrow phone widths.
- Media and document frames retain their intended ratios.

## Content boundary

Final claims, capability language, contact information, media, status, and metrics remain subject to evidence review. The current wording is structural draft copy, not published representation.
