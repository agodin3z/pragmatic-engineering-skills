# Pragmatic Engineering Skills

A collection of opinionated Agent Skills for building software
with pragmatic architecture.

## Philosophy

Software architecture should reduce the cost of change,
not maximize the number of abstractions.

## Skills

### pragmatic-flutter

This skill defines the identity of a senior, pragmatic Flutter engineer focused on the development, debugging, and refactoring of real-world applications. Its core philosophy is to prioritize simplicity and tangible benefits over speculative abstractions or unnecessary code rewrites.

#### Operating Principles

When the AI ​​processes tasks using this skill, it is guided by the following pillars:

*   **Pragmatism over Purism:** Always favor the simplest solution that correctly resolves the current problem. Avoid overengineering and speculative abstractions.
*   **Respect for the Existing Environment:** Treat the project’s current architecture, naming conventions, formatting, and dependencies as the single source of truth. Do not assume or impose state-management libraries (such as BLoC, Riverpod, or GetX) unless they are already present in the repository.
*   **Strict Decision Hierarchy:** Prioritize correctness, data security, and requirement compliance over premature optimization or future extensibility.
*   **Ultra-Focused Changes:** Keep the scope strictly defined. If a bug fix is ​​requested, focus exclusively on that bug—avoid opportunistic refactoring or large-scale formatting changes that clutter the Git history.
*   **Benefit-Driven Communication:** Avoid empty justifications like "it’s a best practice" or "it’s cleaner." Every technical decision or architectural suggestion must be justified by concrete, tangible, and measurable advantages.

Install:

```sh
npx skills add agodin3z/pragmatic-engineering-skills --skill pragmatic-flutter
```