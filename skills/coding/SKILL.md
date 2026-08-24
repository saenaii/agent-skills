---
name: coding
description: Apply repository, language when implementing code changes. Automatically detects language and loads appropriate reference guidance from /reference/<language>/<language>.md. Use at the start of hands-on coding work, including features, fixes, and refactors. Do not use for specifications or other documentation-only work.
---

# Coding

Write code for human readers. Optimize for readability and maintainability while making the smallest change that satisfies the request.

## Workflow

1. Understand the requested change.
   - Read the repository instructions, relevant implementation, and nearby tests before editing.
   - Identify every language and file type the change affects.

2. Load the applicable language guidance.
   - Detect language from file extension (.go, .tf, .json, .yaml, .yml) or repository configuration
   - Load language guidance from /reference/<language>/<language>.md if it exists
   - Also check /reference/<language>/self_valid.md if it exists for self-validation under Generated code and validation
   - For Terraform, JSON, or YAML changes without dedicated reference files, follow the repository's instructions and established conventions

3. Implement the smallest complete change that satisfies the request, repository instructions, language guidance.

4. Add or update tests for every new or changed behavior. For configuration-only changes, run the repository's applicable validation and test commands.

5. Validate the result before finishing.

## Coding Requirements

- Give each new or modified function one clear responsibility.
- Keep cyclomatic complexity at or below 15.
- Prefer early returns over unnecessary `else` blocks.
- Match the repository's existing style and patterns.
- Add unit-test coverage for all new executable code and changed behavior.
- naming is important, use the consistent name for the function, var, etc, keep it same as the name
- don't change other irrelevant code, don't format or change the code style for irrelevant code

## Validation

Before reporting completion:

1. Run the affected unit tests and confirm they pass.
2. Run the broadest practical test suite for the change.
3. Run the repository's configured formatter and linter; confirm there are no lint errors in the affected scope.
4. If any required check cannot run, report the exact command, failure, and remaining uncertainty. Do not claim the check passed.

In the final response, summarize the changed behavior and list the validation commands and results.
