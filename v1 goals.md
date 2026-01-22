# V1_SCOPE.md — Invoice System v1 Scope & Freeze

## Purpose

This document defines the **explicit scope, guarantees, and non-goals** of Version 1 (v1)
of the Invoice System.

Its purpose is to:
- Prevent scope creep
- Preserve architectural integrity
- Set contributor expectations
- Lock invariants before implementation

If something is **not listed here**, it is **out of scope for v1**.

---

## Core Vision (Unchanged)

The system is a **deterministic invoice document compiler** that transforms structured
commercial data into reproducible, print-ready documents.

AI is optional.  
Rendering is deterministic.  
Accounting correctness is non-negotiable.

---

## ✅ IN SCOPE FOR v1

### 1. Identity & Access
- Multi-user accounts
- Multiple businesses per user
- Shared customers across businesses
- Role separation (Owner / Collaborator)
- Bot protection (reCAPTCHA or equivalent)

---

### 2. Business & Numbering
- Per-business document numbering
- Numeric-only sequences
- Render-only prefixes
- Legacy invoice book continuation
- Sequence locking & audit metadata

---

### 3. Commercial Document Types
- Proforma Invoice
- Invoice
- Delivery Note
- Receipt
- Credit Note (flat-amount, placeholder)

Each document type:
- Has its own numbering
- Has immutable issued state
- Has its own template

---

### 4. Financial Logic
- Optional taxes (e.g. Uganda VAT 18%)
- Optional discounts
- Optional vouchers / credits
- Partial payments
- Multiple receipts per invoice
- Outstanding balance tracking

Invoice totals are immutable after issuance.

---

### 5. Document Engine
- Domain vs Document separation
- Deterministic compilation
- Pagination & multi-page support
- Line item detail columns
- Watermarks
- QR codes
- PDF & print-safe rendering

---

### 6. Optional Modules (v1 Placeholders)

#### A. Credit Notes
- Flat amount only
- Reduces outstanding balance
- No line-item recomputation

#### B. Currency
- Single currency per invoice
- No FX conversion

#### C. Exports
- CSV / JSON / PDF bundle
- Read-only
- No external sync

#### D. Notifications
- Manual send only
- No automation

---

## ❌ OUT OF SCOPE FOR v1 (NON-GOALS)

- Automated refunds
- FX conversion or rate engines
- Tax authority APIs
- Accounting software sync
- Scheduled reminders
- Webhooks
- Payment gateways
- Inventory management
- Advanced UI editors

---

## 🔒 Architectural Invariants (Frozen)

- Domain data never mixes with layout logic
- Compiler is stateless and deterministic
- Rendering never mutates data
- Invoice numbers are numeric only
- Issued documents are immutable
- AI cannot bypass validation
- No circular dependencies

---

## 🧠 Versioning Rules

- v1 focuses on correctness over completeness
- Backward compatibility is required for v1.x
- Breaking changes require v2

---

## 📌 Final Note

This document represents an **architecture freeze** for v1.

Any change requires architectural review.

---

End of V1 scope.
