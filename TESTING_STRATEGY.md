# MicroBill - Testing Strategy

This document outlines the testing methodologies, tools, and protocols to maintain a commercial-grade quality standard for MicroBill v1.0.

---

## 1. Automated Test Plan

We implement three layers of testing to guarantee complete system correctness:

```
┌──────────────────────────────────────────────┐
│            Integration Tests (E2E)           │  <- Critical user navigation flows
├──────────────────────────────────────────────┤
│             Widget/UI Tests                  │  <- Screen rendering, validation feedback
├──────────────────────────────────────────────┤
│          Unit Tests (Domain & Data)          │  <- Math, DB queries, validation rules
└──────────────────────────────────────────────┘
```

### 1.1 Unit Tests (Target: >80% Coverage)
* **Domain Layer Use Cases**: Verify that business rules function correctly (e.g., rejecting negative pricing, preventing empty client names).
* **Data Models**: Validate serialization and deserialization maps to ensure SQLite data transfers match class structures.
* **Math Engines**: Write exhaustive tests for calculations (subtotal, tax sum, flat/percentage discounts, payments deduction).
* **SQLite CRUD Tests**: Use in-memory SQLite instances or mock database handlers to test creation, reading, and constraint failures (like unique invoice numbering).

### 1.2 Widget & UI Tests
* **Form Validations**: Verify that error labels appear when invalid values are entered (e.g. malformed email syntax in client inputs).
* **State Updates**: Verify that the UI reflects state transitions (e.g., showing a progress spinner when loading database records, then showing list items).
* **Adaptive Layouts**: Simulate different screen sizes (e.g., 400px width vs. 1200px width) to verify that widgets arrange themselves correctly (mobile bottom bar vs. desktop sidebar).

---

## 2. Test Isolation & Mocking Strategy

To isolate our test targets from system dependencies (like files, physical storage paths, or platform specific binaries):

1. **In-Memory SQLite**: For database testing, configure SQLite to run in-memory (`:memory:`) to ensure fast, isolated, and concurrent test execution.
2. **Mock Repositories**: Create stub/mock repository classes implementing domain repository contracts. This allows presentation-layer widgets and controllers to be tested without reading database files.
3. **Provider Overrides**: Utilize Riverpod's `ProviderContainer(overrides: [...])` to swap actual database-backed repositories with mock implementations in widget tests.

---

## 3. Regression Testing Protocol

Whenever a bug is detected or a feature is refactored:

1. **Write Regression Test**: Create an automated test that isolates and reproduces the bug before writing the fix.
2. **Apply the Fix**: Update the code to resolve the error.
3. **Execute Suite**: Run `flutter test` to verify that the regression test passes and no existing features are broken.
4. **Static Code Quality**: Execute `flutter analyze` to ensure zero lint warnings or compilation errors are present.

---

## 4. Test Execution Command

Run the complete suite of automated unit and widget tests:
```bash
flutter test
```
