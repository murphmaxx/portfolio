# Background / parallax interaction brief

## Scope and mode

Experience-mode homepage composition. This is a replacement of the current static dossier composition's homepage interaction, preserving the British racing green / bronze alloy / Nardo grey visual world and the approved tagline.

## Core experience

The visitor enters a full-viewport animated background that represents a living technical system: layered field, trajectory paths, and slow-moving depth planes. The tagline and short introduction sit above it. As the visitor scrolls, the background continues as a persistent visual substrate while project information boxes travel through it at different parallax rates.

## Visitor path

1. Arrival: background establishes atmosphere and system depth.
2. First scroll: hero text yields to the first project information box.
3. Continued scroll: project boxes enter from alternating depths and positions; each exposes project name, category, short thesis, evidence state, and action.
4. Transition: the background field changes state between project groups without becoming a new page.
5. Close: research artifact and contact settle into quieter foreground planes.

## Signature interaction

The page behaves as one continuous instrument. The animated background remains persistent; content boxes move through it, not inside a sequence of unrelated section cards. Each box has a different depth and entry timing, but all remain readable and keyboard-addressable.

## Motion plan

- Focal moment: background-to-foreground transition as the first project box crosses the hero field.
- Continuity: persistent field coordinates and scroll-linked depth preserve one spatial world.
- Feedback: hover/focus raises a box toward the reader and exposes its action affordance.
- Budget: CSS transforms plus one requestAnimationFrame scroll loop; no continuous WebGL until a real performance baseline exists.
- Reduced motion: freeze the field into a composed still and present boxes in normal document flow.

## Responsive rules

Desktop uses layered parallax planes and generous negative space. Tablet reduces depth range. Mobile uses a single background plane with short, controlled transforms and normal-flow project boxes; no content may depend on precise pointer placement.

## Constraints

The page must keep the racing green, bronze alloy, and Nardo grey palette. Do not revert to a flat capability matrix as the dominant homepage experience. Do not use generic floating cards as decoration; each box must represent a project record and contain real evidence fields once content is added.
