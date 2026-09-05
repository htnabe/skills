---
name: feature-implementation
description: "Workflow skill for implementing features, behavior changes, and bug fixes using a test-driven development approach. Use when: implementing a new feature, changing existing behavior, or fixing a bug that requires code changes. Guides repository inspection, requirements analysis, planning, TDD, implementation, refactoring, and validation."
---

# Feature Implementation Skill

## Overview

This skill provides a disciplined workflow for implementing features, behavior changes, and bug fixes using **test-driven development (TDD)**.

The primary goals are:

* Understand the existing repository before modifying code
* Establish clear requirements and acceptance criteria
* Reuse existing architecture and conventions where appropriate
* Implement behavior using a test-first approach
* Keep changes focused and maintainable
* Validate the implementation with appropriate automated checks
* Avoid unrelated refactoring or speculative changes

This skill focuses exclusively on **implementation**.

It does not define:

* Adversarial code review
* Pull request creation
* Release management
* Deployment
* Repository-wide architectural redesign

A higher-level workflow may invoke this skill and perform those activities separately.

---

## Core Principles

### 1. Understand Before Modifying

Inspect the relevant repository structure, implementation, tests, configuration, and documentation before making changes.

Do not assume that a requested feature should be implemented from scratch.

Prefer extending existing abstractions and patterns when they are appropriate for the requested behavior.

### 2. Follow Repository Conventions

Before implementation, inspect relevant repository guidance, such as:

* `AGENTS.md`
* `CLAUDE.md`
* `.github/copilot-instructions.md`
* contributor guidelines
* package/build configuration
* existing test conventions
* project-specific documentation

Repository-specific instructions take precedence over the generic recommendations in this skill.

Do not introduce a new convention when an established repository convention already exists.

### 3. Use TDD for Behavior Changes

For code changes that introduce or modify behavior, follow the TDD cycle:

1. **Red** — write a failing test that expresses the desired behavior
2. **Green** — implement the minimum change necessary to make the test pass
3. **Refactor** — improve the implementation while keeping tests passing

The failing test should demonstrate that the desired behavior is not already implemented.

Do not skip the failing-test step unless TDD is impractical for the specific change. If TDD cannot reasonably be applied, explain why and use the closest practical test-first approach.

### 4. Prefer Minimal Changes

* Modify only what is necessary to satisfy the requirements.
* Avoid unrelated refactoring.
* Avoid speculative improvements.
* Do not change working behavior merely for stylistic reasons.
* Prefer existing dependencies and abstractions when appropriate.
* Introduce new dependencies only when they provide clear value.
* Preserve existing public behavior unless a breaking change is explicitly required.

### 5. Tests Are Part of the Implementation

Tests should express observable behavior rather than implementation details whenever practical.

Prefer tests that:

* Clearly describe expected behavior
* Cover important success cases
* Cover meaningful failure cases
* Protect against regressions
* Remain useful if the internal implementation changes

Do not add tests merely to increase coverage metrics.

---

# Workflow

## 1. Analyze the Request

Identify:

* Requested behavior
* Expected outcome
* User-visible behavior
* Inputs and outputs
* Constraints
* Potential breaking changes
* Existing behavior that may be affected

Do not ask questions that can be answered by inspecting the repository.

Ask focused clarification questions only when the desired behavior cannot be determined reliably from the request and repository context.

### Acceptance Criteria

Establish concrete acceptance criteria before implementation.

For example:

```text
Acceptance Criteria:
- Valid input produces the expected result
- Invalid input is rejected appropriately
- Existing behavior remains unchanged
- The new behavior is covered by automated tests
```

Acceptance criteria should be specific enough to determine whether the implementation is complete.

---

## 2. Inspect the Repository

Inspect only the repository areas relevant to the requested change.

Typical sources include:

* Existing implementation
* Existing tests
* Package/build configuration
* CLI definitions
* API definitions
* Configuration files
* Database schemas or migrations
* CI workflows
* Documentation
* Repository instructions
* Existing abstractions and utilities

