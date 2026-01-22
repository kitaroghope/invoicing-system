# /ai — AI Assistance Layer

## Purpose

This folder contains AI assistance features that provide suggestions, predictions, and automation during document creation. AI is an advisory layer—it suggests but never decides. All AI output must be validated before use.

## Responsibilities

- Provide AI-powered suggestions (line items, descriptions, pricing)
- Generate document previews or drafts from natural language
- Analyze existing documents for anomalies or improvements
- Classify and tag documents
- Assist with customer communication

## What Belongs Here

- AI service interfaces
- Prompt engineering and templates
- Response parsing and validation
- Suggestion caching and ranking
- AI configuration (model selection, temperature, etc.)

## What Must NOT Go Here

- No AI-generated content that bypasses validation
- No AI modification of issued documents
- No AI access to internal system state beyond document context
- No AI that overrides business rules
- No persistent AI decision-making

## Invariants

- AI suggestions are always explicitly accepted or rejected by the user
- AI output is validated against domain rules before use
- AI never issues documents automatically
- AI context is limited to the current document being edited
- AI is optional and can be disabled entirely

## Example Concepts (Descriptive)

- **Line Item Suggester**: Suggests common line items based on customer history.
- **Description Generator**: Generates item descriptions from brief notes.
- **Pricing Advisor**: Suggests prices based on market data (external).
- **Anomaly Detector**: Flags unusual amounts or quantities.
- **Natural Language Parser**: Converts "50 widgets at $10 each" to line items.
- **Communication Assistant**: Drafts customer email from document context.

## Common Mistakes to Avoid

- **Unvalidated AI output**: Never use AI output directly without validation.
- **AI as authority**: AI is assistive, never authoritative.
- **Leaking context**: Don't expose unrelated customer data to AI.
- **Non-deterministic behavior**: AI suggestions should be reproducible with same input.
- **AI as replacement for business logic**: Don't use AI to implement rules.

## Interactions

- `/ai` receives document context from /editor
- `/ai` suggestions are validated by /validation
- `/ai` may call external AI services via /infrastructure
- `/ai` operates on draft documents only; never on issued documents
- `/ai` configuration lives in /config
