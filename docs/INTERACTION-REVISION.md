# Technical portfolio — interaction revision

The homepage now follows the original experience brief rather than the previous dossier layout.

## Core interaction

- One persistent full-screen British racing green field remains behind the page.
- The field contains restrained mesh, contour, and marker layers.
- Scroll changes the field's depth, scale, rotation, and marker position.
- Text sits in the foreground over the field.
- Project records move through the field at different parallax offsets.
- Project records are intentionally information boxes, not generic cards.
- Each record has project identity, system boundary, evidence path, media field, and action.
- The closing surface uses Nardo grey as a quieter foreground plane.

## Motion thesis

The field is the spatial continuity of the portfolio. Project boxes are objects moving through that field. Scroll is therefore a meaningful inspection control rather than a trigger for unrelated reveal animations.

The implementation uses requestAnimationFrame-throttled scroll updates and CSS transforms. The field does not require WebGL or a runtime dependency yet. Reduced motion freezes the field and leaves all content in normal readable flow.

## Visual identity

- British racing green owns the background.
- Bronze alloy marks active points, links, and evidence paths.
- Nardo grey is reserved for the closing/document surface.
- No cyan, purple, neon-lime, gradients, glows, pills, or playful controls.

## 21st.dev inspiration used as mechanics

- Immersive Scroll Gallery: visual depth and scroll-linked scale.
- Interactive Video Portfolio Scroller: text/media synchronization model for future real demos.
- Stacking Cards / Scroll Cards: depth ordering and continuous project progression.
- Origin UI animated-arrow button: adapted into rectangular technical actions rather than capsules.

The source components are references, not copied production dependencies.
