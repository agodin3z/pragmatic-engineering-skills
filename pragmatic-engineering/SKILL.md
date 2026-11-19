---
name: pragmatic-engineering
description: "Use this skill to apply pragmatic software engineering judgment when planning, writing, debugging, reviewing, or refactoring software—even if not asked explicitly. Evaluate architectural choices, code complexity, abstractions, maintainability, and change risk across any language or framework. Prioritize correctness, existing project context, and the simplest reliable solution over speculative design or over-engineering."
---

# Pragmatic Engineering

Prefer the simplest reliable solution that correctly solves the actual problem. Every layer, abstraction, dependency, or indirection must earn its place by solving a concrete problem—not a hypothetical future requirement.

## Decision hierarchy

Prioritize decisions in this order:

1. Correctness, security, privacy, and data integrity.
2. Explicit requirements and constraints.
3. Existing project conventions and architecture, provided they are fit for purpose.
4. Idiomatic practices for the language, framework, and ecosystem in use.
5. Clear responsibilities, cohesion, and meaningful module boundaries.
6. Readability, maintainability, and ease of change or deletion.
7. Performance improvements supported by evidence.
8. Generality, extensibility, and architectural elegance.

A lower-priority preference must not override a higher-priority requirement. If an existing convention creates a concrete problem relevant to the task, explain the issue and propose a proportionate improvement; otherwise, preserve the established approach.

## Reference guides

Load the relevant reference file when deeper guidance is needed:

- **Abstractions & complexity trade-offs:** [references/abstraction-guidelines.md](references/abstraction-guidelines.md)
- **Design & evaluation checklist:** [references/decision-framework.md](references/decision-framework.md)
- **Focused changes, refactoring & delivery:** [references/change-management.md](references/change-management.md)

## Operating workflow

For any non-trivial task:

1. **Understand** the requested behavior, constraints, and acceptance criteria. Distinguish requirements from preferences and assumptions.
2. **Inspect** relevant project instructions, source code, dependencies, tests, and existing patterns. Use search, symbol navigation, and diagnostics rather than scanning unrelated files.
3. **Trace impact** across callers, dependents, data flows, and affected boundaries before modifying shared code.
4. **Evaluate options** only when there is a meaningful design choice. Choose the smallest viable change that satisfies the requirement without speculative abstractions.
5. **Explain trade-offs** in concrete terms when the choice affects coupling, risk, performance, or change cost. Never call a change “cleaner,” “more scalable,” or “best practice” without explaining the practical benefit.
6. **Implement** a focused change that preserves unrelated behavior. Avoid opportunistic refactors, broad reformatting, or unrequested dependencies.
7. **Validate** proportionately to risk and available tooling. Treat tests, linters, and builds as deliberate tools—never claim a check passed unless it was actually executed.
8. **Report** what changed, why it fits the codebase, what was verified with evidence, and any remaining uncertainty or risk.

## Boundaries and skill coexistence

This skill is language- and framework-agnostic. It governs cross-cutting engineering judgment, not technology-specific implementation syntax.

When a specialized technology or domain skill is also active:

- **Scope:** Use this skill for cross-cutting principles (proportional complexity, change discipline, risk assessment, trade-off communication). Defer to the specialized skill for language idioms, framework conventions, directory structure, and ecosystem-specific validation.
- **Conflict resolution:** Follow the **Decision hierarchy** above, placing specialized technical guidance immediately after project conventions (step 3). If a material conflict cannot be resolved cleanly, state the conflict and explain the trade-off rather than silently mixing approaches.

## Completion criteria

Before declaring a non-trivial task complete, verify that:

- The requested behavior is addressed without unrelated side effects.
- The implementation aligns with the target project's conventions.
- Every introduced abstraction or dependency has a concrete justification.
- Validation claims accurately distinguish executed checks from recommended ones.
- Material assumptions, limitations, and unresolved risks are stated plainly.
