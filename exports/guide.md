# /exports — Export Formats

## Purpose

This folder handles exporting documents to various file formats (PDF, CSV, JSON, etc.). It serializes document data for sharing, backup, or integration with external systems.

## Responsibilities

- Serialize documents to export formats
- Handle format-specific requirements (PDF/A, CSV standards)
- Manage export file generation
- Support batch exports
- Validate export eligibility

## What Belongs Here

- Export format handlers (PDF, CSV, JSON, XML)
- File generation logic
- Batch export processing
- Export format specifications
- Export validation rules

## What Must NOT Go Here

- No document rendering (see /rendering)
- No business logic
- No template storage (see /templates)
- No data transformation beyond serialization
- No external API calls

## Invariants

- Exports are read-only snapshots
- Same document produces same export
- Exports don't modify source documents
- Export failures don't affect source data

## Example Concepts (Descriptive)

- **PDF Export**: Standard document PDF.
- **PDF/A Export**: Archival PDF format.
- **CSV Export**: Spreadsheet-compatible format.
- **JSON Export**: Data interchange format.
- **Batch Export**: Multiple documents in one package.
- **Export Validator**: Checks document eligibility.

## Common Mistakes to Avoid

- **Rendering in exports**: Render first, then export.
- **Large batch exports**: Handle memory and time limits.
- **Encoding issues**: Use consistent character encoding.
- **Non-deterministic output**: Ensure reproducibility.

## Interactions

- `/exports` calls /rendering for visual formats
- `/exports` reads from /documents
- `/exports` uses /templates for export structure
- `/exports` writes to /infrastructure (file storage)
- `/exports` may use /financials for data formatting
