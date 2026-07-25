<!-- markdownlint-disable -->

# Hardening Report: ReactiveCircus--android-emulator-runner/v2.38.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **ReactiveCircus--android-emulator-runner/v2.38.0** was hardened automatically. 7 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Workflow uses mutable tag references instead of pinned SHA commits. Unpinned refs: `actions/checkout@v6`, `actions/setup-java@v5`, `actions/cache@v5`, `gradle/actions/setup-gradle@v5`. These should be pinned to full 40-character commit SHAs.

Locations:

- `.github/workflows/main.yml:37`
- `.github/workflows/main.yml:43`
- `.github/workflows/main.yml:47`
- `.github/workflows/main.yml:57`

### unpinned-uses (severity: high)

Workflow uses mutable tag references instead of pinned SHA commits. Unpinned refs: `actions/checkout@v6`, `actions/setup-java@v5`, `gradle/actions/setup-gradle@v5`. These should be pinned to full 40-character commit SHAs.

Locations:

- `.github/workflows/manually.yml:37`
- `.github/workflows/manually.yml:43`
- `.github/workflows/manually.yml:47`

### unpinned-uses (severity: high)

Workflow uses mutable tag references instead of pinned SHA commits. Unpinned refs: `actions/checkout@v6`, `krzema12/github-actions-typing@v2`. These should be pinned to full 40-character commit SHAs.

Locations:

- `.github/workflows/action-types.yml:11`
- `.github/workflows/action-types.yml:12`

### missing-permissions (severity: medium)

Workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad. Add a top-level `permissions: {}` or minimal scoped permissions.

Locations:

- `.github/workflows/main.yml:1`

### missing-permissions (severity: medium)

Workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad. Add a top-level `permissions: {}` or minimal scoped permissions.

Locations:

- `.github/workflows/manually.yml:1`

### missing-permissions (severity: medium)

Workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad. Add a top-level `permissions: {}` or minimal scoped permissions.

Locations:

- `.github/workflows/action-types.yml:1`

### missing-permissions (severity: medium)

Workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any job. The `pr-comment.yml` workflow is triggered by `issue_comment` events (which can be created by any user on a PR) and delegates to `main.yml` via `workflow_call`, but has no permissions restriction. Add a top-level `permissions: {}` or minimal scoped permissions.

Locations:

- `.github/workflows/pr-comment.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 7 findings across 4 workflow files:

1. main.yml: Added `permissions: {}` at top level; pinned actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803, actions/setup-java@v5 → @03ad4de0992f5dab5e18fcb136590ce7c4a0ac95, actions/cache@v5 → @caa296126883cff596d87d8935842f9db880ef25, gradle/actions/setup-gradle@v5 → @0723195856401067f7a2779048b490ace7a47d7c

2. manually.yml: Added `permissions: {}` at top level; pinned actions/checkout@v6, actions/setup-java@v5, gradle/actions/setup-gradle@v5 with same SHAs as above

3. action-types.yml: Added `permissions: {}` at top level; pinned actions/checkout@v6 → @d23441a48e516b6c34aea4fa41551a30e30af803, krzema12/github-actions-typing@v2 → @9ddf35b71a482be7d8922b28e8d00df16b77e315

4. pr-comment.yml: Added `permissions: {}` at top level (no unpinned actions in this file)

All pinned SHAs were resolved via lookup_action_sha and include the original tag as a comment for readability.

