# Global Code Standards

The project should follow consistent coding practices across all components.

### General Conventions

- Use clear and descriptive names for files, variables, functions, classes, and database fields.
- Keep functions and modules focused on one responsibility.
- Avoid duplicating logic when it can be reused safely.
- Write comments only when they explain important decisions or complex logic.
- Keep secrets, passwords, API keys, and private credentials out of the source code.
- Store configuration values in environment variables or secure configuration files.
- Format code consistently before committing changes.
- Remove unused imports, variables, and debugging statements.
- Update the relevant documentation when a feature or workflow changes.

### Naming Conventions

Use names that describe the purpose of the item:

- `snake_case` for Python files, variables, and functions
- `PascalCase` for classes and components where applicable
- `UPPER_SNAKE_CASE` for constants
- Descriptive names for API endpoints, database tables, and user roles

## Testing Conventions

Tests should be added or updated whenever a feature, bug fix, or important configuration change is introduced.

### Test Organization

Keep tests organized according to the part of the system they cover:

- Unit tests for individual functions or classes
- Integration tests for interactions between services or modules
- API tests for endpoints and request responses
- End-to-end tests for complete user workflows

Test files should use clear names that identify the functionality being tested.

### Test Naming

Test names should describe the expected behaviour. For example:

```text
test_member_registration_with_valid_details
test_permit_request_requires_authentication
test_invalid_payment_callback_is_rejected