# Review Criteria

This document defines the **minimum common review criteria** for adversarial reviews.

It is intentionally technology- and project-agnostic.

Projects may define additional review criteria based on their architecture, domain, security requirements, runtime environment, and development practices.

---

## 1. Correctness

* [ ] Does the implementation satisfy the stated requirements?
* [ ] Does it behave correctly in the normal case?
* [ ] Are important boundary and edge cases handled?
* [ ] Are invalid or unexpected inputs handled appropriately?
* [ ] Does error behavior match the intended behavior?
* [ ] Are existing behaviors preserved where they should be?

---

## 2. Regression Safety

* [ ] Could the change break existing functionality?
* [ ] Are affected existing code paths still valid?
* [ ] Are public interfaces, configuration, or data formats unintentionally changed?
* [ ] Is there an appropriate regression test for the changed behavior when needed?

---

## 3. Test Quality

* [ ] Are the important behaviors covered by tests?
* [ ] Do tests verify observable behavior rather than only implementation details?
* [ ] Are important failure and edge cases tested?
* [ ] Would the tests actually fail if the implementation were incorrectly changed?
* [ ] Is there unnecessary or misleading test coverage?

---

## 4. Security

Consider security risks relevant to the implementation.

* [ ] Is untrusted input handled safely?
* [ ] Could the change expose sensitive information?
* [ ] Could the change introduce an unintended security boundary violation?
* [ ] Are permissions, access control, or authentication concerns handled where applicable?
* [ ] Are unsafe operations or dependencies introduced where applicable?

If a category is not applicable to the project or change, skip it.

---

## 5. Error Handling

* [ ] Are expected failures handled appropriately?
* [ ] Are errors propagated or reported correctly?
* [ ] Are errors accidentally swallowed?
* [ ] Can a failed operation be incorrectly reported as successful?
* [ ] Are partial failures or cleanup concerns handled where applicable?

---

## 6. Maintainability

* [ ] Is the implementation reasonably easy to modify?
* [ ] Are responsibilities appropriately separated?
* [ ] Is unnecessary duplication introduced?
* [ ] Is unnecessary complexity introduced?
* [ ] Does the implementation follow the existing project's conventions where appropriate?

Do not require refactoring solely for stylistic preference.

---

## 7. Readability

* [ ] Are names clear and meaningful?
* [ ] Is the control flow understandable?
* [ ] Are important assumptions apparent from the code?
* [ ] Are comments accurate and useful where comments are needed?
* [ ] Is there unnecessarily clever or obscure code?

---

## 8. Scope

* [ ] Does the change stay within the requested scope?
* [ ] Are unrelated files or behaviors changed unnecessarily?
* [ ] Are new dependencies or configuration changes justified?
* [ ] Is there unnecessary over-engineering?

---

## 9. Project-Specific Criteria

Before completing the review, check whether the repository defines additional criteria in:

* repository instructions
* contribution guidelines
* architecture documentation
* security requirements
* coding standards
* test strategy
* CI/CD requirements
* domain-specific documentation

Project-specific criteria take precedence over this generic checklist when they are more restrictive or specific.

---

## Minimum Review Standard

A review should at minimum consider:

1. Correctness
2. Regression safety
3. Test quality
4. Security
5. Error handling
6. Maintainability
7. Readability
8. Scope

Not every item will apply to every project or change.

The reviewer should use judgment rather than mechanically checking every item.
