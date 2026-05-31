# Utility Library Standards: Zod & Validation

This document defines the standards for data validation and utility library usage within the Project.

## Core Stack
- **Validation**: Zod (Latest)
- **Form Integration**: React Hook Form with Zod-Resolver (Preferred)

## Implementation Rules (Zod)

### 1. Input Types
- **String First**: **STRICT RULE**: All input fields in a Zod schema must be defined as `z.string()` by default for form inputs.
- **Boolean Exception**: Fields for checkboxes/toggles should use `z.boolean()`.
- **No Coercion**: **STRICT RULE**: Do not use Zod's coercion features. Transformations must be explicit.

### 2. Composition Constraints
- **No Unions**: **STRICT RULE**: Avoid using `z.union` or `.or()` where possible. Prefer flat schemas or optional fields to maintain simplicity.
- **Explicit Requirement**: Every field should be explicitly defined.

### 3. Error Handling
- **User-Friendly Messages**: Provide clear error messages for validation constraints.
- **Visual Feedback**: Integration with form libraries should show errors clearly in the UI.

### 4. Reusability
- **Shared Schemas**: Extract common validation patterns (e.g., Email validation, Password complexity) into shared schema constants.

By adhering to these standards, we ensure that our data validation logic remains robust and consistent across the Project.
