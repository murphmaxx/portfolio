# Operating Standards

## Purpose

This repository is the source of truth for a public technical portfolio. It must explain real work clearly without turning experimental or local projects into unsupported professional claims.

## Content rules

1. No final copy is added until the project facts, status, repository URL, and intended audience are reviewed.
2. Each project must distinguish working, verified, experimental, planned, and not-built capabilities.
3. Metrics require a reproducible source, method, date, and scope.
4. Limitations are part of the project story, not hidden in footnotes.
5. Private material, secrets, local paths, credentials, and unpublished research are never committed.
6. The portfolio may link to public repositories, but it does not duplicate their entire documentation.

## Design rules

1. The primary surface is **Decide / Learn**: one clear idea per section, with evidence leading the visual hierarchy.
2. The site must not collapse into a generic centered hero plus equal feature tiles.
3. Use one restrained accent family per direction. Avoid default indigo gradients, decorative glass, and invented dashboard metrics.
4. Type, spacing, and composition carry hierarchy before borders, icons, or ornament.
5. Every motion sequence must explain a transition, a system relationship, or a state change.
6. `prefers-reduced-motion` must disable nonessential movement.
7. Interactive targets are at least 44px on touch layouts. Body text stays comfortably readable on a 1280px laptop viewport.

## Technical standards

- Prefer a static site deployable by GitHub Pages.
- Keep content data separate from layout and theme tokens.
- Pin dependency versions.
- Avoid a backend unless a demonstrated requirement appears.
- Run build, link, accessibility, and responsive checks before publication.
- Optimize media. Provide poster images, captions or transcripts where appropriate, and reduced-motion alternatives.
- No analytics or third-party embeds by default.

## Release gates

A public release requires:

- [ ] Every visible claim has a source or is clearly marked draft.
- [ ] Repository links resolve to the intended public project.
- [ ] Project status and limitations are accurate.
- [ ] All primary routes work on desktop and mobile widths.
- [ ] Keyboard navigation and visible focus states work.
- [ ] Reduced-motion behavior is tested.
- [ ] No secrets or private paths are present.
- [ ] Build and link checks pass.
- [ ] The rendered site has been reviewed visually before publishing.

## Change process

1. Explore visually before locking the direction.
2. Lock tokens and composition before adding content.
3. Add one project page as the reference implementation.
4. Verify it against the release gates.
5. Propagate the system to the remaining projects.
6. Publish only after explicit review and approval.

## Demo-video standards

- Capture real software whenever possible.
- Use motion graphics to clarify, not fabricate, product behavior.
- Keep a short version for social distribution and a longer technical walkthrough when warranted.
- Record the exact software version and environment for each capture.
- Store source project files and a reproducible render command alongside exported media.
- Never imply a feature exists solely because it appears in an animation.
