---
name: doc-maintenance
description: "Workflow skill for proactively updating stale docs and fixing docs path/layout drift. Use when: docs in README.md or docs/** are outdated, command usage has changed, or documentation file/folder placement changed."
---

# Documentation Maintenance Skill

## Overview

This skill standardizes how to keep repository documentation accurate when command usage, setup steps, or file placement changes over time.

**Primary goals:**

- Detect stale command examples and outdated explanations
- Update references when docs files/folders move
- Keep `README.md`, `docs/**`, `.github` guidance, and guidance assets aligned
- Prefer minimal, surgical edits; only reorganize structure when necessary to resolve path/layout drift or duplicated/conflicting instructions
- Preserve existing terminology, tone, and formatting conventions unless they are incorrect or inconsistent.

## Scope

**Default inclusion:**

- `README.md` and other repository-level documentation
- `docs/**`
- contributor/developer guidance files
- agent instruction files
- documentation-related examples and assets when relevant

---

## Source of Truth

When documentation conflicts with repository behavior, treat executable or authoritative repository sources as the source of truth.

Prefer, in order:
1. Explicit user requirements
2. Current intended behavior confirmed by implementation/configuration and tests
3. Automated CI workflows
4. Existing documentation
5. Historical documentation or assumptions

Never change working code solely to make it match stale documentation unless the user explicitly requests a behavior change.

## Workflow

### 1. Inspect repository

Run this workflow when any of the following happens:

- Documentation may be stale after a code or configuration change
- A command, option, API, setup step, or workflow has changed
- Documentation files or directories have been moved or renamed
- Broken links or invalid paths are reported
- A pull request changes behavior that is documented in README.md or docs/

Inspect the relevant repository sources before editing.

Compare documentation against only the authoritative repository sources relevant to the documented behavior, such as:

- package.json / pyproject.toml / Cargo.toml / go.mod / Makefile
- CLI argument definitions
- configuration files
- CI workflows
- source code and exported APIs
- existing documentation indexes

### 2. Detect drift

Find where docs are stale or paths are invalid:

1. Verify docs links and relative paths from each markdown file location
2. Detect folder placement drift (moved/renamed docs files)
3. Identify duplicated instructions that should point to a shared source file

**Output format:**

If there are many changes, or if it appears there will be many, please summarize the detected drifts:

```
Drift Report
- Command drift: [file + section + expected command]
- Path drift: [file + broken link + corrected link]
- Structure drift: [old path -> new path]
```

### 3. Determine scope

**Objective:** Confirm update boundaries before editing.

**Default inclusion:**

- `README.md`, `docs/**`, `.github` guidance docs, guidance assets

**Default exclusion:**

- Runtime source code behavior changes
- Dependency upgrades unrelated to doc accuracy

If uncertainty remains, ask focused clarification before editing.

### 4. Update docs

**Objective:** Decide how to update docs safely and consistently.

- Keep changes limited to documentation accuracy and coherence.
- Preserve existing terminology, tone, and formatting conventions unless they are incorrect or inconsistent.

- Keep short, contextual examples inline when they improve readability
- Consolidate large or frequently duplicated examples only when a shared source materially reduces maintenance cost

- Preserve bilingual parity for paired docs when applicable
- When adding locale-specific docs with untranslated bodies, add a clear placeholder note near the top to avoid misleading readers
- Use native language labels in locale document headings where practical (for example, `हिन्दी`, `한국어`, `简体中文`, `繁體中文`)

- Rewrite outdated file links using valid relative paths.
- Update cross-references in `.github` docs if docs paths changed.

- Confirm the new location from the repository state/history or user request.
- Update inbound references.
- Update contributor guidance that cites the old path.

Execution checklist:

1. Update stale command text and explanations
2. If examples are intentionally shared across multiple documents, use an existing shared examples/assets directory rather than introducing a new structure unnecessarily.
3. Replace duplicated large or frequently changing examples with links to shared example files when this improves maintainability.

### 5. Validate

Confirm documentation is internally consistent:

1. Run the repository's relevant build, test, or documentation validation commands when documentation changes could affect them.
2. Verify no broken internal links in edited docs
3. Confirm referenced files actually exist
4. Confirm and review no unintended files were modified (`git status`and `git diff`) to ensure changes are limited to the intended documentation updates.
5. Search for stale references to the old command, path, filename, or terminology using repository-wide search tools (e.g., `grep`, `rg`, IDE search).

---

## Rules

### Minimal changes

- Do not change runtime behavior to accommodate stale documentation.
- Avoid unrelated refactors and metadata changes.

### Links and paths

- Resolve relative links from the location of each Markdown file.
- Confirm every referenced file and directory exists after an update.

### Examples

- Keep examples short and contextual when inline examples improve readability.
- Use shared example files when the same large example is repeated and an existing assets directory is available.

### Localization

- Keep paired documentation in bilingual parity when applicable.
- Clearly mark untranslated locale documents as English placeholders.
- Use native language labels in locale headings where practical.

### File moves

- Confirm the destination path from repository state, history, or the user's request.
- Update inbound references and contributor guidance after a move.

## Common Patterns

### Pattern A: Command usage drift

When a documented command differs from actual workflow:

1. Update command in docs
2. Update explanation text that depends on the old command
3. Update troubleshooting guidance if symptoms changed

### Pattern B: File placement drift

When documentation files have been intentionally moved or renamed:

1. Confirm the new location from the repository state/history or user request.
2. Update inbound references.
3. Update contributor guidance that cites the old path.

### Pattern C: Shared setup examples

When setup snippets repeat in multiple guides:

1. Prefer an existing shared examples/assets directory when one exists.
2. Move canonical snippets there only when doing so materially reduces maintenance cost.
3. Link from each guide section to the canonical file.
4. Keep local guide text concise and task-oriented.

### Pattern D: Locale docs with placeholder content

When adding language-specific guide files before full translation is ready:

1. Keep heading language label consistent with native naming conventions
2. Add a short note near the top that the body is currently an English placeholder
3. Reflect this status in `README.md` documentation index if relevant

---

## Reporting

Report completed work with a concise summary of changed commands, paths, structure, and validation results.

### Example Run

```
User request:
"README.md and docs setup commands are outdated, and docs folders changed."

Skill output summary:
- Updated stale setup commands in README/docs
- Repointed broken links to new docs paths
- Consolidated devcontainer examples under docs/guidance/assets
- Replaced duplicate snippets with references in prerequisites sections
```

---

## When This Skill Does NOT Apply

- Implementing runtime features unrelated to documentation
- Fixing application bugs without documentation impact
- Broad dependency migration not tied to docs accuracy

---
