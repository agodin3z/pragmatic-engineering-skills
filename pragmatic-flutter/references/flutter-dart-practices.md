# Flutter and Dart Practices

Use this reference when writing or changing Dart/Flutter code. Existing project conventions take precedence when they are intentional and safe.

## Naming and formatting

Follow idiomatic Dart naming:

- Files: `snake_case.dart`
- Classes, enums, extensions: `PascalCase`
- Variables, functions, and methods: `camelCase`
- Constants: idiomatic Dart `lowerCamelCase`, unless the project has a deliberate established convention.

Follow the repository's formatter, analyzer configuration, import sorter, and lint rules.

A common import grouping is:

1. Dart libraries.
2. Flutter and external packages.
3. Project imports.

Use the configured project tooling when it exists rather than manually imposing a different style.

## Types and null safety

- Let inference work when the type is obvious.
- Declare public return types and explicit types when they clarify an API contract or complex expression.
- Avoid `dynamic` to bypass analyzer errors.
- Prefer normal null checks and flow analysis over `!`.
- Use `!` only when a real invariant guarantees non-nullness.
- Do not add null checks solely to silence the analyzer without understanding the source of nullability.

## State management and controllers

Remain agnostic to state-management libraries. Use the library already adopted by the application, whether it is BLoC/Cubit, Riverpod, GetX, Zenify, or another suitable option, unless a change is explicitly requested or a migration is justified.

For controller-based architectures, keep controllers focused on state, state transitions, and orchestration. Keep widget rendering, layout decisions, and large widget trees in the presentation layer.

Keep reactive rebuild scopes as small as practical. Prefer local widget state for state that belongs exclusively to a widget and does not need application-level coordination.

Do not introduce a controller/provider solely to satisfy a blanket rule that every screen must have one.

## Models and code generation

Follow the repository's existing model, serialization, immutability, and code-generation conventions.

- Do not manually maintain generated files.
- Do not edit generated output as the normal way to change behavior.
- Discover the project's generation commands before running tools directly.
- If a generated file appears wrong, inspect its source annotations, generator configuration, and command output.

Libraries such as Freezed may be appropriate in projects that already use them; do not assume they are universal requirements.

## Data and mapping

Keep presentation code independent from transport DTOs when a meaningful domain model or mapper already exists.

Do not create a mapper or domain model automatically for every type. Decide based on whether it protects a real boundary, represents distinct concepts, or reduces coupling.

## Asynchronous work and errors

Handle failures at the layer that can make a meaningful decision about them.

- Report unexpected failures through the project's established logging or crash-reporting mechanism.
- Preserve stack traces when the project's error-reporting API supports them.
- Do not silently swallow exceptions.
- Do not catch every exception just to return a success-shaped result.
- Handle known harmless failures only when ignoring them is intentional, safe, and documented where needed.
- Avoid error handling that masks programming defects.

## Environment and secrets

Use the repository's established environment/configuration mechanism. Never hardcode or commit credentials, API keys, tokens, passwords, or local secret values.

Do not assume a particular environment library. Inspect how the project generates, loads, and validates configuration.

## Images and uploads

When the application requires local image compression, follow the existing upload flow and established compression library. Prefer processing close to the upload boundary rather than spreading image manipulation across widgets and unrelated layers. Avoid compressing the same image repeatedly without a demonstrated need.

## Performance

Common Flutter performance-sensitive areas include large lists, expensive builds, complex animations, large images, and excessive reactive rebuilds.

Measure or reproduce a performance problem when possible. Avoid speculative caching, elaborate memoization, custom render objects, or other complexity without evidence that it addresses a real issue.
