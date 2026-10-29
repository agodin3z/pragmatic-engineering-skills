# Abstraction Guidelines

Use this reference before adding layers, interfaces, factories, generic components, shared utilities, or other abstractions.

## Start with a concrete need

An abstraction may be justified when it:

- Isolates a dependency that changes independently.
- Protects a meaningful domain or module boundary.
- Coordinates a non-trivial workflow.
- Removes duplication that creates real maintenance or divergence risk.
- Makes important behavior independently testable.
- Encapsulates complexity that would otherwise leak to callers.
- Provides a stable contract for multiple real consumers.

The existence of a pattern, tutorial, or theoretical future use is not sufficient justification by itself.

## Check the cost

An abstraction also adds potential costs:

- More indirection when tracing behavior.
- More concepts a developer must understand.
- More files and contracts to maintain.
- More opportunities for generic designs to become awkward.
- Additional change coordination when the abstraction itself evolves.

Consider both the complexity removed and the complexity introduced.

## Common warning signs

Question abstractions that:

- Only forward a call without adding responsibility or protecting a boundary.
- Have one implementation and no concrete substitution or isolation need.
- Generalize a one-off operation without credible reuse.
- Exist only to satisfy a pattern or diagram.
- Hide simple control flow behind factories, registries, or indirection.
- Turn a shared utility into an unowned dumping ground.
- Require unrelated modules to understand each other's internals.

These are warning signs, not absolute prohibitions. A single implementation can still justify an interface when it protects an important boundary or enables a necessary substitution.

## Reuse and duplication

Do not abstract solely because code appears twice. Compare the meaning and expected evolution of the repeated behavior.

- Similar-looking code may represent different business rules and should remain separate.
- Repeated behavior that must change together may benefit from one implementation.
- A third use can be a useful time to reconsider extraction, but no repetition count is a universal law.
- Extract earlier when the component has a clear independent responsibility or its complexity obscures the caller.

## Layers and use cases

Add a layer when it owns a meaningful responsibility, such as coordinating a workflow, enforcing business rules, or isolating infrastructure.

Do not create application services, use cases, repositories, domain entities, adapters, or interfaces automatically for every feature. A simple operation may be clearer without them.

## Decision checklist

Before introducing an abstraction, answer:

1. What specific problem does it solve now?
2. What responsibility does it own?
3. What dependency or change does it isolate?
4. What concrete benefit will callers or maintainers receive?
5. What additional concepts and maintenance costs does it create?
6. Is there a simpler solution with comparable benefits?

If the benefit is speculative and the current implementation is clear, start simpler and evolve when evidence appears.
