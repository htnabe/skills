# TDD and Quality Details

Read this reference when the implementation needs a detailed test-first checklist or quality review.

## TDD Cycle

### Red

For each meaningful behavior:

1. Identify the smallest useful behavior to test.
2. Add or modify the corresponding test.
3. Run the relevant test.
4. Confirm it fails for the expected reason.

A syntax error, broken setup, missing dependency, or unrelated environment problem is not a meaningful Red phase. If the test passes unexpectedly, investigate before implementing.

### Green

Implement the smallest change that satisfies the failing test. Avoid premature abstractions, unrelated refactoring, speculative edge-case handling, and unnecessary complexity. Confirm the new and relevant existing tests pass.

### Refactor

After the tests are green, improve naming, control flow, duplication, responsibilities, error handling, abstraction boundaries, and readability without changing behavior. Rerun relevant tests after refactoring.

Prefer multiple small cycles when behavior has independent parts.

## Implementation Quality

Preserve behavior that is not being changed, public APIs, and expected backward compatibility. Add regression tests for behavior that could be affected. Make intentional breaking changes explicit in the plan and tests.

Consider realistic failure modes such as invalid or missing input, empty or boundary values, duplicates, unexpected external responses, file or network failures, permission errors, partial failures, and invalid configuration. Do not add speculative handling merely to increase complexity.

For changes involving user input, external data, authentication, authorization, filesystems, networks, secrets, or other trust boundaries:

- Validate inputs appropriately.
- Preserve existing security boundaries.
- Avoid sensitive-data exposure, unsafe parsing, and unsafe execution.
- Follow established security mechanisms and defaults.

Security-specific adversarial review belongs to the dedicated review workflow.

## Existing Test Failures

- Fix failures caused by the implementation.
- Update a test only when requirements or established repository behavior show its assumption is wrong.
- Do not change unrelated code to hide unrelated failures.
- Never weaken or remove a valid regression test merely to make the implementation pass.

## Requirements Conflicts

If requirements remain ambiguous, identify the ambiguity, explain the affected choices, ask the smallest necessary question, and avoid irreversible assumptions. If requirements conflict with existing behavior, prefer explicit requirements, determine whether migration or compatibility handling is needed, and test the intended behavior.
