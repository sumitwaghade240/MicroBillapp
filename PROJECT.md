# MicroBill - Project Charter

## Project Vision
MicroBill is a 100% offline, privacy-first, commercial-grade billing and invoicing application. It is designed to empower small business owners, freelancers, and independent service providers with a robust tool to manage client relationships, track product inventory, generate professional A4 PDF invoices, and log payments without relying on cloud-based databases, external APIs, or SaaS subscription models.

All data is stored directly on the user's local hardware using a highly structured, transactional SQLite database.

## Target Users
* **Freelancers & Consultants**: Need to generate fast, customizable invoices for hourly or project-based services.
* **Small Retailers & Service Providers**: Require a simple way to maintain standard product stock levels, pricing, and record customer invoice histories.
* **Field Service Technicians**: Require offline-first software that runs on laptops or mobile devices in locations without cellular coverage.
* **Privacy-Conscious Entities**: Organizations or individuals who refuse to host customer details or financial records on cloud servers.

## Business Goals
1. **Privacy-First Accounting**: Guarantee data security by maintaining 100% local operation with no telemetry, internet trackers, or remote APIs.
2. **High System Reliability**: Zero dependence on internet connectivity. Invoices can be drafted, modified, exported, and printed in fully disconnected environments.
3. **No Hidden Costs**: Avoid ongoing SaaS subscriptions. One-time acquisition, infinite local operation.
4. **Performance & Speed**: Sub-millisecond database queries, instant page loads, and native desktop-level performance on Windows, Linux, and macOS alongside Android.

## Definition of Done (DoD)
To ensure the application meets commercial-grade standards, every feature must meet the following criteria before being marked as "Done":

### Code Quality
* Follows **Clean Architecture** conventions (Separation of Data, Domain, and Presentation layers).
* Zero compile errors, zero warnings, and zero lint issues reported by `flutter analyze`.
* No placeholder text, no hardcoded demo strings, and no dummy models. All edge cases handled.
* Code comments and Dartdoc descriptions provided for all public-facing APIs, repositories, and entities.

### UI/UX Consistency
* Pass the **UI/UX Screen Checklist** in [.agents/AGENTS.md](file:///c:/Projects/microBillapp/.agents/AGENTS.md).
* Dark Mode and Light Mode support with sufficient color contrast.
* Fully responsive layout (Adaptive layout for Mobile, Tablet, and Desktop screen widths).
* Accessibility labels (`Semantics`) included on all input fields and critical buttons.

### Database Design
* All changes align with the **Database Design Protocol** in [.agents/AGENTS.md](file:///c:/Projects/microBillapp/.agents/AGENTS.md).
* Foreign keys enforced with relational consistency (`ON DELETE RESTRICT` or `ON DELETE CASCADE`).
* Database queries optimized with appropriate indexes on search/foreign keys.

### Testing
* At least **80% code coverage** for the Domain and Data layers (Unit tests).
* Integration/Widget tests verified for critical user navigation paths and form submissions.
* Smoke tests verified successfully across Android and Windows desktop environments.
