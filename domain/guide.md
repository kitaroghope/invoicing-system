# /domain — Core Business Entities and Rules

## Purpose

This folder contains the foundational business entities, value objects, aggregates, and invariant rules that define what this invoicing system *is* and *does*. It is the source of truth for all business semantics—no business logic should exist outside this layer.

## Responsibilities

- Define domain entities (Business, Customer, Invoice, Receipt, etc.)
- Define value objects (Money, Quantity, DateRange, etc.)
- Define aggregate roots and their invariants
- Define domain events (e.g., `InvoiceIssued`, `PaymentReceived`)
- Enforce business rules that must hold true at all times
- Provide domain services for operations that don't naturally fit an entity

## What Belongs Here

- Pure domain objects with no infrastructure dependencies
- Business rules and invariants expressed as assertions
- Domain events (immutable records of something that happened)
- Enumerations of document types, statuses, and entity kinds
- Custom value types (Money with currency, Quantity with unit, etc.)
- Repository interfaces (abstract, not implementations)

## What Must NOT Go Here

- No database access code (repositories are interfaces only)
- No HTTP controllers, API endpoints, or routing
- No UI components, templates, or rendering logic
- No external service clients (email, payment gateways, etc.)
- No framework-specific syntax or annotations
- No configuration parsing or environment handling
- No validation of external input (that's /validation)

## Invariants

- Every aggregate must be internally consistent when created
- An aggregate root's invariants are checked before any state change
- Domain events are emitted only after successful state transitions
- Value objects are immutable and self-validating
- All monetary values must be expressed in a single currency per aggregate

## Example Concepts (Descriptive)

- **Business**: The entity that owns and issues documents. Has multiple businesses per user.
- **Customer**: Shared across businesses under the same user. Unique by email within a user's scope.
- **Invoice**: A financial document requesting payment. Has line items, totals, tax, and discounts.
- **InvoiceNumber**: Business-scoped, monotonically increasing, user-editable for legacy continuation.
- **Money**: An amount with an ISO 4217 currency code. Never floats.
- **TaxRate**: A percentage applied to line items or totals. Optional per line or document.

## Common Mistakes to Avoid

- **Anemic domain**: Creating entities that are just data bags without behavior. Encapsulate logic.
- **Leaking concerns**: Putting UI or infrastructure concerns here destroys modularity.
- **Ignoring invariants**: Don't allow invalid states. Fail fast and loudly.
- **Temporal coupling**: Don't assume creation order. Make aggregates valid in isolation.
- **Hybrid objects**: A thing is either an entity (has identity) or a value object (immutable). Not both.

## Interactions

- `/domain` defines interfaces that `/infrastructure` implements (repositories, event handlers)
- `/domain` entities are rendered by `/rendering` using templates from `/templates`
- `/validation` validates external input before it reaches domain objects
- `/ai` may analyze domain objects but never modifies them directly
- `/identity` provides the principal context for domain operations
