# Microsoft Dynamics 365 F&O: Credit Limit Validation & Batch Audit Extension

An enterprise portfolio project demonstrating custom **X++ development** in Microsoft Dynamics 365 Finance & Operations (F&O). This project implements real-time credit limit validations, an asynchronous batch auditing pipeline, and OData API integration patterns without modifying Microsoft standard source code.

---

## 📌 Business Scenario

When an enterprise customer exceeds an allocated credit threshold (e.g., PKR 1,000,000), business risk increases. This project addresses two operational needs:

1. **Real-time Validation:** Prevent saving or updating customer records in `CustTable` if a high credit limit is set without an assigned credit rating.
2. **Automated Batch Processing:** Run a scheduled, off-peak background process to audit all high-credit accounts and flag mandatory credit limit controls across the system.

---

## 🏗️ Technical Architecture & Key Features

* **Chain of Command (CoC) Extensions:** Extends standard `CustTable` table logic using `[ExtensionOf]` and `next` keywords, adhering to Microsoft's open-closed extension model.
* **SysOperation Framework:** Implements a decoupled batch pipeline using the Model-View-Controller (MVC) design pattern (`DataContract`, `Service`, `Controller`).
* **Explicit SQL Transactions:** Utilizes native `ttsbegin` and `ttscommit` transaction blocks with `forUpdate` record locks for reliable bulk database operations.
* **OData v4 REST Integration Concept:** Models custom customer credit attributes as structured JSON payloads for external client applications (e.g., Spring Boot, React, or Power Apps).

---

## 📂 Project Structure

```text
d365-fo-credit-limit-integration/
├── src/
│   ├── Extensions/
│   │   └── CustTable_Extension.xpp         # Chain of Command (CoC) table validation
│   └── SysOperation/
│       ├── CreditAuditContract.xpp         # Data Transfer Object (DTO) for batch inputs
│       ├── CreditAuditService.xpp          # Core business & transactional logic
│       └── CreditAuditController.xpp       # Batch execution orchestrator
├── payload/
│   └── odata-customer-credit.json          # OData REST API JSON payload sample
└── README.md
