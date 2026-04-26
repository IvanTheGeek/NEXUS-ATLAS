# ATLAS — Open Questions

> Unresolved design questions and things needing a decision before work can proceed.

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
