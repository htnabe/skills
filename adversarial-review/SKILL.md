---
name: adversarial-review
description: "Independent adversarial review skill for implemented features, behavior changes, and bug fixes. Use after implementation to challenge correctness, security, maintainability, readability, test coverage, and regression safety. Reviews the implementation without modifying code and produces actionable findings."
license: MIT
---

# Adversarial Review

## Overview

This skill performs an **independent adversarial review** of an implementation.

The purpose is not to confirm that the implementation looks reasonable. The purpose is to actively search for:

* incorrect behavior
* missed requirements
* regressions
* insufficient test coverage
* security vulnerabilities
* maintainability problems
* readability problems
* unnecessary complexity
* edge cases
* failure handling problems
* inconsistencies with the repository's conventions

Assume that the implementation may contain defects even when the tests pass.

This skill is a **review skill**, not an implementation skill.

Do not modify source code, tests, configuration, or documentation while performing the review unless the caller explicitly requests a review with fixes.

---

# Core Principles

## 1. Review Independently

Do not assume the implementation is correct because:

* the implementer believes it is correct
* tests pass
* the implementation is small
* the code looks idiomatic
* similar code already exists
* the requested behavior appears straightforward

Evaluate the implementation against the requirements and repository context independently.

---

## 2. Try to Break the Implementation

Think adversarially.

Ask:

> "What input, state, environment, sequence of operations, or future change would cause this implementation to fail?"

Look beyond the happy path.

Consider:

* empty values
* nullish values
* malformed input
* unexpected types
* boundary values
* duplicate values
* large inputs
* missing configuration
* invalid configuration
* concurrent operations
* repeated operations
* partial failures
* external service failures
* unusual execution environments
* existing data
* backwards compatibility

The exact categories depend on the implementation being reviewed.

---

## 3. Requirements Are the Primary Oracle

Review against the actual requirements, not merely against the implementation's apparent intent.

Use this priority order:

1. Explicit user requirements
2. Acceptance criteria
3. Current implementation and architecture
4. Tests and CI behavior
5. Repository conventions and instructions
6. Existing documentation
7. Historical assumptions

If the implementation satisfies the code's existing behavior but violates an explicit requirement, report it.

---

## 4. Passing Tests Are Evidence, Not Proof

A passing test suite does not establish correctness.

Review whether the tests actually prove the important behavior.

Look for:

* missing scenarios
* tests that only verify implementation details
* assertions that are too weak
* tests that cannot fail when the implementation is broken
* missing boundary cases
* missing error cases
* missing regression tests
* mocked behavior that hides real failures

When appropriate, mentally construct a failing case that the current tests would not detect.

---

# Review Workflow

## 1. Understand the Change

Before reviewing individual lines, establish:

* What behavior was requested?
* What behavior changed?
* Which files changed?
* What assumptions does the implementation make?
* What existing behavior must remain unchanged?
* What interfaces or contracts are affected?

Read the relevant implementation, tests, configuration, and repository instructions before reaching conclusions.

---

## 2. Inspect the Final Diff

Review the complete diff rather than only newly added code.

Look for:

* unintended modifications
* unrelated changes
* deleted behavior
* changed defaults
* changed public interfaces
* changed error behavior
* configuration changes
* dependency changes
* generated files
* missing files
* suspicious workarounds

Pay particular attention to changes that appear unrelated to the requested behavior.

---

## 3. Trace the Behavior

Follow the implementation from input to output.

For each important path, determine:

1. What enters the system?
2. How is it validated?
3. How is it transformed?
4. Where is state changed?
5. What can fail?
6. How are failures handled?
7. What is returned or exposed to the caller?
8. What happens on subsequent calls?

Do not stop at the function where the feature was implemented. Trace relevant callers, dependencies, and side effects.

---

# Review Dimensions

Review each dimension that is relevant to the change.

## 4. Correctness

Determine whether the implementation actually produces the required behavior.

Check:

* normal cases
* boundary conditions
* invalid inputs
* state transitions
* return values
* side effects
* ordering assumptions
* asynchronous behavior
* error behavior
* compatibility with existing behavior

A passing test does not override evidence that the implementation is logically incorrect.

---

