# /business — Business Profile Management

## Purpose

This folder defines the business profile entity—the organization or individual issuing documents. Each user can manage multiple businesses. Business profiles contain all settings and branding relevant to issued documents.

## Responsibilities

- Manage business profiles (name, address, contact)
- Define business-specific settings (currency, tax number, logo)
- Manage document defaults per business
- Handle business-specific numbering sequences
- Support business branding customization

## What Belongs Here

- Business entity definition
- Business address and contact information
- Business branding (logo, colors, typography)
- Business-specific configuration (currency, timezone, tax settings)
- Default line item categories
- Business-scoped settings

## What Must NOT Go Here

- No user management (see /identity)
- No customer data (see /customers)
- No document operations (see /documents)
- No payment processing (see /payments)
- No rendering logic (see /rendering)

## Invariants

- Each business is owned by exactly one user
- Business names are unique per user
- A business has exactly one active profile at a time
- Business settings are validated before use
- Tax numbers are validated against jurisdiction rules

## Example Concepts (Descriptive)

- **Business Profile**: The entity's public identity on documents.
- **Business Address**: Physical and postal addresses.
- **Tax Identifier**: VAT number, EIN, or local equivalent.
- **Logo Asset**: The business's visual mark for documents.
- **Default Currency**: The currency used for new documents.
- **Business Branding**: Colors, fonts, and visual style.
- **Document Defaults**: Default payment terms, line item templates.

## Common Mistakes to Avoid

- **Duplicate businesses**: Prevent same business from being created twice.
- **Orphaned data**: Delete related documents when business is deleted.
- **Global settings**: Don't assume one-size-fits-all settings.
- **Hardcoded addresses**: Use templates for document-specific formatting.
- **Mixed currencies**: Default currency applies to new documents only.

## Interactions

- `/business` provides profile data to /documents
- `/business` provides templates to /rendering
- `/business` sequences are managed by /numbering
- `/business` settings come from /config
- `/business` customers are in /customers
- `/business` uses /identity for ownership verification
