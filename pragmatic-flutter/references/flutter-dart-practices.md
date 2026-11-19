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

## Images and uploads

When the application requires local image compression, follow the existing upload flow and established compression library. Prefer processing close to the upload boundary rather than spreading image manipulation across widgets and unrelated layers. Avoid compressing the same image repeatedly without a demonstrated need.

## Widget lifecycle and BuildContext safety

- **Dispose resources:** Always dispose `TextEditingController`, `ScrollController`, `AnimationController`, `FocusNode`, and active `StreamSubscription` instances in `dispose()` (or through the project's established lifecycle hooks).
- **Async gaps and `BuildContext`:** Never use `BuildContext` across an `await` boundary without checking `context.mounted` (or `mounted` inside a `State` class) first.
- **Avoid side effects in `build`:** Never trigger network calls, navigation, dialogs, or state mutations directly inside a `build()` method.
- **Keys and lists:** Provide meaningful keys (`ValueKey`, `ObjectKey`) when list items are reordered, inserted, removed, or hold stateful widgets.

## Performance

Common Flutter performance-sensitive areas include large lists, expensive builds, complex animations, large images, and excessive reactive rebuilds.

Measure or reproduce a performance problem when possible. Avoid speculative caching, elaborate memoization, custom render objects, or other complexity without evidence that it addresses a real issue.
