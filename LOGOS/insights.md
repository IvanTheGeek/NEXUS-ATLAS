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

## Promotion Candidates → NEXUS-LOGOS

The following insights are candidates for promotion to NEXUS-LOGOS/docs/ when mature:
- Three classification dimensions (Domain/Context/Lens) → methods/modeling.md or new file
- PATH as total traversal definition → methods/paths.md
- Time/Control implicit in PATH structure → methods/paths.md
- NEXUS model scope vs Event Modeling → principles/ or methods/influence.md
