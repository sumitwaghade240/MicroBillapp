# MicroBill - System Requirements

This document details the functional and non-functional requirements for MicroBill v1.0.

---

## 1. Functional Requirements (FR)

### FR1: Client Directory
* **FR1.1**: The system must allow users to create, read, update, and delete (CRUD) client profiles.
* **FR1.2**: Each client profile must store name, optional company, email, phone, billing address, shipping address, and Tax ID.
* **FR1.3**: The system must check if a client has outstanding or paid invoices before permitting deletion. If invoices exist, deletion must be blocked to preserve relational integrity.
* **FR1.4**: Users must be able to search the client list by name, company name, or email in real-time.

### FR2: Product & Service Inventory
* **FR2.1**: The system must allow users to CRUD products or service items.
* **FR2.2**: Each product record must store SKU, name, description, unit price, tax rate (%), stock level, and unit of measure.
* **FR2.3**: The system must display a warning status (Amber/Red) when a product's stock drops below 5 units.

### FR3: Invoicing Engine
* **FR3.1**: The system must support generating invoices linked to a registered client.
* **FR3.2**: Each invoice must generate a unique, sequential invoice number.
* **FR3.3**: The invoice builder must support adding multiple line items, adjusting quantities, applying item-level or invoice-level discounts (flat rate or percentage), and calculating taxes.
* **FR3.4**: Invoices must support status flows: `Draft` -> `Sent` -> `Paid` / `Overdue` / `Cancelled`.

### FR4: Payments & History
* **FR4.1**: The system must support recording partial or full payments against outstanding invoices.
* **FR4.2**: The system must log payment details (date, amount, method, reference number).
* **FR4.3**: Recording a payment must immediately update the invoice's balance due and transition the invoice status automatically.

### FR5: PDF Document Exporter
* **FR5.1**: The system must render professional A4-sized PDF invoices locally.
* **FR5.2**: The system must integrate with the host OS's native print dialogue.
* **FR5.3**: Users must be able to export the generated PDF directly to a folder on local storage.

### FR6: Seller Profile & Database Portability
* **FR6.1**: The system must maintain a single-record seller profile for the user's own business details.
* **FR6.2**: The system must allow exporting the entire local SQLite database to a backup file.
* **FR6.3**: The system must allow importing a backup database file, overwriting the current state.

---

## 2. Non-Functional Requirements (NFR)

### NFR1: 100% Offline operation
* **NFR1.1**: The system must run completely local. It must not make HTTP requests, resolve remote URLs, or connect to cloud databases (no Firebase, Supabase, or AWS).
* **NFR1.2**: All dependencies must be packaged locally; no web assets or remote fonts should load at runtime.

### NFR2: Cross-Platform Compatibility
* **NFR2.1**: The application codebase must compile natively on **Android (API 21+)** and **Windows (10/11)**.
* **NFR2.2**: Desktop configurations must support mouse, trackpad, and keyboard integrations (e.g. scrollbars, hover states, tab-focusing inputs).

### NFR3: Database Integrity & Relationships
* **NFR3.1**: Local storage must use a transactional **SQLite** engine.
* **NFR3.2**: SQLite foreign keys must be active (`PRAGMA foreign_keys = ON`) to preserve relationship constraints.
* **NFR3.3**: All relational changes (e.g. deleting an invoice) must execute using cascade triggers or checks.

### NFR4: Performance & Latency
* **NFR4.1**: The app must startup and render the dashboard view in **under 300ms** on desktop and **under 500ms** on mobile.
* **NFR4.2**: SQLite database queries (read/write) must complete in **under 15ms** under standard database sizes (<5000 invoices).

### NFR5: Security & Privacy
* **NFR5.1**: The application must require no network permissions in its final release build.
* **NFR5.2**: All database backups and exports must reside in user-owned local directories.
