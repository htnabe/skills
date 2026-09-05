# Review Reporting

## Finding Requirements

Every substantive finding includes:

1. Severity
2. Location
3. Problem
4. Why it matters
5. Concrete scenario
6. Recommended direction

Do not report vague theoretical concerns. Distinguish defects from optional improvements and do not inflate severity.

## Severity

- **Critical:** severe security impact, data loss, major system failure, or fundamentally unusable requested behavior.
- **High:** significant correctness, security, compatibility, or reliability problem that should block acceptance.
- **Medium:** meaningful defect, test gap, maintainability problem, or edge-case failure that should normally be addressed.
- **Low:** minor issue with limited practical impact.
- **Informational:** observation or optional improvement, not a defect.

## Finding Template

```text
### [Severity] Finding title

- Location: path/to/file:line
- Problem: [What is wrong]
- Why it matters: [Impact]
- Scenario: [Reproducible failure or attack path]
- Recommendation: [Concrete remediation direction]
```

## Result Format

```text
## Review Result

Status: PASS | CHANGES_REQUESTED | HUMAN_REVIEW_REQUIRED

## Summary
[Brief assessment]

## Findings
[Findings ordered by severity, or "No material findings identified."]

## Test Assessment
[Whether important behavior is adequately covered]

## Risk Assessment
[Remaining correctness, security, maintainability, and regression risks]

## Recommendation
[Accept, revise, or escalate]
```

Use `HUMAN_REVIEW_REQUIRED` when unresolved ambiguity, missing information, external dependencies, or requirement conflicts prevent reliable review.
