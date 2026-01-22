# /documents — Document Types and Lifecycle

## Purpose

This folder defines the document types (Invoice, Proforma, Receipt, Delivery Note, Credit Note) and their lifecycle rules. Documents are the primary artifacts of the system—everything exists to create, manage, and render them.

## Responsibilities

- Define each document type's structure and required fields
- Define document status transitions (Draft → Issued → Paid/Cancelled)
- Define which documents reference which other documents
- Enforce document-specific business rules
- Define document-line item structures

## What Belongs Here

- Document type definitions (Invoice, Proforma, Delivery Note, Receipt, Credit Note)
- Document status enumerations and transition rules
- Document line item types and their validation rules
- Document relationship rules (Receipt references Invoice)
- Document date handling (Issue Date, Due Date, Print Date)
- Document totals calculation rules

## What Must NOT Go Here

- No numbering logic (see /numbering)
- No rendering or template selection (see /rendering, /templates)
- No persistence (see /infrastructure)
- No validation of user input format (see /validation)
- No PDF generation (see /exports)
- No UI component definitions

## Invariants

- Issued documents are immutable—no field changes after issue
- Document numbers are unique per business and document type
- A Receipt must reference exactly one Invoice
- Partial payments sum to no more than the Invoice total
- Credit Note amount cannot exceed the parent Invoice amount
- Line item totals must equal the sum of all line items
- Tax calculations must be mathematically consistent

## Example Concepts (Descriptive)

- **Invoice**: The primary sales document. Requests payment. Has an Invoice Number.
- **Proforma Invoice**: Preliminary document before正式 invoicing. Not legally binding.
- **Delivery Note**: Acknowledges goods transfer. References an Invoice.
- **Receipt**: Proof of payment. References an Invoice, may be partial.
- **Credit Note**: Reduces the amount owed. References an Invoice.
- **Document Line**: Item description, quantity, unit price, tax, discount.
- **Document Status**: Draft, Issued, Paid, Partially Paid, Cancelled, Overdue.

## Common Mistakes to Avoid

- **Status explosion**: Don't create too many granular statuses. Keep them meaningful.
- **Circular references**: A Credit Note references Invoice; never the reverse.
- **Mutable issued documents**: Never allow changes to issued documents. Issue a correction document instead.
- **Coupling to rendering**: Document structure should not be influenced by how it's printed.
- **Ignoring legacy continuation**: The numbering system must support manual start numbers for migration.

## Interactions

- `/documents` uses `/financials` for Money, Tax, and Discount calculations
- `/documents` uses `/numbering` to assign and validate document numbers
- `/documents` emits domain events consumed by `/notifications` and `/payments`
- `/rendering` transforms document data into visual output
- `/exports` serializes documents to file formats
- `/validation` ensures incoming document data meets structural requirements
