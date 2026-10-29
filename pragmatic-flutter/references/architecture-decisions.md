# Pragmatic Architecture Decisions

Use this reference when choosing module boundaries, introducing abstractions, extracting widgets, or refactoring existing code.

## Good enough code

Prefer code that is:

- Easy to read and reason about.
- Easy to debug.
- Easy to modify.
- Easy to remove.
- Proportionate to current complexity.

Do not optimize for hypothetical requirements. The goal is not minimum lines of code; it is minimum unnecessary complexity while preserving correctness and changeability.

## Before introducing an abstraction

Ask:

1. What concrete problem does this abstraction solve?
2. Which dependency or change does it isolate?
3. Does it reduce meaningful duplication or divergence risk?
4. Does it improve testing in a way that matters?
5. What indirection, cognitive load, and maintenance cost does it add?
6. Could a simpler implementation meet the same need?

Introduce an abstraction only when there is a concrete need or demonstrable benefit, such as isolating a dependency that changes, protecting a meaningful boundary, removing costly duplication, or making important behavior independently testable. Explain the trade-off when it materially affects the design. Do not add interfaces, factories, base classes, generic repositories, or helpers merely because a pattern recommends them.

### Common premature abstractions

Be skeptical of:

- Generic repositories for straightforward CRUD.
- Interfaces with one implementation when no meaningful boundary or substitution need exists.
- Factories for trivial object construction.
- Base controllers created only to share a few methods.
- Generic helpers used by a single call site.
- Extra layers that simply forward calls without owning a responsibility.

These are not forbidden in every case. They need a concrete justification.

## Rule of Three as a heuristic

For reusable UI components and helpers:

1. First use: keep it local by default.
2. Second use: consider whether duplication creates a real maintenance problem.
3. Third use: consider extraction into a shared module.

This is a heuristic, not a law. Extract earlier when the component has a distinct conceptual responsibility, meaningful independent state, substantial complexity, independent testing value, or a real risk of divergent implementations.

Do not extract solely to reduce line count.

## Optimize for deletion

Prefer cohesive modules with minimal coupling. A feature should ideally be removable without requiring changes throughout unrelated modules.

Be cautious about:

- Deep controller-to-controller dependencies.
- Global mutable state without a clear reason.
- Shared abstractions created for hypothetical reuse.
- Utility classes that become dumping grounds.
- Circular dependencies.
- Cross-module knowledge that belongs in an application or domain service.

Before adding a module dependency, ask: “Will this make either module harder to change or delete?”

If yes, reconsider the boundary.

## Widget extraction

Keep small, screen-specific widgets near their use when locality improves understanding.

Extract a widget when it is reused, has a clear independent responsibility, materially simplifies the parent widget, owns meaningful state, benefits from independent testing, or has become difficult to navigate.

Prefer standard Flutter widgets before inventing custom abstractions. Do not use arbitrary line-count thresholds as the sole extraction criterion.

## Respect existing boundaries

Respect the architecture actually present in the repository by default. Recommend changing it only when the task reveals a concrete problem or a clear, relevant benefit. Prefer incremental evolution over broad rewrites. A layered flow might be:

`presentation → controllers/state → application/domain → data`

But this is an example, not a universal mandate. Preserve meaningful boundaries between presentation, business behavior, and infrastructure without introducing layers that only forward calls.

Do not reorganize unrelated code because another folder structure appears more elegant.

## Refactoring discipline

Refactor when there is a concrete benefit, such as:

- Reduced complexity or coupling.
- Improved correctness.
- Easier maintenance or testing.
- Removal of duplication that has become costly.
- A demonstrated performance improvement.
- A clear business or delivery benefit.

Do not turn a small feature or bug fix into an architecture migration unless requested or necessary to make the change correct.
