# /validation — Input Validation

## Purpose

This folder defines validation rules for external input before it reaches the domain layer. Validation ensures data conforms to structural and format requirements. It is the boundary guard between the outside world and the domain.

## Responsibilities

- Validate input format and structure
- Validate business-scoped constraints (unique names, valid references)
- Validate document structure before domain operations
- Provide validation error messages
- Support custom validation rules
- Validate AI output before use

## What Belongs Here

- Validator implementations
- Validation rule definitions
- Error message formatting
- Constraint specifications
- Custom validation logic
- AI output validators

## What Must NOT Go Here

- No business rule enforcement (see /domain)
- No authentication or authorization (see /identity)
- No data transformation or normalization
- No persistence of validated data
- No rendering or output generation

## Invariants

- All external input is validated before domain operations
- Validation failures prevent state changes
- Validation errors are specific and actionable
- Validated data still passes domain invariants

## Example Concepts (Descriptive)

- **Structural Validator**: Checks required fields and types.
- **Business Validator**: Checks business rules (unique, references).
- **Validation Error**: Specific error with field and message.
- **Validation Rule**: Definition of valid input.
- **AI Output Validator**: Validates AI suggestions before use.

## Common Mistakes to Avoid

- **Duplicating domain logic**: Validation ≠ business rules.
- **Silent failures**: Fail loudly on invalid input.
- **Inconsistent validation**: Same input, same result everywhere.
- **Leaking internals**: Don't expose internal structure in errors.
- **Over-validating**: Don't validate what the domain validates.

## Interactions

- `/validation` guards all input to /domain
- `/validation` is called by /editor before domain operations
- `/validation` validates AI output from /ai
- `/validation` uses /config for validation settings
- `/validation` may use /financials for numeric validation
