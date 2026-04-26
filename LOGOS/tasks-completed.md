# ATLAS — Active Tasks

> What is done, in progress, or immediately next. Updated each session.

## Completed

- [x] `atlas-design-system.html` — initial creation with token reference, entity types, concern contexts, typography, badges, entity boxes, thumbnails, lens toggles, shell header, geometry reference
- [x] `atlas-design-system.html` — left nav (sticky 248px sidebar, section headers, anchor links, IntersectionObserver active tracking)
- [x] `atlas-design-system.html` — text size control S/M/L/XL (13/16/19/22px), dark/light theme toggle, localStorage persistence
- [x] `atlas-column-gallery.html` — 6-column PATH1 flow (LaunchApp, ResolveStartupRoute, SetLocation, MachineTypeSelected, LogExpense, RecentExpenses)
- [x] `atlas-column-gallery.html` — LogExpense expanded 2× with GWT open
- [x] Badge padding fix — asymmetric vertical padding (4px top / 2px bottom) for uppercase glyph optical centering — applied to both files
- [x] `atlas-column-gallery.html` — text size control S/M/L/XL matching design system
- [x] `atlas-column-gallery.html` — COMMAND badge overflow at XL fixed (flex-wrap + margin-left: auto on kind badge)
- [x] `logos/` renamed to `LOGOS/` via `git mv` (history preserved)
- [x] Stop hook configured with two-step sequence: (1) LOGOS maintenance via `claude --print` on transcript stdin, (2) git checkpoint commit+push — docs always committed in sync with code
- [x] `atlas-column-gallery.html` — CSS Grid zone layout bug fixed: adjacent named line groups `[header-end] [screen-start]` are invalid `<track-list>` syntax; browser silently drops the entire `grid-template-rows` declaration; fix is to merge into `[header-end screen-start]`
- [x] `atlas-slice-detail.html` — S/M/L/XL size controls in header (M default active), `atlas-slice-size` localStorage key independent of gallery preference; slice renders correctly at medium size
- [x] `atlas-column-gallery.html` — actor column: sticky left column with `actor-bg` covering all rows including header; DRIVER spans screen+command zones (blue tint + label), SYSTEM spans event+GWT zones; right border separates actor column from slice card; sticky horizontal scroll behavior wired (holds position at left edge as slices scroll past)
