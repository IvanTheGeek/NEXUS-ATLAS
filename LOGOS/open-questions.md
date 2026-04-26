# ATLAS — Open Questions

> Unresolved design questions and things needing a decision before work can proceed.

## Slice Concern Taxonomy

**Is Automation a concern layer or only an interaction pattern?**
The Automation interaction pattern (Event(s) → Processor → Command(s)) is clearly distinct from Behavior and Translation. But should it also appear as a *concern layer* alongside Business? If Automation is folded into Business, FORGE loses the signal it needs to generate a processor rather than a handler. If it's a separate layer, does it conflict with the Interaction Pattern axis — are two different axes capturing the same distinction?
Decision needed before finalising slice metadata schema.

**Is UX a concern layer, or an attribute/quality of a PATH?**
UX interaction slices (form validation feedback, gesture responses) could be modeled as a concern layer on individual slices. But UX could equally be a property of how Business/Runtime/UI slices are sequenced and designed within a PATH, not a layer on a single slice. If UX is a cross-cut rather than a layer, it belongs in PATH annotations, not slice classification.
Decision needed before updating column classification badge treatment.

**Are Lifecycle and Runtime distinct enough to warrant separation?**
Lifecycle = process-level events (AppStarted, AppSuspended). Runtime = application framework events (RouteResolved, DI wiring). For FORGE they are distinct (Lifecycle drives platform integration code; Runtime drives app framework layer). For ATLAS they may both render in the same "System" swimlane. Worth deciding whether ATLAS needs to distinguish them or can treat them as one concern zone.

**Domain / App / SubDomain hierarchy and relativity**
The same concept can be a Domain for one application and a SubDomain within another application's Domain. ExpenseTracking is a top-level Domain for LaundryLog but a SubDomain inside CheddarBooks' Bookkeeping Domain. How does the model represent this relativity? Are Domain/SubDomain absolute names in a global hierarchy, or relative to the App in scope?
Decision needed before finalizing the 7-axis slice metadata schema.

## Classification System

**Domain / Context / Lens — badge visual treatment**
The column header currently shows Context Group (dark pill) + Bounded Context (outlined pill) + Lens (faint pill). These need to be replaced with the three new dimensions. Questions:
- How many badges does a column header show? All three always, or only what's set?
- Does Domain appear as a pill, a label, or something else?
- When a PATH spans multiple Domains, how is that navigated?

**"Domain" naming collision**
The dimension is called Domain. The DDD-derived Context value that was previously called "Bounded Context: Domain" needs a different name (e.g. "Core", or the actual subject name like "ExpenseTracking"). Need to rename this in all existing gallery columns.

## Column Design

**Single slice expressing multiple flows**
A slice like `MachineTypeSelected` is both Control Flow (form routing) and State Flow (UI memory). The lens filtering question: if a user wants only Information+State, does MachineTypeSelected show? Does it need a flow-type tag, or is this resolved by Context (UX) alone?
Decision needed before implementing lens filtering logic.

**Flow/Workflow grouping visual representation**
How do Flow and Workflow groupings appear in the column viewer?
- Header row above a set of columns? (like a section divider)
- Bracket or visual grouping on the columns themselves?
- Label only, or with a description?
These groupings are expected to emerge from modeling — ATLAS should make them easy to apply after the fact, not require them upfront.

**Interface / screen state beyond thumbnail**
The thumbnail is a placeholder. What is the full Interface representation?
- Is it a link to the Screen State Catalog entry?
- Does it expand inline to show the actual screen design?
- Is there a separate Interface column type, or is screen state always attached to a slice column?

**Column expand-in-place mechanics**
2x expansion is shown in the gallery as a static example. The interaction:
- Click to expand? Button? Both?
- Does it push sibling columns right (reflows the flow), or does it overlay?
- Animation: slide open, or instant?

## PATH Design

**PATH as total traversal — viewer UX**
A PATH crosses all domains and contexts. In the viewer, how does the user navigate a long PATH?
- Horizontal scroll only?
- Jump-to-step navigation?
- Mini-map?

**PATH chaining in the viewer**
PATH B starts where PATH A ends. How is the chain boundary represented? A visual connector between PATH flows? A separate view?

## Patterns

**Pattern recognition**
Translation patterns and external process patterns are structural shapes in the slice graph. Does ATLAS detect and label these automatically, or does the modeler annotate them manually? What does a pattern look like visually in the column flow?

## Event Taxonomy / LaundryLog Domain

**Session model: derived vs. explicit**
If sessions are always derived (3-hour gap rule), `LaundrySessionStarted/Closed` never exist as events. If the driver can explicitly close a session or start a new one at the same location, they become real durable events.
Decision needed before implementing session-aware projections.

**`LaundryLocationUpdated` vs repeated `LaundryLocationCaptured`**
Using the same event for first-set and mid-session location change is simpler but loses signal. Distinct events allow queries like "how many times did this driver change locations in one outing." However, a single event type with a sequence number or `isUpdate` flag could also work.
Decision needed before finalizing the event stream shape.

**Correction semantics: edit vs. history**
`LaundryExpenseCorrected` as an immutable append keeps the stream honest. The question is whether the UI exposes this as "edit" (hides the correction event) or "history" (shows it). The event model can support either — this is a lens/projection choice — but the UI contract needs to be decided.

**`AppStarted` / `RouteResolved` — domain events or PATH scaffolding?**
These are in PATH1 but may be scaffolding for the PATH walkthrough rather than true LaundryLog domain events. If ATLAS needs to show them in a timeline, they stay. If they are PATH sequencing notation only, they should be modeled differently or excluded from the domain event catalog.

**SubDomain name for location identity**
Location identity matching (resolving free-text to a canonical place, e.g. "Love's #123" → a specific GPS-located stop) is richer than just "Location." The SubDomain may need its own name (e.g., "Identity", "LocationRegistry", "PlaceResolution") if the concept grows into a distinct bounded context.
