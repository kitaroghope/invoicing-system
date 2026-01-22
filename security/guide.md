# /security — Security Concerns

## Purpose

This folder defines security infrastructure: encryption, audit logging, access control enforcement, and security policies. It protects the system from unauthorized access and provides accountability.

## Responsibilities

- Define encryption at rest and in transit
- Implement audit logging for all significant actions
- Enforce access control policies
- Handle security headers and hardening
- Manage secrets and sensitive data
- Support security incident response

## What Belongs Here

- Encryption implementations
- Audit logging infrastructure
- Security policy definitions
- Access control enforcement
- Secrets management
- Security middleware

## What Must NOT Go Here

- No authentication logic (see /identity)
- No business rule enforcement
- No document rendering or processing
- No user interface code
- No configuration management (see /config)

## Invariants

- All sensitive data is encrypted at rest
- Audit logs are immutable and append-only
- Access decisions are deny-by-default
- Secrets never appear in logs or error messages
- Security events are logged before processing

## Example Concepts (Descriptive)

- **Audit Log**: Immutable record of who did what when.
- **Encryption Key**: Key used for data encryption.
- **Access Policy**: Rules governing resource access.
- **Security Event**: Notable security-relative occurrence.
- **Secrets Vault**: Secure storage for credentials.
- **Rate Limiter**: Controls request frequency.

## Common Mistakes to Avoid

- **Logging secrets**: Never log passwords, keys, or tokens.
- **Weak encryption**: Use standard, reviewed algorithms.
- **Disabled audit**: Always log, even in development.
- **Overly permissive**: Default to deny access.
- **Ignoring security headers**: Web responses need security headers.

## Interactions

- `/security` provides encryption to /infrastructure
- `/security` audits all /identity actions
- `/security` enforces policies on /domain operations
- `/security` integrates with /config for policy settings
- `/security` may emit events to /notifications
