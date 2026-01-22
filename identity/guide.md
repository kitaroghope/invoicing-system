# /identity — User Authentication and Authorization

## Purpose

This folder defines user identity, authentication, and authorization mechanisms. It establishes who is performing actions and what they are allowed to do. It is the gatekeeper for all system access.

## Responsibilities

- Manage user accounts and credentials
- Handle authentication (login, logout, session management)
- Define authorization policies and permission checks
- Manage API keys and tokens
- Handle password reset and recovery
- Support multi-tenancy (user → businesses)

## What Belongs Here

- User entity and aggregate
- Authentication services and handlers
- Session and token management
- Permission and role definitions
- Policy enforcement point
- Security context holders

## What Must NOT Go Here

- No business logic (see /domain)
- No document operations (see /documents)
- No customer data management (see /customers)
- No rendering or exports
- No validation of business rules (see /validation)

## Invariants

- Authentication is required for all protected operations
- Authorization is checked before any state-changing operation
- Users have exactly one owning entity (the account)
- Sessions expire and must be refreshed
- Credentials are never logged or exposed

## Example Concepts (Descriptive)

- **User**: The human or system accessing the application.
- **Principal**: The authenticated identity making a request.
- **Session**: An authenticated user's active connection.
- **Permission**: A discrete access right (read, write, delete).
- **Role**: A grouping of permissions assigned to users.
- **API Key**: Programmatically authenticatable token.
- **Security Context**: Thread-local or request-local identity information.

## Common Mistakes to Avoid

- **Authz without authn**: Never check permissions without verifying identity first.
- **Storing plain passwords**: Always hash and salt credentials.
- **Over-permissioned tokens**: Follow principle of least privilege.
- **Insecure session handling**: Use secure cookies, proper expiration.
- **Bypassing auth**: All endpoints must require authentication.

## Interactions

- `/identity` is consulted by /security for access control
- `/identity` provides principal to /domain for user-scoped operations
- `/identity` uses /infrastructure for user storage
- `/identity` integrates with /config for security settings
- `/identity` may emit security events to /notifications
