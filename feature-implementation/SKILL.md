---
name: feature-implementation
description: "Workflow skill for implementing features, behavior changes, and bug fixes using a test-driven development approach. Use when: implementing a new feature, changing existing behavior, or fixing a bug that requires code changes. Guides repository inspection, requirements analysis, planning, TDD, implementation, refactoring, and validation."
license: MIT
---

# Feature Implementation Skill

Use this skill for feature work, behavior changes, and bug fixes that require code changes. It covers implementation only; use dedicated workflows for review, documentation maintenance, release, deployment, or pull requests.

## Principles

- Inspect relevant implementation, tests, configuration, documentation, and repository guidance before editing.
- Follow repository-specific instructions and conventions; do not invent a competing pattern.
- Prefer existing abstractions and dependencies, minimal changes, preserved public behavior, and no speculative refactoring.
- Test observable behavior and meaningful success, failure, boundary, and regression cases rather than chasing coverage metrics.

## Workflow

### 1. Analyze the Request

Identify the requested behavior, expected outcome, inputs and outputs, constraints, affected existing behavior, and possible breaking changes. Establish concrete acceptance criteria before implementation. Ask only focused questions that repository inspection cannot answer.

### 2. Inspect the Repository

Inspect only relevant areas. Check existing implementation and tests, build and package configuration, APIs and CLI definitions, schemas, CI, documentation, repository instructions, and reusable abstractions. Determine where the change belongs, what tests and conventions apply, which validation commands are relevant, and whether compatibility or migration concerns exist. Do not edit during inspection.

Before implementation, create a concise plan covering behavior, tests, implementation, validation, and risks. Resolve ambiguities that could materially change behavior before making irreversible changes.

### 3. Follow TDD

For each meaningful behavior, repeat:

1. **Red:** write the smallest useful failing test and confirm it fails for the expected reason.
2. **Green:** implement the minimum change needed to pass, then run the new and relevant existing tests.
3. **Refactor:** improve naming, control flow, duplication, responsibilities, errors, and readability without changing behavior; rerun tests.

Do not skip Red unless TDD is impractical; explain the deviation and use the closest test-first approach. Prefer several small cycles for independent behaviors. See [TDD and quality details](references/tdd-and-quality.md) when the detailed checklist is needed.

### 4. Preserve Quality and Boundaries

Preserve behavior that is not being changed, public APIs, and expected backward compatibility. For relevant trust boundaries, validate input, preserve security controls, avoid sensitive-data exposure and unsafe parsing or execution, and follow existing mechanisms. Consider realistic error and edge cases without adding speculative complexity.

### 5. Validate and Complete

Run targeted tests first, then relevant regression tests and repository checks such as type checking, linting, builds, packaging, or documentation validation. Inspect `git diff` and `git status`; confirm only intended files changed, tests and documentation are included where needed, and no debug or temporary artifacts remain. See [Validation and completion](references/validation-and-completion.md) for the detailed checklist and reporting format.

## Failure and Ambiguity Rules

- Fix failures caused by the implementation.
- Correct a test only when requirements or established repository behavior show its assumption is wrong.
- Do not alter unrelated code to hide unrelated failures; report them separately.
- If requirements conflict, identify the conflict, prioritize explicit requirements, and add compatibility or migration handling as needed.
- Do not claim completion while known validation failures remain unexplained.

## Completion Criteria

Complete only when acceptance criteria are met, appropriate tests are added or updated, TDD was followed or its deviation documented, relevant validation passes, existing behavior is preserved unless intentionally changed, the final diff is scoped, required documentation is updated, and no known in-scope issue remains.
