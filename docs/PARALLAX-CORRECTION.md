# Parallax correction — final interaction contract

The card effect is intentionally a whole-card pointer tilt, matching the Keel reference's middle-pane interaction rather than using scroll translation as a substitute.

## Rest state

- Every project card is flat at `0deg`.
- Cards do not have built-in rotation.
- Cards do not use a sticky stack.

## Pointer state

- Pointer movement over the card calculates normalized local coordinates.
- The full `.project-box` receives `rotateX()` and `rotateY()`.
- Maximum target is approximately 8–10 degrees.
- The card transitions with transform easing.
- Pointer leave returns both axes to zero.

## Scroll state

- Scroll changes only `--scroll-shift` translation.
- Pointer tilt and scroll shift are composed in one transform declaration.
- The card remains the moving plane, not only the media child.

## Background

- The previous vector/image background layers are removed from the page.
- The page uses the field background while the new render is being produced.
