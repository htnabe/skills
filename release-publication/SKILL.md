---
name: release-publication
description: "Prepare and publish a software release using the repository release process. Use when asked to release a version, publish a package, or complete npm and GitHub Release publication, including dependency updates and publication verification."
license: MIT
user-invocable: true
---

# Release Publication

Complete the requested release, not merely its preparation PR. Follow repository-specific commands and workflow ordering rather than introducing a new release process. Apply registry, runtime, and GitHub-specific checks only when relevant to the target repository.

## 1. Establish Scope and Permissions

- Inspect the current branch, dirty worktree, latest release, pending dependency PRs, package metadata, CI, and documented publishing workflows.
- Preserve existing work. Separate unreleased branch commits, pending worktree edits, and changes introduced by this task.
- Summarize the intended release contents before editing, especially when an integration branch already contains substantial changes.
- Confirm whether dependency updates include major versions. Do not equate "no open Dependabot PRs" with "dependencies are current"; inspect available updates and failed update jobs when relevant.
- Confirm permission for push, PR merge, package publication, and release tags. Do not assume one permission grants the others.
- Keeping the working branch unchanged does not mean publishing from that branch. Respect existing branch and environment guards.
- Treat validation blockers separately from optional cleanup. Explain necessary fixes; obtain agreement before expanding into adjacent CI, toolchain, example, or documentation work outside the agreed scope.
- If the user questions scope, pause irreversible release actions until the concern is resolved.

## 2. Prepare and Validate

- Follow repository versioning and changelog conventions. Keep dependency manifests and lockfiles consistent; do not overwrite pending user updates.
- Check runtime and development-tool compatibility separately, including the target ecosystem's runtime versions and dependency constraints.
- Establish baseline failures when practical. For metadata/dependency-only changes, use existing tests and package smoke checks rather than inventing behavior tests solely to satisfy TDD.
- Run the repository's required lint, formatting, tests, type checks, build, and packaging checks as applicable.
- Verify which runner each command invokes. For example, `bun test` and `bun run test` can run different test frameworks.
- Ensure example and smoke commands actually exercise the package: an ignored fixture, no-op output, or fallback can return success without proving formatting or parsing works.
- Inspect package contents and test the packed artifact in isolation for representative supported inputs and expected output. Reuse an existing smoke check when available.
- Review the full release diff and directly relevant documentation. Do not turn a release into a broad cleanup.

## 3. Integrate the Validated Commit

- Follow the repository's integration process and the user's authorization. Use [git-commit-push-pr](../git-commit-push-pr/SKILL.md) for applicable commit, push, and PR preparation, including any repository PR template and exact validation results.
- Wait for relevant CI checks to pass. When using a PR, confirm its head is still the validated commit before merging.
- Record the actual release commit after integration; do not assume the local working branch has the same SHA.
- Preserve the requested working branch. If synchronization is authorized and needed, prefer a fast-forward; stop on unexpected divergence rather than resetting or force-pushing.

## 4. Publish and Verify

- Follow the repository's documented order. Some repositories publish before pushing a tag; others publish from tag-triggered workflows. Do not change that order or bypass publishing guards.
- Trigger the existing trusted workflow for the intended version and commit. Avoid replacing OIDC publishing with local tokens or ad hoc publication.
- Record the workflow run ID and verify both validation and publication steps, not only the overall run status.
- Check the actual registry for the version and intended distribution tag (`latest`, `rc`, or another configured tag). Verify source commit metadata when available.
- A successful publish can precede registry availability. If logs say the package is processing, use bounded retries with a delay and report pending status if the bound is reached. Do not republish, reuse the version, or bump it solely because metadata initially returns 404.
- Download the published artifact and compare its digest or bytes with the tested package when reproducible, or smoke-test the registry artifact itself.
- For publish-before-tag repositories, create and push the matching tag only after registry publication is verified. Point it at the published commit, not whichever branch happens to be checked out.
- Verify the remote tag's resolved commit and the GitHub Release's version, public/draft state, and prerelease status. A tag push alone does not prove a Release exists.
- Check an existing tag or release before creating one on a resumed run. Never move or overwrite a published tag to hide a mismatch.

## 5. Finish

- Confirm the requested working branch, worktree state, remote release commit, registry version/tag, and GitHub Release.
- Remove only specifically identified temporary validation files and directories.
- Report the published version and registry/Release links, key validation results, and any material limitation. Do not replace release results with a PR URL-only response.
- If an external step remains blocked or processing, state exactly what completed and what remains; do not claim the release is complete.
