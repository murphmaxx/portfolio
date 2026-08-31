# Project card motion contract

- Cards remain at `rotate(0deg)` in their resting state.
- Cards receive only scroll parallax translation.
- Pointer movement applies `rotateX` and `rotateY` to the entire project card, making the card itself the 3D plane.
- The media field and card contents inherit the plane; they do not own the primary tilt.
- Pointer tilt is capped at 4 degrees and eased with a spring-like cubic-bezier.
- Pointer leave returns the whole card to flat orientation.
- Touch and reduced-motion users receive no tilt.
- The persistent background remains independently positioned, so card movement reads against it.
