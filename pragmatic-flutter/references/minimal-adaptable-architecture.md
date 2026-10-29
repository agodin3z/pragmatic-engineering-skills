# Minimal, Adaptable Flutter Architecture (MVVM)

Use this reference when starting a new Flutter application or feature and the repository does not already establish an architecture.

## Goal

Use Flutter's recommended separation of concerns as the default: **Views and ViewModels in the UI layer, with repositories and services in the data layer**. Keep the implementation as small as the feature allows, and add a domain layer only when business complexity justifies it.

MVVM is a responsibility model, not a mandate to create a large number of files or adopt a particular state-management package. Follow the target project's established conventions when they are sound.

Reference: [Flutter app architecture recommendations](https://docs.flutter.dev/app-architecture/recommendations).

## Start with the existing repository

Before proposing a structure:

1. Inspect the current folders, dependencies, routing, state-management approach, tests, and conventions.
2. Identify whether the project already has useful boundaries and whether it follows a different, intentional architecture.
3. Extend the existing approach when it is sound; do not migrate an established project to MVVM merely to match this reference.
4. Avoid reorganizing unrelated code just to match the example below.

## Recommended default structure

For a new small or medium application, a feature-oriented structure with MVVM in the UI layer is a practical starting point:

```text
project/
├── lib/
│   ├── ui/
│   │   ├── core/
│   │   │   ├── ui/
│   │   │   │   └── shared_widget.dart
│   │   │   └── themes/
│   │   └── example_feature/
│   │       ├── view_models/
│   │       └── widgets/
│   ├── domain/
│   │   └── models/
│   ├── data/
│   │   ├── repositories/
│   │   ├── services/
│   │   └── model/
│   ├── config/
│   ├── utils/
│   ├── routing/
│   ├── main.dart
│   ├── main_development.dart
│   └── main_staging.dart
├── test/
│   ├── data/
│   ├── domain/
│   ├── ui/
│   └── utils/
└── testing/
    ├── fakes/
    └── models/
```

This structure is a starting point, not a mandatory directory checklist. Existing projects may use different names or organization. Preserve established conventions unless a concrete problem justifies changing them.

## Architectural Layers

### 1. View

**Location:** `lib/ui/<feature>/widgets/`

The View is responsible for presenting UI and forwarding user interactions to its ViewModel.

Responsibilities:
- Render the current presentation state.
- Forward user actions to the ViewModel.
- Display loading, success, empty, and error states as needed.
- Compose feature-specific widgets and reusable UI components.

Rules:
- Keep business and presentation logic out of widget build methods.
- Do not access data sources directly from Views.
- Avoid duplicating state already owned by the ViewModel.
- Extract widgets when doing so improves readability, reuse, or independent testing, not merely to reduce line count.

A screen may be implemented in a single file or split across multiple widgets when complexity warrants it.

### 2. ViewModel

**Location:** `lib/ui/<feature>/view_models/`

The ViewModel manages presentation state and coordinates the actions required by the View.

Responsibilities:
- Expose state needed by the UI.
- Handle user-triggered actions.
- Coordinate repository operations.
- Transform domain or repository data into presentation-ready state when necessary.
- Manage loading, error, and other UI-related states.

Rules:
- Keep widget-specific concerns out of the ViewModel.
- Avoid direct access to HTTP clients, databases, or other low-level data sources.
- Do not duplicate business rules that belong in the domain.
- Prefer explicit state and clear method names over generic command or event abstractions.
- Use the project's established state-management solution.

The ViewModel is a role, not a requirement to use a specific package. GetX controllers, BLoC/Cubit, Riverpod Notifiers, and other suitable constructs can fulfill this role.

Do not introduce a second state-management abstraction on top of the one already used by the project without a concrete reason.

### 3. Repository

**Location:** `lib/data/repositories/`

Repositories provide a consistent interface for accessing and managing application data.

Responsibilities:
- Coordinate access to one or more data sources when needed.
- Expose operations meaningful to the application.
- Handle data retrieval, persistence, and synchronization concerns.
- Map data-source results into domain models where appropriate.
- Abstract data-source details from ViewModels and other consumers.

Rules:
- Introduce repositories when they provide a useful boundary around data access.
- Keep database and network implementation details out of the UI layer.
- Avoid creating interfaces and implementation classes for every repository by default.
- Do not make repositories responsible for unrelated business workflows or UI state.

Use abstractions when they provide a real benefit, such as multiple data sources, meaningful isolation, or easier testing.

### 4. Service

**Location:** `lib/data/services/`

Services encapsulate communication with external systems or technical data sources.

Examples include:
- REST or GraphQL APIs.
- Local databases.
- File storage.
- Platform-specific integrations.
- Third-party SDKs.

Rules:
- Keep services focused on a technical responsibility.
- Let repositories coordinate data sources when that coordination belongs to the data-access boundary.
- Do not create a service for every function or wrap a package without adding meaningful value.
- Keep transport and persistence models separate from domain models when their responsibilities or lifecycles differ.

A simple feature may not need a separate service and repository if the project's conventions and complexity justify a smaller design.

### 5. Domain Models

**Location:** `lib/domain/models/`

Domain models represent concepts used by the application, independent of how data is retrieved or displayed.

Rules:
- Use domain models when they clarify business concepts or provide a stable boundary.
- Keep them independent of widget rendering and data-source implementation details.
- Avoid creating duplicate model types when one model adequately serves the current requirements.
- Separate API, persistence, domain, and presentation models when their responsibilities genuinely differ.

A dedicated domain layer is not mandatory for every feature. Simple applications may not need additional domain abstractions.

### 6. Optional Domain Use Cases

**Location:** Add a suitable location under `lib/domain/` only when justified by the project's conventions.

Use cases are appropriate when a business operation:
- Represents a meaningful application capability.
- Contains non-trivial business rules or orchestration.
- Is reused across multiple ViewModels or entry points.
- Benefits from independent testing or an explicit boundary.

Do not create a use-case class for every repository method or simple CRUD operation by default.

A ViewModel can call a repository directly when the operation is straightforward and introducing a use case would add indirection without meaningful benefit.

## Data Flow

Prefer a clear, unidirectional flow:

```text
User interaction
      |
      v
     View
      |
      v
   ViewModel
      |
      v
  Repository
      |
      v
    Service
      |
      v
 External system / local storage

Results return through the same layers,
updating ViewModel state and then the View.
```

The service is optional. A repository may access a local or remote source through the project's existing implementation.

Keep dependencies directed toward the appropriate abstraction boundaries. Views should not bypass the ViewModel to access repositories or services directly.

## Feature Organization

Organize feature-specific presentation code together:

```text
lib/ui/example_feature/
├── view_models/
│   └── example_view_model.dart
└── widgets/
    ├── example_screen.dart
    └── example_card.dart
```

Keep shared UI components in `lib/ui/core/ui/` when they are genuinely reusable across features.

Avoid moving a widget into a shared directory simply because it might be reused someday. Move it when reuse is real or when a clear shared responsibility emerges.

Keep data and domain code in their established top-level locations unless the project already follows a different, coherent feature-first convention.

## State and Dependency Management

- Follow the project's established state-management and dependency-injection conventions.
- Keep one clear owner for each piece of state.
- Distinguish transient widget state from state that must be shared, persisted, or coordinated.
- Make dependencies explicit where practical.
- Avoid service locators, global mutable state, and dependency-injection layers that add indirection without a concrete benefit.
- Follow the framework and package lifecycle requirements for subscriptions, controllers, and disposable resources.

Do not prescribe a specific package or rewrite working state management solely to conform to this architecture.

## Testing Strategy

Test behavior at the boundaries where tests provide meaningful confidence.

- **ViewModels:** Test state transitions, user actions, and coordination behavior.
- **Repositories:** Test data mapping, source coordination, and relevant error handling.
- **Services:** Test technical behavior using appropriate fakes, mocks, or controlled integration tests.
- **Domain:** Test meaningful business rules when they exist.
- **Views:** Test important rendering and user interaction behavior where it adds value.

Use `test/` for automated tests and `testing/` for reusable fakes, fixtures, or test models when that organization fits the project.

Do not create test scaffolding for layers that do not exist. Match validation effort to the risk, complexity, and impact of the change.

## When to Add Complexity

Add architectural structure only when there is a concrete reason, such as:

- A ViewModel has become difficult to understand or test.
- Business rules are duplicated across features.
- Multiple data sources require coordination.
- A technical dependency needs meaningful isolation.
- Several features share a stable capability.
- A requirement introduces real complexity that the current design cannot handle cleanly.

Before introducing another layer, interface, abstraction, or directory, explain what problem it solves and why a simpler option is insufficient.

Prefer refactoring toward a clearer design over speculative extensibility.

## Adapting Existing Projects

For existing applications:

1. Identify the current architecture, naming conventions, and state-management solution.
2. Preserve working boundaries and established patterns.
3. Apply MVVM concepts incrementally where they improve separation of concerns.
4. Avoid broad migrations unrelated to the requested change.
5. Do not force the example directory structure onto a project that already has a coherent organization.

The objective is not to make every project look identical. It is to make responsibilities clear and changes easier to understand, test, and maintain.

## Decision Rule

When choosing between a simple implementation and a more elaborate architecture, prefer the simple implementation unless the additional structure delivers a concrete, explainable benefit.

**MVVM is the recommended starting point, not an excuse to over-engineer.**