Determine:

1. Where the change belongs
2. Which existing components should be reused
3. Which tests cover related behavior
4. Which conventions apply
5. Which validation commands are relevant
6. Whether compatibility or migration concerns exist

Do not modify files during repository inspection unless explicitly necessary.

---

## 3. Create an Implementation Plan

Before writing code, create a concise implementation plan.

Use a structure similar to:

```text
# Implementation Plan

## Behavior
- [Expected behavior]

## Tests
- [Test case]
- [Test case]
- [Edge case]

## Implementation
- [Implementation task]
- [Implementation task]

## Validation
- [Relevant test command]
- [Relevant typecheck/build/lint command]

## Risks
- [Compatibility/security/performance/etc.]
```

Break the work into small, independently verifiable steps.

Do not prescribe exact file locations until repository inspection establishes the appropriate location.

Avoid creating a detailed plan for work that is not necessary to satisfy the request.

---

## 4. Resolve Ambiguity

Before modifying code, resolve ambiguities that could materially change the implementation.

Ask the user when:

* Multiple reasonable behaviors exist
* The change could break existing consumers
* The requested behavior conflicts with existing requirements
* A destructive migration is required
* Security-sensitive behavior cannot be determined
* The repository does not provide enough information to determine the intended behavior

Do not ask for confirmation of routine implementation details that can be determined objectively from the repository.

---

# TDD Implementation Cycle

## 5. Red — Write a Failing Test

For each meaningful behavior:

1. Identify the smallest useful behavior to test.
2. Add or modify the corresponding test.
3. Run the relevant test.
4. Confirm that it fails for the expected reason.

The failure should demonstrate that the desired behavior is not yet implemented.

A test that fails because of a syntax error, incorrect test setup, missing dependency, or unrelated environment problem does not constitute a meaningful Red phase.

If the test unexpectedly passes, investigate why before implementing the feature.

---

## 6. Green — Implement the Minimum Change

Implement the smallest change necessary to satisfy the failing test.

At this stage:

* Avoid premature abstractions.
* Avoid unrelated refactoring.
* Avoid speculative edge-case handling that is not required by the acceptance criteria.
* Prefer simple implementations that clearly express the intended behavior.

Run the relevant test after implementation.

Confirm that:

* The new test passes.
* Existing relevant tests continue to pass.

---

## 7. Refactor

After the tests are green, improve the implementation without changing its behavior.

Consider:

* Naming
* Control flow
* Duplication
* Function and module responsibilities
* Error handling
* Abstraction boundaries
* Existing repository conventions
* Readability

Do not refactor merely because another implementation style is possible.

Run the relevant tests again after refactoring.

---

## 8. Repeat the TDD Cycle

Repeat:

```text
Red
 ↓
Green
 ↓
Refactor
```

until the acceptance criteria are satisfied.

Prefer multiple small TDD cycles over one large test and implementation cycle when the feature contains several independent behaviors.

---

# Implementation Quality

## 9. Preserve Existing Behavior

When modifying existing functionality:

* Identify behavior that must remain unchanged.
* Add regression tests for behavior that could be affected.
* Avoid changing public APIs unless required.
* Preserve backward compatibility where the repository expects it.

If a breaking change is required, make it explicit in the implementation plan and tests.

---

## 10. Handle Errors and Edge Cases

Consider meaningful failure modes relevant to the feature.

Examples include:

* Invalid input
* Missing required values
* Empty input
* Boundary values
* Duplicate values
* Unexpected external responses
* File or network failures
* Permission failures
* Partial failures
* Invalid configuration

Do not add speculative handling for unrealistic scenarios merely to increase code complexity.

Prioritize edge cases based on the actual behavior, trust boundaries, and domain of the feature.

---

## 11. Consider Security

For changes involving user input, external data, authentication, authorization, filesystem access, network communication, secrets, or other trust boundaries:

