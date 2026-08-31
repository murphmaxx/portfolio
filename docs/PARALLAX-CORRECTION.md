# Parallax correction

The previous implementation exposed a source-level parallax variable but did not reliably apply visible motion because the panel transform declaration was duplicated during iterative edits and the scroll loop was duplicated in the inline script.

This correction makes the interaction explicit:

- each `.project-box` receives a measurable `--scroll-shift` value;
- the value is applied in the panel transform;
- the panel transform is the only transform owner for its depth movement;
- the fixed background remains independently translated;
- mobile removes the lateral depth offsets for a stable reading path;
- the source script declares `boxes` once before `setMotion()` is called.

The effect should be judged visually with the preview open, not from the stylesheet alone.
