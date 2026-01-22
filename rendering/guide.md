# /rendering — Document Rendering Engine

## Purpose

This folder contains the rendering engine that transforms domain document objects into visual output (PDF, HTML, etc.). Rendering is a pure function: input document → output file. It never mutates data.

## Responsibilities

- Transform document domain objects into rendered output
- Apply template transformations
- Handle layout and pagination
- Generate deterministic, reproducible output
- Support multiple output formats

## What Belongs Here

- Rendering engines (PDF, HTML, plain text)
- Layout algorithms
- Pagination logic
- Template application logic
- Output format handlers
- Image and barcode generation

## What Must NOT Go Here

- No document creation or modification logic (see /documents)
- No business rule enforcement
- No validation of document content (see /validation)
- No template storage (see /templates)
- No UI components or web views
- No database access

## Invariants

- Same document with same template produces byte-identical output
- Rendering never modifies the source document
- Rendering is idempotent—can be repeated without side effects
- Output is deterministic given the same inputs
- Rendering failures are non-destructive (document remains unchanged)

## Example Concepts (Descriptive)

- **PDF Renderer**: Converts document to PDF/A for archival.
- **HTML Renderer**: Generates web-viewable HTML.
- **Barcode Generator**: Renders invoice number as machine-readable barcode.
- **Pagination Engine**: Splits multi-page documents correctly.
- **Layout Calculator**: Positions elements on the page.
- **QR Code Generator**: Renders payment QR codes.

## Common Mistakes to Avoid

- **Stateful renderers**: Don't maintain internal state across render calls.
- **Non-deterministic output**: Timestamps should be configurable, not "now".
- **Coupling to document structure**: Renderers should adapt to template changes.
- **Hardcoding layout**: Use templates for layout, code for logic.
- **Ignoring encoding**: All text must use consistent encoding.

## Interactions

- `/rendering` receives document data from /documents
- `/rendering` reads templates from /templates
- `/rendering` outputs to /exports for file generation
- `/rendering` may use /financials for number formatting
- `/rendering` may generate data for /notifications (e.g., embedded images)
