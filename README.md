# Portfolio Repository

A GitHub Pages portfolio system for technical projects, research, and production demos.

## Status

Scaffold and design exploration only. Public-facing content, project claims, and publication status are intentionally not finalized.

## Principles

- Evidence before assertion.
- Projects remain projects; no inflated titles or unsupported claims.
- Every project page states its status, boundaries, and verification.
- Motion explains systems; it does not decorate them.
- The site remains static, portable, and easy to maintain from GitHub.
- No secrets, private documents, credentials, or unverified metrics enter this repository.

## Planned architecture

- Static GitHub Pages site.
- Component-based frontend with content separated from presentation.
- Project records stored as structured local data.
- Dedicated project routes rather than modal-only detail views.
- Reusable motion-demo pipeline, likely Remotion plus real product capture.
- Accessibility, reduced motion, responsive layouts, and performance budgets treated as release criteria.

## Design explorations

Open `designs/index.html` locally to review the five no-content design directions.

The mockups are deliberately content-free. They establish composition, color, typography, navigation, project-card behavior, detail-page anatomy, and motion posture before copy or media production begins.

## Operating standards

See `docs/OPERATING-STANDARDS.md` for the working contract.

## Current repository layout

```text
portfolio/
├── README.md
├── docs/
│   └── OPERATING-STANDARDS.md
├── designs/
│   ├── index.html
│   └── README.md
├── site/
│   └── README.md
├── motion/
│   └── README.md
├── content/
│   └── README.md
└── .github/
    └── workflows/
        └── pages.yml
```

No public site is enabled by this scaffold yet.
