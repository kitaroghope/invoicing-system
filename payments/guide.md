# /payments — Payment Processing

## Purpose

This folder defines payment recording and tracking. It handles the association of payments with invoices, partial payment management, and payment status updates. It does not process payments (gateway integration).

## Responsibilities

- Record payments against invoices
- Track partial payments and their accumulation
- Manage payment status (paid, partial, overdue)
- Support multiple receipts per invoice
- Handle payment reversals and refunds
- Generate payment receipts

## What Belongs Here

- Payment entity definition
- Payment-invoice association
- Partial payment tracking
- Payment status enumeration
- Payment reversal logic
- Payment receipt generation

## What Must NOT Go Here

- No payment gateway integration (external concern)
- No payment processing (only recording)
- No currency conversion (external concern)
- No bank API calls
- No payment scheduling or reminders (see /notifications)

## Invariants

- A payment cannot exceed the invoice total (except overpayment rules)
- Partial payments sum must not exceed invoice total
- A receipt is generated for each payment
- Once recorded, payments can only be reversed (not deleted)
- Overpayment handling is configurable (refund vs. credit note)

## Example Concepts (Descriptive)

- **Payment**: Money received, associated with an invoice.
- **Partial Payment**: A payment covering less than the full invoice amount.
- **Overpayment**: Payment exceeding invoice total.
- **Payment Reversal**: Voiding a payment (creates audit trail).
- **Payment Method**: Cash, bank transfer, mobile money, card.
- **Payment Reference**: Bank transfer number, transaction ID.
- **Receipt**: Document proving payment received.

## Common Mistakes to Avoid

- **Allowing overpayment**: Define and enforce overpayment policy.
- **Deleting payments**: Always reverse, never delete.
- **Race conditions**: Handle concurrent payment recording.
- **Mismatched currencies**: Payments must match invoice currency.
- **Losing audit trail**: Every payment change creates history.

## Interactions

- `/payments` references /documents (invoices)
- `/payments` uses /financials for amount calculations
- `/payments` emits events for /notifications
- `/payments` generates receipts via /rendering
- `/payments` updates invoice status in /documents
- `/payments` uses /infrastructure for persistence
