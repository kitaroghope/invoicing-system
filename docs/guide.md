# /docs — Documentation

## Purpose

This folder contains all project documentation: architecture decisions, API documentation, guides, and developer resources. It is the authoritative source for "how" and "why" the system works.

## Responsibilities

- Store architecture decision records (ADRs)
- Maintain API documentation
- Provide developer guides
- Store user documentation
- Maintain style guides and conventions
- Store contributing guidelines

## What Belongs Here

- Architecture decision records
- API documentation
- Developer guides
- User documentation
- Style guides
- Contributing guidelines
- Changelog and release notes

## What Must NOT Go Here

- No implementation code
- No configuration files
- No templates or assets (see relevant folders)
- No build artifacts
- No generated documentation (may include in some cases)

## Invariants

- Documentation is version-controlled with code
- Documentation reflects current system state
- Documentation is reviewed with code changes
- Outdated documentation is updated or removed

## Example Concepts (Descriptive)

- **ADR**: Architecture Decision Record.
- **API Doc**: API endpoint documentation.
- **Dev Guide**: Developer getting started.
- **User Guide**: End-user documentation.
- **Style Guide**: Code and documentation style.
- **Contributing**: Guidelines for contributors.
- **Changelog**: Version history.

## Common Mistakes to Avoid

- **Outdated documentation**: Keep docs synchronized.
- **Documentation drift**: Docs should match implementation.
- **Missing ADRs**: Record decisions with context.
- **Duplicate documentation**: Single source of truth.

## Interactions

- `/docs` references all other folders
- `/docs` is generated from code in some cases
- `/docs` uses /config for documentation config
- `/docs` may reference /infrastructure for deployment
