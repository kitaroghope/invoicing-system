# /templates — Document Templates

## Purpose

This folder contains all document templates that define how documents look when rendered. Templates are the visual specification—they separate structure (data) from presentation (layout). Templates are declarative, not executable code.

## Responsibilities

- Store declarative template definitions for each document type
- Define placeholder variables and their substitution rules
- Specify layout, typography, and visual elements
- Support multiple template versions and variants
- Define print-friendly specifications

## What Belongs Here

- Template files (HTML, LaTeX, XML-based, or structured data formats)
- Template variable definitions
- Style specifications (CSS, formatting rules)
- Template metadata (version, supported document types)
- Template partials and components

## What Must NOT Go Here

- No executable code or logic in templates
- No database access or external calls
- No validation logic
- No business rules
- No rendered output files

## Invariants

- Templates are read-only at runtime
- Templates use only declared variables
- Missing template variables result in clear errors, not silent omission
- Templates are versioned and compatible with document structure versions
- A document can always be re-rendered with its original template

## Example Concepts (Descriptive)

- **Invoice Template**: Defines invoice visual structure (header, line items table, totals).
- **Header Partial**: Reusable document header component.
- **Footer Partial**: Reusable document footer with legal text.
- **Variable**: `{{invoice.number}}`, `{{customer.name}}`.
- **Loop Directive**: `{{#each line_items}}...{{/each}}`.
- **Style Block**: CSS rules for HTML-based templates.

## Common Mistakes to Avoid

- **Logic in templates**: Keep templates declarative. Business logic belongs in /domain.
- **Hardcoded values**: Use variables for anything that might change.
- **Tight coupling to rendering engine**: Use standard template formats where possible.
- **Ignoring template versioning**: Templates evolve; track compatibility.
- **Embedding sensitive data**: Templates may be logged or cached.

## Interactions

- `/templates` is read by `/rendering` during document generation
- `/templates` references variables defined in `/documents`
- `/editor` may use templates for preview (but not modify them)
- `/exports` packages rendered output, potentially with original template reference
