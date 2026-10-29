# Pragmatic Decision Framework

Use this reference when a task involves a meaningful design choice. Do not turn routine edits into a formal review exercise.

## Seven questions

1. **Problem:** What concrete problem or requirement are we addressing?
2. **Constraints:** Which requirements, project conventions, compatibility limits, and operational constraints matter?
3. **Simplicity:** What is the simplest reliable solution that meets the requirement?
4. **Complexity:** What complexity does each option introduce or remove?
5. **Changeability:** How does the option affect coupling, cohesion, testing, and future modification?
6. **Risk:** What could break, how severe would that be, and how can we detect it?
7. **Evidence:** What observations, diagnostics, or tests support the choice?

Use the questions proportionately. For a small, obvious change, most answers may be self-evident and need not be written out.

## Compare alternatives only when useful

When two or more plausible approaches have materially different consequences, compare them by:

- Correctness and safety.
- Fit with the current project.
- Implementation and maintenance cost.
- Coupling and isolation of change.
- Testing and debugging implications.
- Operational or performance consequences.
- Reversibility if the decision proves wrong.

Do not manufacture multiple options for a straightforward task. Recommend one approach when evidence and constraints make it the clear choice.

## A practical decision rule

Prefer an option when its concrete benefits outweigh the complexity, indirection, and maintenance it adds.

This is a reasoning heuristic, not a numerical score. Do not invent precise weights or claim mathematical certainty for subjective architectural decisions.

## Explain the result

When the choice matters, communicate:

- The recommended approach.
- The main reason it fits.
- The most important trade-off.
- Any assumption or risk that could change the recommendation.

Keep the explanation short for low-impact decisions and more detailed for consequential ones.
