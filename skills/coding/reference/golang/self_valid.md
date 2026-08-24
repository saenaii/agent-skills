# Self Validation for Go

When implementing Go changes, perform the following self-validation checks before considering the work complete:

## 1. Table-Driven Tests

- Check if the test code follows table-driven test pattern.
- If not, rewrite the test to use table-driven tests. Table-driven tests improve coverage, readability, and maintainability by separating test data from test logic.

## 2. interface{} vs Concrete Types/Interfaces

- Check if the code uses `any` (or `interface{}`) instead of proper interfaces.
- If the code uses `any`/`interface{}` without a valid reason, correct it to use specific interfaces or concrete types as appropriate.

## 3. Unrelated Code Changes

- Check if the change inadvertently formatted unrelated files or added/removed blank lines in unrelated files.
- If yes, revert any irrelevant code style changes (formatting, blank lines) to keep the change minimal and focused.

## Self-Check: Update Loop Limit

- The self-validation update loop must not exceed 3 times. If changes are still needed after 3 iterations, stop and report the remaining issues.