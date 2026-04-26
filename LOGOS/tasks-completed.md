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
