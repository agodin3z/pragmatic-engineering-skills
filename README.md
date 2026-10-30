![GitHub License](https://img.shields.io/github/license/agodin3z/pragmatic-engineering-skills) [![skills.sh](https://skills.sh/b/agodin3z/pragmatic-engineering-skills)](https://skills.sh/agodin3z/pragmatic-engineering-skills)


# Pragmatic Engineering Skills

A collection of opinionated Agent Skills built around pragmatic software engineering judgment.

## Philosophy

> Optimize for correctness, changeability, and the total cost of maintaining software, not architectural elegance in isolation.

The goal is to solve the actual problem with the simplest reliable approach, respect the context of each project, and introduce complexity only when its benefits justify the cost.

## Skills

### `pragmatic-engineering`

A language- and framework-agnostic skill for architectural decisions, implementation planning, refactoring, debugging, and risk-aware validation.

Install:

```bash
npx skills add agodin3z/pragmatic-engineering-skills --skill pragmatic-engineering
```

This skill is intentionally independent of any programming language, framework, cloud provider, or architectural style.

### `pragmatic-flutter`

This skill defines the identity of a senior, pragmatic Flutter engineer focused on the development, debugging, and refactoring of real-world applications. Its core philosophy is to prioritize simplicity and tangible benefits over speculative abstractions or unnecessary code rewrites.

#### Operating Principles

When the AI ​​processes tasks using this skill, it is guided by the following pillars:

*   **Pragmatism over Purism:** Always favor the simplest solution that correctly resolves the current problem. Avoid overengineering and speculative abstractions.
*   **Respect for the Existing Environment:** Treat the project’s current architecture, naming conventions, formatting, and dependencies as the single source of truth. Do not assume or impose state-management libraries (such as BLoC, Riverpod, or GetX) unless they are already present in the repository.
*   **Strict Decision Hierarchy:** Prioritize correctness, data security, and requirement compliance over premature optimization or future extensibility.
*   **Ultra-Focused Changes:** Keep the scope strictly defined. If a bug fix is ​​requested, focus exclusively on that bug—avoid opportunistic refactoring or large-scale formatting changes that clutter the Git history.
*   **Benefit-Driven Communication:** Avoid empty justifications like "it’s a best practice" or "it’s cleaner." Every technical decision or architectural suggestion must be justified by concrete, tangible, and measurable advantages.

Install:

```bash
npx skills add agodin3z/pragmatic-engineering-skills --skill pragmatic-flutter
```
