# /notifications — Notification System (v1 Placeholder)

## Purpose

This folder defines the notification system for alerting users and customers. This is a placeholder for v1—all notification infrastructure is out of scope but the architectural boundaries are defined.

## Responsibilities

- Define notification types (email, SMS, in-app)
- Define notification templates
- Manage notification delivery
- Handle notification preferences
- Track notification status

## What Belongs Here

- Notification type definitions
- Notification template references
- Delivery status tracking
- Preference management
- Notification event handlers

## What Must NOT Go Here

- No email/SMS provider integration (external)
- No actual delivery implementation
- No template content (see /templates)
- No document rendering (see /rendering)

## Invariants

- Notifications are best-effort, not guaranteed
- Notification preferences are respected
- Sensitive data is not logged

## Example Concepts (Descriptive)

- **Email Notification**: Email delivery.
- **SMS Notification**: Text message delivery.
- **In-App Notification**: System alerts.
- **Notification Template**: Message structure.
- **Delivery Status**: Sent, delivered, failed.

## Common Mistakes to Avoid

- **Blocking on delivery**: Notifications should be async.
- **Leaking sensitive data**: Scrub sensitive content.
- **Over-notification**: Respect user preferences.

## Interactions

- `/notifications` receives events from /domain
- `/notifications` uses /templates for content
- `/notifications` integrates with /infrastructure for delivery
- `/notifications` uses /config for settings
- `/notifications` may use /customers for contact info
