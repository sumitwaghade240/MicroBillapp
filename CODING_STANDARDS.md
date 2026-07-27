# MicroBill - Coding Standards

This document establishes the architecture patterns, database rules, state management guidelines, and coding style rules for the MicroBill project.

---

## 1. Clean Architecture Standard

Every module or feature folder must reside under `lib/features/` and follow the three-tier layer architecture.

```
lib/features/feature_name/
├── domain/
│   ├── entities/      # Pure business entities (no framework code or serialization logic)
│   ├── repositories/  # Abstract repository interfaces defining data access contracts
│   └── usecases/      # Use case business logic classes (single public call method)
├── data/
│   ├── models/        # Data models extending entities with serialization (toMap/fromMap)
│   └── repositories/  # Concrete implementations of domain repository contracts
└── presentation/
    ├── controllers/   # Riverpod Notifier/StateNotifier controllers representing state
    ├── screens/       # Main screen widgets (Scaffolds, GoRouter endpoints)
    └── widgets/       # Reusable feature-level UI components
```

### Layer Boundaries
1. **Domain Layer**: Must have zero dependencies on external packages, UI frameworks, or SQLite database libraries. It only interacts with other domain entities and repository contracts.
2. **Data Layer**: Communicates with the local database helper, maps relational structures to Models, and implements repository interfaces.
3. **Presentation Layer**: Consumes controllers, renders UI, captures forms, handles routing navigation, and manages layout responsive adaptions.

---

## 2. State Management (Riverpod)

* **Separation of Concerns**: UI widgets must not perform calculations, database writes, or parse strings directly. All updates must route through a Riverpod `StateNotifier` or `Notifier`.
* **State Immutability**: All states must use immutable classes. Always utilize `copyWith` to generate updated states.
* **Ref/Reader**: Use `ref.watch` in build methods to monitor state changes. Use `ref.read` in event callback handlers (e.g. `onPressed`) to trigger controller actions.

---

## 3. Dependency Injection (GetIt)

* **Central Registry**: All singletons (Database helper, repository implementations, use cases) are registered in `lib/core/di/injection.dart` using GetIt (`sl`).
* **Clean UI**: UI Screens must never import or call `sl<T>()` directly. Instead, Riverpod providers should resolve dependencies from GetIt and pass them down or inject them into StateNotifiers.

---

## 4. SQLite Database Guidelines

* **SQLite Enforcements**:
  - Always verify foreign keys are enabled using `PRAGMA foreign_keys = ON;`.
  - All SQL keywords in schema creation and queries must be written in **UPPERCASE** (e.g., `SELECT`, `FROM`, `WHERE`, `INSERT INTO`, `CREATE TABLE`).
* **Table & Column Naming**:
  - SQLite table names and column names must use `snake_case` (e.g. `client_id`, `company_name`).
  - Dart Entity and Model properties must map these to `camelCase` (e.g. `clientId`, `companyName`).
* **Referential Integrity**:
  - Utilize `ON DELETE RESTRICT` for records with associated critical transactions (e.g., preventing client deletion if invoices exist).
  - Utilize `ON DELETE CASCADE` for parent-child items (e.g. deleting invoice items when the parent invoice is deleted).

---

## 5. UI/UX & Responsive Layouts

* **Responsive Design**:
  - Width >= 800 width is treated as Desktop/Tablet landscape. Use sidebar navigation shells and split pane lists.
  - Width < 800 is treated as Mobile/Portrait. Use bottom navigation bars and full-screen push routes.
* **Styling Consistency**:
  - Spacing must follow the 8dp grid system (`const SizedBox(height: 8)`, `16`, `24`, `32`).
  - Color styling must reference `Theme.of(context).colorScheme` rather than hardcoded colors, ensuring instant Light/Dark mode transitions.
* **Component Modularity**: UI sections (cards, forms, list tiles) should be extracted into small, focused, stateless widgets.
