# Go Code Changes

Apply these local Effective Go-derived rules to every Go change, alongside repository instructions. Do not fetch the Effective Go page during normal coding work; this reference contains the required guidance. Where repository conventions are stricter, follow the repository convention.

## Read and match the package

- Inspect the affected package and nearby tests before editing.
- Match established package patterns and reuse existing helpers before adding abstractions.
- Keep exported APIs minimal. Export a name only when another package needs it.
- Keep interfaces small and define them where they are consumed, not pre-emptively beside an implementation.
- Prefer concrete types until an interface is necessary.
- Use composition and embedding only when they make the API clearer; do not imitate inheritance.

## Formatting and names

- Run `gofmt` on every changed Go file. Do not hand-format Go code.
- Use short, clear, package-appropriate names. Avoid stuttering, such as `http.HTTPServer` or `user.UserService`.
- Follow Go initialism conventions: `ID`, `URL`, `HTTP`, `API`, `JSON`, and `SQL`.
- Use `MixedCaps`, not underscores, for Go identifiers. Keep package names short, lowercase, and singular where practical.
- Write doc comments for exported declarations when their purpose is not self-evident. Begin the comment with the declaration name.
- Prefer zero-value declarations when an initializer adds no meaning:

  ```go
  var count int
  var items []Item
  ```

## Control flow and functions

- Keep functions focused on one responsibility.
- Prefer early returns to deeply nested conditionals and unnecessary `else` blocks.
- Use `for` for all loops. Prefer `for range` when iterating over a collection and neither index nor mutation requires another form.
- Use `switch` for multi-way decisions; omit a default when a missing case should remain visible.
- Use named result values only when they clarify the function contract. Do not use naked returns in non-trivial functions.
- Avoid `panic` for ordinary errors. Return an error that lets the caller decide how to proceed.
- Never ignore a returned error without an explicit, documented reason.

## Types, methods, and data

- Prefer values unless mutation, identity, avoiding a meaningful copy, or nullable semantics require a pointer.
- Keep methods close to the type they serve. Use a pointer receiver consistently when any method on that type needs one.
- Do not use a pointer to an interface.
- Prefer `make` for slices, maps, and channels; use `new` only when a pointer to a zero value is the clearest result.
- Treat maps as unordered. Do not depend on map iteration order.
- Return a `nil` slice when there are no results unless the API contract requires a distinct empty slice.

## Errors and logging

- Return errors instead of logging them at multiple layers. Log at the boundary that has enough context to make the event actionable.
- Add context while preserving the original error:

  ```go
  return fmt.Errorf("load user %s: %w", id, err)
  ```

- Include `traceID` when available.
- Do not expose secrets, credentials, tokens, or unnecessary personal data in errors or logs.
- Do not start a goroutine without a clear owner, cancellation behavior, and error-handling path.
- Make channel ownership explicit: the sender closes a channel, and receivers handle closure with the two-value receive when needed.
- Prefer synchronization primitives and channels that make communication explicit over shared mutable state.

## Generated code and validation

- Do not guess. When a requirement, convention, or implementation choice is uncertain, ask the user before proceeding.
- Add unit tests for all new or changed behavior. Use table-driven tests when they improve coverage or readability.
- Run affected package tests after each behavioral change.
- Before finishing, run the broadest practical test suite.
- Run the repository's formatter and linter, and resolve errors in the affected scope.
- If the full suite is impractical or a check is blocked, report the exact command, result, and remaining uncertainty.
