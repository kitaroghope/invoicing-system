# /numbering — Document Numbering System

## Purpose

This folder defines the rules and logic for assigning unique, sequential document numbers to each business's documents. Document numbering is the primary lookup mechanism and provides legal audit trails.

## Responsibilities

- Generate and validate document numbers per business and document type
- Support numeric-only sequences with optional render-only prefixes
- Handle legacy invoice book continuation (manual start number)
- Ensure uniqueness within business scope
- Enforce sequencing rules (monotonically increasing)

## What Belongs Here

- Numbering strategy definitions
- Sequence generation and reservation logic
- Prefix handling (for rendering only, not for ordering)
- Legacy continuation support
- Number format validation rules
- Gap handling policies

## What Must NOT Go Here

- No persistence of sequences (storage is in /infrastructure)
- No document creation logic (see /documents)
- No formatting for display vs. storage distinction
- No UI for number assignment
- No validation of document content (see /validation)

## Invariants

- Document numbers are unique within (Business, DocumentType) scope
- Numbers are assigned in strictly increasing order per sequence
- Once assigned, a number cannot be reassigned or skipped
- Prefixes are cosmetic—ordering is determined by numeric portion only
- Legacy continuation requires explicit manual start; system won't guess
- A document without a number cannot be issued

## Example Concepts (Descriptive)

- **Sequence**: A per-business, per-document-type numbering stream
- **Numeric Only**: The actual sequence number (e.g., 0001, 0002, 1005)
- **Render Prefix**: Optional prefix prepended during rendering (e.g., "INV-0001")
- **Legacy Continuation**: The ability to specify "start at 1453" for migration
- **Sequence Gap**: A missing number in the sequence (should not happen in normal operation)
- **Number Format**: Defines padding, leading zeros, maximum digits

## Common Mistakes to Avoid

- **Coupling prefix to sequence**: The prefix is for display only. Two invoices "INV-001" and "INV-002" are 001 and 002, not "INV-001".
- **Allowing sequence reset**: Never reset to 1 at year boundaries unless business explicitly configures this.
- **Not supporting gaps**: The system may generate non-contiguous numbers if numbers are reserved but not used.
- **Inconsistent validation**: Don't accept "001" in one place and "1" in another without normalization.

## Interactions

- `/numbering` is used by `/documents` when a document is issued
- `/numbering` reads/writes sequence state via `/infrastructure` repositories
- `/rendering` may apply prefixes during document rendering
- `/exports` includes document numbers in output files
- `/validation` validates user-provided numbers for legacy continuation
