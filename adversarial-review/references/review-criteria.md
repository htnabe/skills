# Review Criteria

Use this technology- and project-agnostic checklist for applicable dimensions. Repository-specific criteria may be stricter and take precedence.

## Correctness and Requirements

- Does the implementation satisfy explicit requirements and acceptance criteria?
- Does it behave correctly for normal, invalid, and boundary inputs?
- Are state transitions, return values, side effects, ordering, and asynchronous behavior correct?
- Is every meaningful requirement implemented and tested?

## Regression Safety and Scope

- Could existing functionality, public APIs, CLI behavior, configuration, data formats, error codes, or environment variables break?
- Are affected callers and code paths still valid?
- Does the change stay within scope without unrelated refactoring, over-engineering, unjustified dependencies, or configuration changes?
- Is a regression test present when needed?

## Test Quality

- Do tests express observable behavior?
- Do they cover important success, failure, edge, and regression cases?
- Would they fail if the implementation were incorrectly changed?
- Are assertions meaningful rather than implementation-detail coupled?
- Do mocks hide relevant failures?

## Security

Where applicable, consider:

- untrusted input, injection, command execution, path traversal, unsafe file operations, and unsafe deserialization
- authentication, authorization, permissions, insecure defaults, and trust-boundary violations
- secret exposure, sensitive-data leakage, logging, dependency risks, and denial of service

Report a security concern only with a plausible attack or failure path and meaningful risk.

## Error Handling and Resources

- Are expected and unexpected errors propagated or reported correctly?
- Are errors swallowed or failures reported as success?
- Are partial failures, cleanup, retry behavior, and user-facing messages intentional?
- Are performance costs, repeated work, memory growth, resource leaks, and external requests relevant and controlled?

## Maintainability and Readability

- Are responsibilities and abstractions appropriate?
- Is duplication, coupling, hidden state, or brittle configuration creating meaningful future cost?
- Are names, control flow, constants, assumptions, and comments clear and accurate?
- Is the code straightforward rather than needlessly clever?

## Project-Specific Criteria

Before completing the review, check repository instructions, contribution and architecture documentation, security requirements, coding standards, test strategy, and CI/CD requirements. Apply more restrictive project-specific criteria when present.

Not every item applies to every change. Use judgment rather than mechanically checking every box.
