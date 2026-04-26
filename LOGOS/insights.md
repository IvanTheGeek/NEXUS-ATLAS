# ATLAS — Cross-Cutting Insights

> Insights with implications beyond ATLAS — for NEXUS as a whole, for other projects,
> or for the methodology. Items here should be promoted to NEXUS-LOGOS when mature.

## NEXUS Model Scope (vs. Event Modeling)

Adam Dymitruk's Event Modeling focuses on business behavior — the information flow through
a system as the business cares about it. NEXUS intentionally extends this scope:

- The NEXUS model can express the complete program — Control, Information, State, Effect,
  Authority — not just business behavior
- "Business behavior" (Adam's view) is one Lens on the complete NEXUS model, not the whole model
- The extended scope enables compilation: the model becomes the source; code is the output
- Adam says "the model is not the implementation" — NEXUS's hypothesis is that a sufficiently
  complete model makes implementation mechanical (FORGE as compiler)

## Three Classification Dimensions

Every slice in the model belongs to three orthogonal dimensions:

- **Domain** — the subject matter area; hierarchical (Domain > Subdomain); the *what*
- **Context** — the ownership/responsibility boundary; the *who*
- **Lens** — the perspective filter; the *how you want to look at it*

These are independent: varying one does not constrain the others.

Note: avoid using "Domain" as a Context value name — it collides with the dimension name.
Use the actual subject name (e.g. "ExpenseTracking", "Core") for the Context value.

## PATH as Total Traversal

A PATH is a complete, concrete, example-data-bound traversal through the entire system —
all domains, all contexts, using specific example data. It is not scoped to one domain.

This distinguishes PATH from Flow/Workflow:
- Flow/Workflow = organizational grouping of slices toward a sub-goal (can be domain-scoped)
- PATH = the complete causal sequence (crosses all boundaries)

A PATH *passes through* Flows; it does not consist of them.

## Time and Control are Implicit in PATH Structure

- **Time** is encoded in PATH sequence — the ordering is causal time, not just clock time.
  PATH says "A must precede B because B depends on what A produced." This is stronger than
  temporal ordering.
- **Control flow** is the PATH sequence itself. The PATH IS the control flow.
  `ResolveStartupRoute` is a Control Flow slice, but its place in the PATH encodes the
  control dependency — no separate control flow dimension is needed.

Multiple PATHs express multiple causal sequences that run independently, intersect, or chain.
This is richer than Adam's single-timeline blueprint and handles complex systems better.

## Flows are Emergent from Model Primitives

The 9 program flows (Control, Information, State, Effect, Error, Time, Resource, Authority,
Event) map onto the model primitives rather than being a separate classification:

- Information → Events, Commands, Views carry it
- State → Views accumulate it
- Control → PATH sequence and Actor type express it
- Effect → Context boundary crossing; ExternalSystem actor
- Authority → Actor role; swimlane
- Error → impossible states by design (make invalid states unrepresentable)
- Time → Actor is a Clock (automation/scheduled trigger)
- Event → the modeling mechanism itself, not a flow category
- Resource → sub-concern of Effect

Lenses filter by perspective; they do not filter by "flow type" as a separate tag.

## UX Interactions as First-Class Slices

UX interaction slices (e.g. `MachineTypeSelected`) have the same Command→Event structure
as business slices. They are not second-class or "just UI." They express real domain
facts — state changes that the system needs to know about.

UX being a business concern: a website's signup UX affects customer acquisition, which IS
a business concern — just in a different Domain/Context than the core product domain.
The model accommodates this without forcing a choice.

## Flow/Workflow Groupings Should Emerge

Flow and Workflow groupings should not be imposed top-down. They become obvious after enough
slices are modeled and natural clusters appear. ATLAS should make it easy to apply grouping
labels after the fact. Pre-designing groupings risks creating artificial boundaries.

## Error Handling as Model Completeness

If an exception is thrown in code, either:
1. The model is incomplete (a case was not designed)
2. The code is wrong (an invalid state was made possible that the model excludes)

Per Scott Wlaschin / Domain Modeling Made Functional: make invalid states unrepresentable.
Error flow is not a separate modeling concern — it is a signal of modeling gaps.

## Shared CSS Grid for Multi-Column Alignment

When slice columns are placed in a single shared CSS Grid (rather than each column having
its own independent grid), row heights are determined by the tallest cell across all columns
in that row. This means COMMAND rows, EVENT rows, and GWT rows stay perfectly aligned
regardless of how many fields each individual slice has. The layout does the alignment work
automatically — no per-column height coordination is needed.

This is the correct structural approach for the ATLAS column viewer: one grid, all columns
as grid children, zone rows defined once at the grid level.

## CSS Grid Named Line Syntax: One Group Per Boundary

CSS Grid's `<track-list>` grammar allows exactly one `<line-names>?` token at each track
boundary. Writing two separate bracket groups at the same position — even on adjacent lines —
is invalid and causes the browser to silently discard the entire `grid-template-rows`
declaration with no error in the console:

```css
/* INVALID — two <line-names> groups at the same boundary */
grid-template-rows:
  [header-start] auto
  [header-end]
  [screen-start] auto
  [screen-end];

/* VALID — merge adjacent end/start names into one group */
grid-template-rows:
  [header-start] auto
  [header-end screen-start] auto
  [screen-end];
```

The silent failure mode makes this particularly hard to diagnose. If a grid layout
appears to apply no row structure at all, check for adjacent named-line groups first.

## Screenshot Fidelity vs. Bounding Rect Measurement

JPEG compression and scaling in screenshot tools can make correctly-centered elements
appear misaligned. When a visual inspection raises an alignment concern, verify by reading
`getBoundingClientRect()` center values rather than trusting the screenshot pixel pattern.
If `label.center_y === item.center_y` the alignment is correct regardless of how the
screenshot renders it. Trust measurements over visuals when they disagree.

## Flex Items Default to `min-width: auto`

Flex items have `min-width: auto` by default, which means they will not shrink below their
min-content width even when the container is smaller. A label inside a narrow flex column
will hold the column open rather than truncate or wrap as expected.

Fix: set `min-width: 0` on the flex item to allow it to shrink freely. This is a silent
failure mode — the column appears not to resize without any console error.

```css
/* WRONG — flex item holds open to its text's min-content width */
.sub-lane { display: flex; align-items: center; justify-content: center; }

/* CORRECT — allow shrinking below min-content */
.sub-lane { display: flex; align-items: center; justify-content: center; min-width: 0; }
```

## VIEW Slice: Read-Side Design Conventions

The VIEW slice type has a distinct visual treatment that mirrors COMMAND but signals read-side semantics:

- **Banner colour**: green (vs. blue for COMMAND) — visually distinct at a glance
- **Concern meta**: "Business.Translation" (vs. "Business.Behavior" for commands)
- **GWT pattern**: Event → Criteria → View (trigger event, filter criteria, projected view result)
  — the read-side analog of COMMAND's Given → When → Then
- **GWT colour**: Criteria card uses slate grey header + light grey-tinted background; W pill is grey with near-black text — neutral tone avoids semantic colour association; rose was rejected for error connotation, cyan was also tried and rejected
- **DRIVER thumbnails**: list-style layout showing the projected data screen
- **Actor rows**: `GET /api/…` for RestAPI, `-q …` for CLI — query conventions vs. `POST` / verb commands

The banner approach (used for both COMMAND and VIEW) moves classification out of the entity header
and into the column-level zone label. The colour convention (blue=write, green=read) is now
established across both slice types in `atlas-slice-design-concept.html`.

## Command Header: Banner vs. Badge Treatment

The COMMAND zone header can be rendered two ways:
- **Badge-heavy**: entity name + kind badge + classification badges stacked in the header row
- **Clean banner**: solid colour fill (`--cmd-header` blue) with only the zone label ("COMMAND") right-aligned, rounded top corners flush with the card

The banner approach moves classification context out of the per-entity header and into the column-level (or swimlane-level) context. This keeps the entity card focused on the entity itself. The side-by-side comparison in `atlas-slice-design-concept.html` (Slice 01 = banner, Slice 02 = badges) is the reference for this decision.

Decision needed: which treatment becomes canonical for COMMAND (and by extension EVENT) zone headers.

## Adam's Three Swimlane Patterns

Event Modeling distinguishes three distinct swimlane interaction patterns:

1. **Command (human-driven)** — a person issues a command; the system records an event. The human is the trigger.
2. **View (projection-driven)** — the system projects events into a read model; a person or system queries it. No command is issued by the query.
3. **Automation (system-driven)** — a read model threshold or clock triggers a command with no human actor. The system is the trigger.

These are structurally distinct: Automation is a read-model → command chain driven by the system, not by a human gesture. It is the third swimlane in Adam's visual, explicitly separate from the human-driven Command lane.

In ATLAS terms, the Automation pattern's actor is a Clock or Processor (not a person). The swimlane is the carrier of this distinction — which is why the actor column is load-bearing, not decorative.

## Domain Events vs. UI/Form State

Not every state change that affects the UI is a domain event. The test:

- **Domain event** — something the system needs to remember across sessions; a durable fact that read models project from.
- **Form/UI state** — ephemeral selection or input that only matters for the duration of a form interaction. It is a field on the command that eventually fires, not an event in its own right.

Examples for LaundryLog:
- `MachineTypeSelected` → NOT an event; it is the `machineType` field on `LaundryExpenseLogged`
- `PriceEntered`, `QuantityChanged` → NOT events; form step state
- `ViewedExpenseHistory` → NOT an event; read model queries do not produce events
- `LaundryExpenseLogged` → IS an event; the system needs this fact to build every projection

The boundary matters for FORGE: only domain events enter the event stream and get persisted.

## Narrow Blueprint Pattern

Some systems have a single dominant event that feeds the majority of read models. LaundryLog is an example: almost every projection (recent expenses, session total, monthly summary, location breakdown) derives from `LaundryExpenseLogged` alone.

The supporting events (location management, session lifecycle, settings) are infrastructure around the single core loop. In Adam's visual, most columns on the board are VIEW slices projecting off that one core event in different shapes for different actors and contexts.

This is the **narrow blueprint pattern**: one main command slice, many read-model projections, sparse supporting infrastructure. Recognising this shape early keeps the model honest — it resists over-engineering supporting events before they are needed.

## Promotion Candidates → NEXUS-LOGOS

The following insights are candidates for promotion to NEXUS-LOGOS/docs/ when mature:
- Three classification dimensions (Domain/Context/Lens) → methods/modeling.md or new file
- PATH as total traversal definition → methods/paths.md
- Time/Control implicit in PATH structure → methods/paths.md
- NEXUS model scope vs Event Modeling → principles/ or methods/influence.md
