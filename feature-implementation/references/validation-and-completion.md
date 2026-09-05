# Validation and Completion

Read this reference when selecting repository checks or preparing the completion report.

## Validation Order

1. Run tests directly related to the change.
2. Run relevant regression tests.
3. Run repository checks relevant to the changed area, such as unit, integration, or E2E tests, type checking, linting, builds, packaging checks, and documentation checks.
4. Use documented repository commands when available; do not run unrelated expensive checks merely because they exist.

## Final Diff Checklist

Before completion:

- Review `git diff` and `git status`.
- Confirm only intended files changed.
- Remove debug code and temporary files.
- Confirm tests are included where appropriate.
- Confirm documentation is updated when user-facing behavior changed.
- Confirm no unrelated refactoring was introduced.

## Completion Criteria

The workflow is complete only when:

- Acceptance criteria are satisfied.
- Appropriate tests are added or updated.
- TDD was followed, or its deviation is documented.
- Relevant tests and applicable type checking, linting, and build checks pass.
- Existing behavior is preserved unless a change was explicitly requested.
- The final diff contains only intended changes.
- Required documentation is updated.
- No known in-scope issue remains.

Do not claim completion while known validation failures remain unexplained.

## Completion Report

Use a concise report with these sections:

```text
Implementation Complete

Changes:
- [Major implementation change]

Tests:
- [Tests added or updated]
- [Test results]

Validation:
- [Typecheck, build, lint, or other checks]

TDD:
- Red -> Green -> Refactor completed, or explain the deviation

Notes:
- [Important implementation or compatibility note]
```

Mention unrelated pre-existing failures explicitly.
