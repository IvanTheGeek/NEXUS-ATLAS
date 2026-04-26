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
- [x] `atlas-column-gallery.html` — INTERFACE bar added between DRIVER thumbnail row and SYSTEM row in actor column (dark slate background, "INTERFACE" label at correct weight); actor column zone labels (DRIVER / INTERFACE / SYSTEM) all align cleanly to their respective grid rows with no overlap on slice card borders
- [x] `atlas-column-gallery.html` — SYSTEM zone height fix: gear icon gives the SYSTEM zone proper height so the label is clearly below the INTERFACE bar; SYSTEM lane in actor column covers only the gear row, not COMMAND/EVENT entities below it
- [x] `atlas-column-gallery.html` — RESTAPI actor swimlane added (dark terminal block with `POST /api/log-expense`); all four actor swimlanes (DRIVER thumbnail, RESTAPI dark terminal, INTERFACE grey divider, SYSTEM gear) rendering cleanly with actor lane labels aligned to their respective rows
- [x] `atlas-column-gallery.html` — DRIVER and RESTAPI swimlane heights equalized to 126px each via shared `--swim-lane-h` CSS token; terminal block anchored to top of RESTAPI zone; both rows adjust together by changing the single token
- [x] `atlas-column-gallery.html` — actor swimlane color differentiation: DRIVER → blue tint, RestAPI → purple (label rendered as mixed-case `RestAPI`), CLI → dark slate; each lane now has a visually distinct colour and border
- [x] `atlas-column-gallery.html` — zone tinting inside slice cards: each zone within a card carries its swimlane tint (blue=DRIVER, purple=RestAPI, slate=CLI, light grey=SYSTEM), matching actor column labels exactly, driven by shared `--swim-*-bg` CSS variables
- [x] `atlas-column-gallery.html` — card border z-index fix: slice card border now renders above zone background tints (visible cleanly at INTERFACE and SYSTEM rows); zone backgrounds no longer bleed over card outlines
- [x] `atlas-column-gallery.html` — RestAPI swimlane color changed from purple to teal; clearly distinct from blue DRIVER row; all four swimlane colours (blue, teal, slate, light grey) are visually unambiguous
- [x] `atlas-column-gallery.html` — ADMIN swimlane added (amber zone, wide desktop thumbnail with dark title bar, dark nav with active tab highlighted in amber, four KPI cards with coloured value bars, a bar chart, and a status sidebar with green/yellow/red dots); all five swimlanes above INTERFACE are now distinct and equal height
- [x] `atlas-column-gallery.html` — GWT zone condensed inline view: G/W/T labels as small coloured badges, Given event (`AppOpened`) as blue-tinted pill, When fields as monospace `key : value` chips (`machineType : Dryer`, `quantity : 1`, `unitPrice : 2.50`, `payment : Coins`), Then event (`LaundryExpenseLogged`) as green-tinted pill
