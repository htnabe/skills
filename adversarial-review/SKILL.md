---
name: adversarial-review
description: "Independent adversarial review skill for implemented features, behavior changes, and bug fixes. Use after implementation to challenge correctness, security, maintainability, readability, test coverage, and regression safety. Reviews the implementation without modifying code and produces actionable findings."
license: MIT
---

# Adversarial Review

Use this skill after implementation to independently challenge correctness, requirements coverage, security, maintainability, readability, test quality, and regression safety. This is a review workflow, not an implementation workflow.

Do not modify source code, tests, configuration, or documentation during review unless the caller explicitly requests review fixes.

## Review Principles

- Treat explicit user requirements as the primary oracle.
- Do not assume correctness because the implementation is small, idiomatic, similar to existing code, or covered by passing tests.
- Look for plausible failure scenarios, not theoretical concerns without meaningful impact.
- Report actionable defects and distinguish them from optional improvements.

Use this priority order when evidence conflicts:

1. Explicit user requirements
2. Acceptance criteria
3. Current implementation and architecture
4. Tests and CI behavior
5. Repository conventions and instructions
6. Existing documentation
7. Historical assumptions

## Workflow

### 1. Understand the Change

Establish the requested and changed behavior, changed files, assumptions, preserved behavior, and affected interfaces or contracts. Read relevant implementation, tests, configuration, documentation, and repository instructions.

### 2. Inspect the Diff and Trace Behavior

Review the complete final diff for unintended modifications, deleted behavior, changed defaults or interfaces, configuration and dependency changes, generated or missing files, and suspicious workarounds. Trace important paths from input through validation and transformation to state changes, failures, side effects, and returned results. Inspect callers and dependencies when relevant.

### 3. Challenge the Implementation

For each applicable review dimension, determine whether behavior is correct, requirements are fully covered, regressions are possible, tests prove observable behavior, security boundaries hold, errors are intentional, and design remains maintainable and readable. Use the detailed [review criteria](references/review-criteria.md). Apply [adversarial techniques](references/review-techniques.md) when the change calls for them.

At minimum, consider correctness, regression safety, test quality, security, error handling, maintainability, readability, and scope. Consider performance, resources, dependencies, and configuration when relevant. Skip categories that do not apply.

### 4. Report Findings

Every substantive finding must include severity, location, problem, impact, concrete scenario, and a remediation direction. Order findings by severity, do not inflate severity, and do not invent findings. Use the [reporting format](references/reporting.md).

Conclude with exactly one status:

- **PASS:** no material defects identified.
- **CHANGES_REQUESTED:** one or more material findings should be addressed.
- **HUMAN_REVIEW_REQUIRED:** unresolved ambiguity, missing information, external dependencies, or requirement conflict prevents reliable review.

## Review Boundaries

The review should inspect implementation, tests, relevant context, and the final diff; challenge assumptions; and report actionable risks independently. It should not implement fixes, refactor unrelated code, expand scope, impose personal style preferences, or approve merely because tests pass.

## Completion Criteria

The review is complete when the requested behavior, relevant paths and tests, final diff, correctness, regression risks, applicable security concerns, maintainability, readability, edge cases, finding severity, and final status have all been considered. The report should be concise enough to act on and detailed enough to reproduce each substantive finding.
