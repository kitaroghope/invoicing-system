# /infrastructure — Technical Infrastructure

## Purpose

This folder implements technical infrastructure: database access, file storage, external service clients, and system-level integrations. It provides implementations of abstractions defined elsewhere.

## Responsibilities

- Implement repository interfaces
- Handle database access and migrations
- Manage file storage (documents, templates, exports)
- Integrate with external services (email, AI, payment)
- Provide caching infrastructure
- Handle messaging and events

## What Belongs Here

- Repository implementations
- Database schema definitions
- File storage services
- External service clients
- Cache implementations
- Message queue integration
- Event bus implementations

## What Must NOT Go Here

- No business logic
- No domain entities or rules
- No UI code
- No validation rules
- No configuration (see /config)

## Invariants

- Infrastructure is replaceable without affecting domain
- External service failures are isolated
- Transactions are used where needed
- Connections are properly managed

## Example Concepts (Descriptive)

- **Repository Implementation**: Database access for aggregates.
- **File Storage**: Blob storage for documents and exports.
- **External Client**: Integration with external APIs.
- **Cache**: Performance optimization layer.
- **Event Bus**: System for publishing/consuming events.
- **Migration**: Database schema changes.

## Common Mistakes to Avoid

- **Leaking infrastructure to domain**: Keep layers clean.
- **Synchronous external calls**: Use async where possible.
- **Connection leaks**: Manage resources properly.
- **Hardcoded credentials**: Use secrets management.

## Interactions

- `/infrastructure` implements interfaces from /domain
- `/infrastructure` uses /config for connection settings
- `/infrastructure` stores files for /exports and /rendering
- `/infrastructure` sends events via /notifications
- `/infrastructure` may use /security for encryption
