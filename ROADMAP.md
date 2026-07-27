# MicroBill v1.0 - Future Roadmap

This roadmap outlines the milestones for building the commercial-grade MicroBill application.

---

## Phase 1: Planning & Setup
- [x] Initial design specifications and architecture modeling.
- [x] Project charter, requirements, standards, and testing strategy.

## Phase 2: Core Foundation (Current)
- [/] Initialize project boilerplate and folder structures.
- [/] Set up Dependency Injection, Logging, and Routing frameworks.
- [/] Design the global Material 3 theme (Light & Dark profiles).
- [/] Develop the adaptive shell navigation layout (Desktop sidebar vs. Mobile bottom bar).
- [/] Standardize error handling and Result structures.

## Phase 3: Inventory & Product Management
- [ ] Implement database schema for `products` table including SKUs and inventory tracking.
- [ ] Build Data and Domain models for products.
- [ ] Build product list and search views with stock level warnings.
- [ ] Design product forms with pricing, unit, and tax configurations.
- [ ] Add product unit tests and widget tests.

## Phase 4: Client Management
- [/] Implement database schema for `clients` table.
- [/] Build client details, list, and form screens.
- [/] Add address fields, tax ID registration inputs, and validation checks.
- [/] Add client unit tests and widget tests.

## Phase 5: Invoicing Engine & Calculations
- [ ] Design `invoices` and `invoice_items` schemas (supporting foreign keys & cascade deletes).
- [ ] Write invoicing math engine (handles subtotal, discount rates, tax sums, and payment updates).
- [ ] Build interactive Invoice Form (add items, select client, apply discounts in real-time).
- [ ] Display invoice listing filtered by payment states (Draft, Sent, Paid, Overdue).
- [ ] Implement unit tests validating tax/discount calculations.

## Phase 6: Offline Document Exporter
- [x] Implement PDF generator using `pdf` and `printing` packages.
- [x] Format beautiful, professional A4 invoices with logo, item grids, and payment terms.
- [x] Implement file save/export dialogs for local storage (desktop & mobile).
- [x] Configure native print dialog integrations.

## Phase 7: Analytics & Dashboards
- [x] Build business metrics controller calculating unpaid totals and earnings.
- [x] Design interactive dashboard with charts (`fl_chart`) for weekly/monthly sales curves.
- [x] Add "Low Stock" alerts and "Overdue Invoices" notifications panels.

## Phase 8: Profile Settings & Data Portability
- [ ] Build Profile form for custom Business details (Logo, address, Tax identification).
- [ ] Build backup utility (JSON/CSV export & restore tool) for local database backups.
- [ ] Run complete regression testing across Android and Windows Desktop.

---

## Future Goals (v2.0+)
* **SQLCipher Integration**: Encrypt SQLite database locally using a master password.
* **Workspace Environments**: Switch between multiple separate local business directories.
* **Smart Scan**: Capture receipt images locally and attach them to invoice records.
* **Multi-Currency Accounts**: Support invoice generation in foreign currencies with manual exchange rate overrides.
