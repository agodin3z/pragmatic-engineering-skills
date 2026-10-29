# Change Management and Validation

Use this reference when modifying existing software, refactoring, debugging, or recommending checks.

## Keep changes focused

- Preserve unrelated behavior.
- Avoid opportunistic architecture migrations.
- Do not reformat entire files or rename unrelated symbols without a reason.
- Avoid adding dependencies unless they provide a justified benefit.
- Keep a bug fix focused on the bug unless a wider change is necessary or explicitly requested.
- Prefer small, reviewable changes when they can safely achieve the goal.

## Understand impact before editing

For non-trivial changes, identify relevant:

- Callers and dependents.
- Data flows and integration boundaries.
- Shared models, contracts, and utilities.
- Tests and automation.
- Configuration, migration, and deployment implications.

Use available search, symbol navigation, dependency analysis, and project tooling. Inspect source directly where tools leave gaps.

## Recommend validation based on risk

Do not impose a universal test or build checklist on every task. Recommend checks based on:

- Severity if the change is wrong.
- Scope and number of affected components.
- Data integrity, security, and compatibility implications.
- Whether the behavior is easy to observe manually.
- Existing test coverage and available tooling.

Possible checks include focused tests, integration tests, static analysis, type checking, builds, security checks, migration validation, and manual verification.

Start with the narrowest useful check and broaden validation when the scope or risk warrants it. Explain why an important check is recommended.

## Be accurate about verification

- Report only checks actually executed as completed.
- Distinguish “recommended,” “not run,” “blocked,” and “passed.”
- Do not claim a bug is fixed solely because code was changed.
- If a check could not be run, explain the limitation without implying success.
- When root cause is uncertain, label the hypothesis and state what evidence is missing.

## Completion summary

For non-trivial work, summarize:

1. What changed.
2. Why the approach fits the requirement and project.
3. Which checks were actually run and their results.
4. Important assumptions, risks, or follow-up work.
