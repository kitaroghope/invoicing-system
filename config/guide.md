# /config — Configuration Management

## Purpose

This folder defines configuration: application settings, feature flags, environment variables, and user preferences. It is the single source of truth for all tunable values.

## Responsibilities

- Define configuration schemas
- Load configuration from sources (env, files, database)
- Validate configuration
- Provide configuration to other layers
- Handle feature flags
- Manage user preferences

## What Belongs Here

- Configuration schemas
- Configuration loaders
- Feature flags
- Default values
- Configuration validators
- Environment-specific settings

## What Must NOT Go Here

- No business rules
- No secrets (should be in secrets management)
- No runtime state (use infrastructure)
- No code behavior changes without configuration

## Invariants

- Configuration is read-only at runtime
- Configuration changes require restart or reload
- Invalid configuration prevents startup
- Secrets are never in configuration files

## Example Concepts (Descriptive)

- **App Config**: Core application settings.
- **Feature Flag**: Toggle features on/off.
- **User Preference**: User-specific settings.
- **Environment Config**: Environment-specific values.
- **Configuration Schema**: Structure definition.
- **Configuration Validator**: Validates completeness.

## Common Mistakes to Avoid

- **Hardcoding values**: Everything configurable.
- **Secrets in config**: Use secrets management.
- **Runtime config changes**: Require explicit reload.
- **Invalid defaults**: Validate all configuration.

## Interactions

- `/config` provides settings to all layers
- `/config` uses /infrastructure for persistence
- `/config` may integrate with /security for secrets
- `/config` is read at startup by all components
