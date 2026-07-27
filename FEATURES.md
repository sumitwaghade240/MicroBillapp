# MicroBill - Feature Specifications

This document outlines the detailed functional requirements and design specifications for each core feature in MicroBill v1.0.

---

## 1. Dashboard & Reports
* **Core Goal**: Provide an immediate, premium visual summary of business health upon opening the application.
* **UI/UX Widgets**:
  - **KPI Cards**: Total Invoiced, Collected (Paid), Outstanding (Unpaid), and Active Client count. Features hover effects and micro-scale animations.
  - **Sales Charts**: Weekly or monthly visual bar/line chart mapping earnings using `fl_chart`.
  - **Urgent Action Center**: Lists invoices nearing due dates, overdue invoices, and items that have fallen below warning stock quantities.
  - **Quick Actions Panel**: Direct buttons to "Create Invoice", "Add Client", and "Add Product".

## 2. Client Directory
* **Core Goal**: Maintain customer contact lists, addresses, and tax information locally.
* **Fields**: Unique ID (UUID), Full Name, Company Name (Optional), Email (Optional), Phone Number (Optional), Billing Address (Optional), Shipping Address (Optional), Tax/VAT Registration Number (Optional), Timestamps.
* **UI/UX Widgets**:
  - **Responsive Split View (Desktop)**: Client list on the left with a real-time text filter (search-by-name/company/email). Selecting a client displays their full contact profile and invoice history on the right.
  - **Compact List (Mobile)**: List page with search input that pushes to separate details and form screens.
  - **Auto-Address Match**: A single checkbox during client creation to copy the billing address to the shipping address.

## 3. Product & Service Inventory
* **Core Goal**: Manage pricing catalog and inventory stock levels.
* **Fields**: Unique ID (UUID), SKU/Product Code (Optional), Name, Description (Optional), Unit Price, Unit of Measure (e.g., pcs, hours, kg), Tax Rate (%), Stock Quantity, Timestamps.
* **UI/UX Widgets**:
  - **Stock Status Badge**: Color-coded badges indicating "In Stock" (Green), "Low Stock" (Amber), or "Out of Stock" (Red) based on a configurable warning limit.
  - **Search & Sort Headers**: Sort catalog by name, price, stock levels, or SKUs.
  - **Price Formatters**: Automatically localized currency markers based on system preferences.

## 4. Invoice Generator
* **Core Goal**: Draft and calculate customer bills with absolute precision.
* **Fields**: Unique ID, Unique Invoice Number (e.g. `INV-0001`), Client ID, Issue Date, Due Date, Status (Draft, Sent, Paid, Overdue, Cancelled), Subtotal, Discount Amount, Discount Type (percentage/flat), Tax Total, Grand Total, Paid Amount, Balance Due, Notes, Invoice Terms.
* **Invoice Items**: Maps products to quantity, unit price, tax rate, discount, subtotal, and total.
* **UI/UX Widgets**:
  - **Interactive Invoice Builder**: Select a client from a dropdown, add products from the catalog as line items, dynamically modify quantities/pricing, and see subtotal, taxes, and totals recalculate live.
  - **Status Badges**: Premium indicators for payment status.
  - **Delete/Void Dialog**: Safety verification step before deleting or voiding any recorded invoice.

## 5. Payments Registry
* **Core Goal**: Record payment transactions against outstanding balances.
* **Fields**: Unique ID, Invoice ID, Amount Paid, Transaction Date, Payment Method (Cash, Bank Transfer, Card, Check, Other), Reference Number/Notes.
* **Business Logic**:
  - Automatically updates invoice status to "Paid" if the balance becomes zero, or "Partial" if a partial payment is recorded.
  - Prevents recording payments exceeding the balance due.

## 6. Document Exporter (PDF)
* **Core Goal**: Generate production-grade, print-ready documents without cloud dependancies.
* **Features**:
  - **A4 PDF Template**: Premium layout with clean alignment, business address block, logo container, client details, transaction table, summary calculations, payment instructions, and terms block.
  - **Print Dialog Integration**: Native operating system print preview and print action.
  - **Local Save**: File picker dialog to save PDF to a chosen directory.

## 7. Business Settings & Backup
* **Core Goal**: Configure app details and manage local database backups.
* **Features**:
  - **Seller Profile Form**: Business Name, logo file path, email, phone, website, billing address, Tax ID.
  - **Global Preferences**: Default currency symbol, default tax labels (VAT/GST/TAX), default payment terms (e.g., 14 days, 30 days).
  - **Data Portability**: Export database to a standard `.json` or `.db` backup file. Import backup file to overwrite/restore data.
