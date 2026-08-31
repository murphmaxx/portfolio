# Motion / field asset plan

The background must become a real high-resolution industrial render before the first content pass. The intended asset is not a diagram and not a generic texture.

## Asset

`field-background.webp` — 2400×1350 minimum, 16:9, full-bleed.

## Visual content

Dark British racing green operations environment viewed from a shallow overhead angle. Matte composite panels, a central circular aperture, bronze alloy machined rings, Nardo grey markings, fine measurement ticks, sparse trajectories, physically plausible shadows, expensive aerospace/automotive finish, quiet negative space left-center for the tagline, detail weighted toward right and lower field.

## Production route

1. Generate or commission the render using `FIELD-BACKGROUND-PROMPT.md`.
2. Embed the exact generation prompt or source origin in the file metadata.
3. Add a poster/crop variant for mobile.
4. Replace `.field:before` atmosphere with the real image.
5. Preserve semantic text and project panels as HTML.
6. Use a slow transform/parallax layer, not a continuously animated video by default.
7. Add a static fallback for reduced motion and low-data contexts.

## Current limitation

The 21st.dev AI generation endpoint was called for three UI concept takes but returned `generation_limit_reached` and provided the upgrade URL `https://21st.dev/pricing`. It is useful for UI component mechanics and can be used again after the quota is available, but it did not generate the photographic background asset in this pass.
