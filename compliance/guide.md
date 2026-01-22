# /compliance — Regulatory and Tax Compliance

## Purpose

This folder defines compliance rules, tax jurisdiction handling, and regulatory requirements. It ensures documents meet legal and tax obligations. This is a placeholder for v1 compliance concerns—tax filing integration is out of scope.

## Responsibilities

- Define tax jurisdiction rules and rates
- Enforce document requirements per jurisdiction
- Support tax-inclusive and tax-exclusive pricing
- Generate compliance reports
- Handle e-invoicing mandates (where applicable)
- Manage document archiving requirements

## What Belongs Here

- Tax jurisdiction definitions
- Compliance rule engines
- Regulatory report generation
- Document requirement validators
- Archival specification handling
- E-invoicing format support

## What Must NOT Go Here

- No tax filing API integration (external)
- No payment gateway compliance
- No legal advice or interpretation
- No automatic tax calculation (see /financials)
- No audit logging (see /security)

## Invariants

- Documents meet basic requirements for their jurisdiction
- Tax calculations are consistent with /financials
- Compliance rules are read-only at runtime
- Required fields are validated before document issuance

## Example Concepts (Descriptive)

- **Jurisdiction**: Geographic or tax authority region (e.g., Uganda VAT).
- **Tax Requirement**: Mandatory fields or formatting per jurisdiction.
- **E-Invoicing Format**: Structured format for government submission.
- **Archival Period**: How long documents must be retained.
- **Compliance Report**: Summary of document compliance status.
- **Tax Registration**: Business tax identifiers per jurisdiction.

## Common Mistakes to Avoid

- **Hardcoding tax rates**: Use configurable jurisdiction rules.
- **Ignoring jurisdiction differences**: One size doesn't fit all.
- **Compliance as afterthought**: Build compliance into document structure.
- **Over-complicating**: Start with basic requirements.

## Interactions

- `/compliance` uses /financials for tax calculations
- `/compliance` validates /documents before issuance
- `/compliance` may export data to /exports
- `/compliance` settings come from /config
- `/compliance` integrates with /security for audit
