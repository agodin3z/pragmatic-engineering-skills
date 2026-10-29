# Debugging, Impact Analysis, and Validation

Use this reference when investigating bugs, modifying shared components, or deciding how much validation a change needs.

## Bug investigation

1. Reproduce the bug or identify the observable failure condition.
2. Inspect relevant logs, diagnostics, and analyzer output.
3. Trace the affected code path and dependency relationships.
4. Inspect the smallest relevant section of code.
5. Form a root-cause hypothesis and check it against available evidence.
6. Implement the smallest correct fix.
7. Run appropriate tests, analyzer checks, or builds.
8. Review the diff for unrelated changes.

If the root cause remains uncertain, state that uncertainty. Do not present a plausible workaround as a verified fix.

## Impact analysis

Before changing shared or widely consumed components, identify:

- Callers and dependents.
- Related controllers and screens.
- Models, DTOs, mappers, and repository contracts.
- Services, routes, and cross-module utilities.
- Existing implementations of similar behavior.
- Tests and other code that rely on the current behavior.

Use available repository navigation, symbol search, dependency graphs, or code intelligence tools to do this efficiently. Inspect source files directly when tooling does not provide enough context.

## Recommend validation proportionally

Recommend validation based on the change's risk, scope, and available project tooling. Do not impose one universal mandatory test/build policy on every task. Explain when a check is important, and distinguish recommended checks from checks actually executed.

Start with the smallest meaningful check:

- Type or compile issue: analyzer or compiler diagnostics.
- Isolated behavior: targeted unit test.
- Widget behavior: relevant Flutter widget tests.
- Cross-module change: relevant integration tests and broader checks.
- Release-sensitive change: applicable build or CI validation.

Prefer project scripts when they exist. Do not invent script names; inspect `pubspec.yaml`, `package.json`, project documentation, and CI configuration first.

Do not run expensive or destructive commands without understanding their effects. Do not claim tests, analyzers, or builds passed unless they were actually run and their results support that claim.

## Change discipline

- Preserve unrelated behavior.
- Avoid broad formatting changes unless required.
- Do not rename unrelated symbols.
- Do not add dependencies without justification.
- Do not migrate architecture opportunistically.
- Keep the diff focused on the task.

## Completion report

Summarize:

1. What changed.
2. Why the approach fits the existing project.
3. Which checks were actually run and their outcomes.
4. Any assumptions, risks, or remaining work.
