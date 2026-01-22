# /editor — Document Editing Interface

## Purpose

This folder defines the document editing interface layer—the UI concerns for creating and modifying documents before they are issued. It is strictly about user interaction, not business logic or persistence.

## Responsibilities

- Define editing workflows (create, edit, duplicate, convert)
- Handle user input collection and state management
- Provide real-time validation feedback
- Manage draft document state
- Coordinate between domain and presentation

## What Belongs Here

- Editor state management
- Input form definitions and handlers
- Draft persistence coordination
- Real-time calculation previews
- Undo/redo logic for editing
- Clipboard and import utilities

## What Must NOT Go Here

- No business rule enforcement (see /domain)
- No document validation (see /validation)
- No rendering logic (see /rendering)
- No API endpoints (see /infrastructure)
- No authentication (see /identity)
- No template storage (see /templates)

## Invariants

- Drafts can always be discarded without affecting issued documents
- Editing an issued document creates a new document or correction
- Pending changes are explicitly saved or discarded
- Editor state is local until persisted

## Example Concepts (Descriptive)

- **Line Item Editor**: Manages adding/removing line items.
- **Customer Autocomplete**: UI component for customer selection.
- **Draft Manager**: Handles temporary storage of in-progress documents.
- **Calculation Preview**: Shows running totals as user types.
- **Conversion Wizard**: Converts Proforma to Invoice.
- **Import Handler**: Bulk line item import from external sources.

## Common Mistakes to Avoid

- **Business logic in UI**: Calculations must use /financials, not UI code.
- **Bypassing validation**: All user input must go through /validation.
- **Stateful editors**: Editing should be stateless; server is source of truth.
- **Direct mutation**: Don't mutate domain objects directly; use commands.
- **Tight coupling to framework**: Keep UI concerns isolated.

## Interactions

- `/editor` calls /validation for input validation
- `/editor` coordinates with /documents for draft operations
- `/editor` uses /financials for calculation previews
- `/editor` may use /ai for suggestions during editing
- `/editor` requests rendering from /rendering for previews
- `/editor` persists drafts via /infrastructure