## 5. Requirements Coverage

Map important requirements to implementation and tests.

For each meaningful requirement, ask:

* Is it implemented?
* Is it tested?
* Can the test actually detect a regression?
* Is any requirement only partially implemented?

Report requirements that are missing or ambiguously implemented.

---

## 6. Regression Safety

Check whether existing functionality could have been unintentionally changed.

Pay attention to:

* public APIs
* CLI behavior
* configuration formats
* file formats
* database schemas
* network requests
* error codes
* exported functions
* environment variables
* default behavior

Consider both direct and indirect regressions.

---

## 7. Test Quality

Evaluate tests as tests, not merely by their existence.

Check whether tests:

* express observable behavior
* cover important branches
* cover failure paths
* cover edge cases
* verify meaningful results
* prevent the reported bug from returning
* avoid excessive implementation-detail coupling

Prefer a smaller number of strong tests over many superficial tests.

When the implementation was expected to follow TDD, also consider whether the tests reasonably represent the behavior that should have driven the implementation.

---

## 8. Security

Look for security weaknesses relevant to the implementation.

Consider, where applicable:

* injection
* command execution
* path traversal
* unsafe file operations
* authentication and authorization
* secret exposure
* sensitive data leakage
* insecure defaults
* unsafe deserialization
* dependency risks
* insufficient input validation
* excessive permissions
* denial-of-service risks
* untrusted external input
* logging of sensitive information

Do not report theoretical security concerns without a plausible attack path or meaningful risk.

For each security finding, explain:

* attack or failure scenario
* affected behavior
* impact
* recommended direction for remediation

---

## 9. Maintainability

Look for problems that make future changes unnecessarily difficult.

Consider:

* excessive coupling
* duplicated logic
* unclear abstractions
* inappropriate responsibilities
* hidden dependencies
* unnecessary state
* brittle assumptions
* over-engineering
* difficult-to-test design
* configuration scattered across unrelated locations

Do not recommend refactoring merely because another design is aesthetically preferable.

Report maintainability issues when they create meaningful engineering cost or increase defect risk.

---

## 10. Human Readability

Review whether another developer can understand the implementation without reconstructing hidden assumptions.

Look for:

* misleading names
* unclear control flow
* overly clever code
* excessive nesting
* implicit behavior
* unexplained constants
* confusing abstractions
* misleading comments
* comments that contradict the code

Prefer straightforward code over clever code when both provide equivalent behavior.

---

## 11. Error Handling and Failure Modes

Check whether failures are handled intentionally.

Consider:

* expected errors
* unexpected errors
* partial failures
* cleanup after failure
* retry behavior
* user-facing error messages
* error propagation
* swallowed errors
* incorrect success reporting
* inconsistent failure behavior

An implementation should not silently convert meaningful failures into apparent success.

---

## 12. Performance and Resource Usage

Evaluate performance only where it is relevant.

Look for:

* unnecessary repeated work
* unbounded memory usage
* accidental quadratic behavior
* excessive network requests
* unnecessary filesystem operations
* expensive work inside loops
* resource leaks
* missing cleanup

Do not optimize hypothetical micro-benchmarks when there is no meaningful performance concern.

---

## 13. Dependency and Configuration Changes

If dependencies or configuration changed, verify:

* the dependency is actually necessary
* versions are appropriate
* existing dependencies could already provide the behavior
* configuration defaults are safe
* environment variables are handled correctly
* development and production behavior remain consistent
* CI and local environments remain compatible

Treat changes to package metadata and build configuration as part of the implementation, not as incidental details.

---

# Adversarial Techniques

Use techniques appropriate to the implementation.

## Boundary Analysis

Test mentally at:

* minimum values
* maximum values
* zero
* empty values
* one-item collections
* very large collections
* just-inside boundaries
* just-outside boundaries

---

## Negative Testing

Ask:

> "What happens when the input is invalid?"

Consider malformed, incomplete, unexpected, duplicated, or contradictory input.

---

## State Transition Analysis

For stateful behavior, inspect transitions such as:

* initial → active
* active → active
* active → completed
* active → failed
* failed → retry
* completed → repeated invocation

Look for states the implementation assumes cannot occur.