* Validate inputs appropriately.
* Preserve existing security boundaries.
* Avoid exposing sensitive information.
* Avoid unsafe parsing or execution.
* Follow existing security mechanisms.
* Do not introduce insecure defaults.

Do not invent security mechanisms that conflict with established project architecture.

Security-specific adversarial review, if required, should be handled by a dedicated review workflow.

---

# Validation

## 12. Run Targeted Tests

After implementation:

1. Run the tests directly related to the change.
2. Confirm they pass.
3. Run relevant regression tests.

Prefer targeted tests during development to shorten the feedback loop.

---

## 13. Run Broader Validation

After targeted tests pass, run repository validation relevant to the changed areas.

Depending on the project, this may include:

```text
- Unit tests
- Integration tests
- E2E tests
- Type checking
- Linting
- Build
- Packaging checks
- Documentation checks
```

Use the repository's documented commands when available.

Do not run unrelated expensive checks merely because they exist.

---

## 14. Inspect the Final Diff

Before considering the implementation complete:

1. Review `git diff`
2. Review `git status`
3. Confirm only intended files changed
4. Remove accidental debug code
5. Remove temporary files
6. Confirm tests are included where appropriate
7. Confirm documentation is updated when user-facing behavior changed
8. Confirm no unrelated refactoring was introduced

If unexpected changes are found, investigate and remove them unless they are required by the task.

---

# Handling Existing Tests

When existing tests fail during implementation:

### If the failure is caused by the implementation

Fix the implementation.

### If the failure reveals an incorrect test assumption

Update the test only when the intended behavior has been established by the requirements or repository behavior.

### If the failure is unrelated

Do not modify unrelated code merely to make the current task pass.

Report the unrelated failure separately.

Never weaken or remove a valid regression test simply to make the implementation pass.

---

# Handling Incomplete or Conflicting Requirements

If requirements remain ambiguous after repository inspection:

1. Identify the specific ambiguity.
2. Explain the implementation choices it affects.
3. Ask the smallest number of questions necessary.
4. Do not make irreversible assumptions.

If requirements conflict with existing repository behavior:

1. Identify the conflict.
2. Prefer explicit user requirements when they clearly define the intended new behavior.
3. Determine whether existing behavior needs a migration or compatibility strategy.
4. Add appropriate tests for the intended behavior.

---

# Completion Criteria

The implementation workflow is complete when all applicable conditions are satisfied:

* Acceptance criteria are satisfied.
* Appropriate tests have been added or updated.
* TDD was followed, or the reason for deviation is documented.
* Relevant tests pass.
* Relevant type checking, linting, and build checks pass when applicable.
* Existing behavior is preserved unless a change was explicitly requested.
* The final diff contains only intended changes.
* Required documentation has been updated.
* No known implementation issue remains within the scope of the task.

Do not claim completion when known validation failures remain unexplained.

---

# Completion Report

Report the completed implementation concisely.

Use a structure similar to:

```text
Implementation Complete

Changes:
- [Major implementation change]
- [Major implementation change]

Tests:
- [Tests added/updated]
- [Test results]

Validation:
- [Typecheck/build/lint/etc.]

TDD:
- Red → Green → Refactor completed

Notes:
- [Important implementation or compatibility note]
```

If unrelated pre-existing failures were encountered, mention them explicitly.

---

# Out of Scope

This skill does not define:

* Adversarial code review
* Multi-agent review orchestration
* Pull request creation
* Release management
* Deployment
* Dependency update policy
* Broad architectural redesign
* Repository-wide documentation maintenance

Use a more specific workflow when one exists.

---

# When This Skill Does NOT Apply

Do not use this skill as the primary workflow for:

* Purely informational questions
* Code explanations with no requested changes
* Pure documentation maintenance with no implementation change
* PR-only review requests
* Release or deployment tasks
* Broad architectural research without an implementation request
* Changes that have a dedicated repository-specific workflow

Use the most specific applicable workflow available.
