# /customers — Customer Management

## Purpose

This folder defines customer entities and their management. Customers are shared across businesses under the same user, allowing for centralized address books and unified customer history.

## Responsibilities

- Manage customer profiles (name, contact, address)
- Track customer metadata (tags, categories, notes)
- Support customer search and deduplication
- Maintain customer-business relationships
- Handle customer merging and archival

## What Belongs Here

- Customer entity definition
- Customer contact information
- Customer address management
- Customer tags and categorization
- Customer notes and history
- Customer deduplication rules

## What Must NOT Go Here

- No customer-specific pricing (business-level concern)
- No document creation (see /documents)
- No payment tracking (see /payments)
- No email sending (see /notifications)
- No customer-facing portal logic

## Invariants

- Customers are unique per user (not per business)
- A customer can belong to multiple businesses under the same user
- Customer email is unique per user (cannot have two customers with same email)
- Customers can be archived but not hard-deleted if they have documents
- Merged customers preserve document history

## Example Concepts (Descriptive)

- **Customer**: The entity receiving goods/services and invoices.
- **Customer Contact**: Email, phone, and other contact methods.
- **Customer Address**: Billing and shipping addresses.
- **Customer Tag**: Categorization for filtering and reporting.
- **Customer Note**: Internal notes about the customer.
- **Customer Merge**: Combining duplicate customer records.
- **Customer Archive**: Soft-delete for inactive customers.

## Common Mistakes to Avoid

- **Business-scoped customers**: Customers are user-scoped, not business-scoped.
- **Hard deletes**: Never delete customers with document history.
- **Email case sensitivity**: Normalize emails before comparison.
- **Ignoring duplicates**: Implement deduplication on create.
- **Stale data**: Update customer info doesn't retroactively change documents.

## Interactions

- `/customers` provides data to /documents (invoice recipients)
- `/customers` is searched by /editor for autocomplete
- `/customers` uses /identity for access control
- `/customers` uses /infrastructure for persistence
- `/payments` references customers for payment attribution
- `/notifications` uses customer contact info
