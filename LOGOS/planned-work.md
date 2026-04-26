# ATLAS — Planned Work

> Sequenced intentions. Not yet active — promoted to tasks.md when work begins.

## Phase 1 — HTML Prototypes (current phase)

Goal: get the design right in HTML/CSS before building in F#. Each prototype page is a spec.

### Design System (`atlas-design-system.html`)
- [ ] Finalize Domain / Context / Lens token and badge treatment
- [ ] Document column classification system (all three dimensions with examples)
- [ ] Add Flow/Workflow grouping section to design system
- [ ] Add Interface/screen state section
- [ ] Add Actor swimlane section
- [ ] Add column expand-in-place (2x) interaction spec

### Column Gallery (`atlas-column-gallery.html`)
- [ ] All column types represented (see tasks.md for specific types)
- [ ] Flow/Workflow grouping shown with real LaundryLog example
- [ ] GWT toggle interaction working (show/hide per column)
- [ ] Column expand-in-place working (click to 2x, click again to collapse)
- [x] Actor swimlane column visible (sticky left, spans zone rows per actor type)

### Additional Prototype Pages
- [ ] PATH Index page — list of available PATHs, entry point into the viewer
- [ ] Slice Detail page — full spec view for one slice (fields, all GWT cases, notes) ← in progress
- [ ] PATH viewer page — full PATH1 as the real viewer (not gallery)

## Phase 2 — F# Implementation

Goal: build ATLAS in F# (Fun.Blazor or Blazor) using prototypes as specification.

- [ ] Parse `*.nexus.md` files (TOML frontmatter + markdown body)
- [ ] Build PATH graph from slice files (ATLAS builds reverse index at load)
- [ ] Render PATH flow as column sequence
- [ ] Lens toggle filtering (show/hide columns by lens)
- [ ] Domain/Context/Lens classification on each column
- [ ] GWT toggle per column
- [ ] Column expand-in-place
- [ ] PATH Index
- [ ] Slice Detail

## Phase 3 — PAXUS Integration

- [ ] Surface runtime PATH data alongside design PATHs
- [ ] Gap analysis view (design vs runtime)
- [ ] SLA / time constraint annotations (deferred — needs real PAXUS data first)