---

## Failure Injection

Mentally or through existing tests, consider failures from:

* network calls
* filesystem operations
* parsing
* validation
* external APIs
* dependencies
* configuration
* user input

Determine whether the resulting behavior is safe and understandable.

---

## Compatibility Analysis

Ask:

> "What existing consumer could break because of this change?"

Inspect callers, exported APIs, CLI interfaces, configuration, and data formats when applicable.

---

## Test-Evasion Analysis

Ask:

> "Could I make the implementation wrong while keeping all existing tests green?"

If yes, identify the missing assertion or scenario.

---

# Finding Classification

Classify findings by severity.

### Critical

A defect that can cause severe security impact, data loss, major system failure, or makes the requested behavior fundamentally unusable.

### High

A significant correctness, security, compatibility, or reliability problem that should be fixed before the change is accepted.

### Medium

A meaningful defect, maintainability problem, test gap, or edge-case failure that should normally be addressed before or shortly after acceptance.

### Low

A minor issue with limited practical impact, such as a small readability problem or non-critical test improvement.

### Informational

An observation or optional improvement that does not represent a defect.

Do not inflate severity.

---

# Reporting Findings

Every substantive finding should contain:

1. **Severity**
2. **Location**
3. **Problem**
4. **Why it matters**
5. **Concrete scenario**
6. **Recommended direction**

Example structure:

```text
[High] Missing validation for externally supplied path

Location:
src/loader.ts:42

Problem:
The implementation passes an externally supplied path directly to the filesystem operation.

Why it matters:
A caller can potentially access files outside the intended directory.

Scenario:
A path containing parent-directory traversal is supplied.

Recommendation:
Validate and constrain the resolved path against the intended base directory.
```

Avoid vague findings such as:

> "This could be more secure."

Explain the actual failure or attack scenario.

---

# Distinguish Defects from Suggestions

A review should clearly distinguish:

* **Must fix** — implementation is incorrect, unsafe, or materially risky.
* **Should fix** — meaningful quality or maintainability issue.
* **Could improve** — optional improvement.
* **Informational** — observation only.

Do not turn personal style preferences into defects.

---

# Review Conclusion

After evaluating the implementation, provide one of:

### PASS

No material defects were identified.

Minor optional improvements may still exist, but they do not justify another implementation cycle.

### CHANGES_REQUESTED

One or more material findings should be addressed.

List the findings ordered by severity.

### HUMAN_REVIEW_REQUIRED

The reviewer cannot reliably determine correctness because of unresolved ambiguity, missing information, external dependencies, or a conflict in requirements.

Explain exactly what information is needed.

---

# Review Output Format

Use the following structure:

```text
## Review Result

Status: PASS | CHANGES_REQUESTED | HUMAN_REVIEW_REQUIRED

## Summary

Briefly describe the overall assessment.

## Findings

### [Severity] Finding title

- Location:
- Problem:
- Why it matters:
- Scenario:
- Recommendation:

...

## Test Assessment

Describe whether the current tests adequately cover the important behavior.

## Risk Assessment

Briefly summarize remaining correctness, security, maintainability, and regression risks.

## Recommendation

State whether the implementation should be accepted, revised, or escalated to human review.
```

If there are no findings, explicitly state:

```text
No material findings identified.
```

Do not invent findings to make the review appear thorough.

---

# Review Boundaries

This skill should:

* inspect the implementation
* inspect relevant tests
* inspect relevant repository context
* challenge assumptions
* identify actionable defects
* report risks independently

This skill should not normally:

* implement fixes
* rewrite the implementation
* refactor unrelated code
* expand scope
* impose personal stylistic preferences
* approve an implementation merely because tests pass

Fixes belong to the implementation workflow.

---

# Completion Criteria

The review is complete when:

* the requested behavior is understood
* relevant implementation paths were inspected
* the final diff was examined
* relevant tests were examined
* correctness was challenged
* regression risks were considered
* relevant security risks were considered
* maintainability and readability were evaluated
* meaningful edge cases were considered
* findings were classified by severity
* the final review status was explicitly stated

The review should be concise enough to act on, but detailed enough that another developer can reproduce and understand every substantive finding.
