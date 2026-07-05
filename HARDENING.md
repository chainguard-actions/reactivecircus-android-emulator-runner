<!-- markdownlint-disable -->

# Hardening Report: reactivecircus--android-emulator-runner--/v2.38.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **reactivecircus--android-emulator-runner--/v2.38.0** was hardened automatically. 7 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files use action references pinned to mutable tags/versions instead of full 40-character commit SHAs, making them vulnerable to supply-chain attacks. Failing references: actions/checkout@v6, krzema12/github-actions-typing@v2

Locations:

- `.github/workflows/action-types.yml:11`
- `.github/workflows/action-types.yml:12`

### unpinned-uses (severity: high)

Multiple workflow files use action references pinned to mutable tags/versions instead of full 40-character commit SHAs. Failing references: actions/checkout@v6, actions/setup-java@v5, actions/cache@v5, gradle/actions/setup-gradle@v5

Locations:

- `.github/workflows/main.yml:44`
- `.github/workflows/main.yml:50`
- `.github/workflows/main.yml:55`
- `.github/workflows/main.yml:63`

### unpinned-uses (severity: high)

Multiple workflow files use action references pinned to mutable tags/versions instead of full 40-character commit SHAs. Failing references: actions/checkout@v6, actions/setup-java@v5, gradle/actions/setup-gradle@v5

Locations:

- `.github/workflows/manually.yml:47`
- `.github/workflows/manually.yml:53`
- `.github/workflows/manually.yml:57`

### missing-permissions (severity: medium)

Workflow file has no top-level permissions: key and no job-level permissions: key on any job. This means the workflow runs with default (potentially broad) permissions.

Locations:

- `.github/workflows/action-types.yml:1`

### missing-permissions (severity: medium)

Workflow file has no top-level permissions: key and no job-level permissions: key on any job. This means the workflow runs with default (potentially broad) permissions.

Locations:

- `.github/workflows/main.yml:1`

### missing-permissions (severity: medium)

Workflow file has no top-level permissions: key and no job-level permissions: key on any job. This means the workflow runs with default (potentially broad) permissions.

Locations:

- `.github/workflows/manually.yml:1`

### missing-permissions (severity: medium)

Workflow file has no top-level permissions: key and no job-level permissions: key on any job. This means the workflow runs with default (potentially broad) permissions.

Locations:

- `.github/workflows/pr-comment.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 4 workflow files:
1. action-types.yml: Pinned actions/checkout@v6 to SHA df4cb1c069e1874edd31b4311f1884172cec0e10 and krzema12/github-actions-typing@v2 to SHA 9ddf35b71a482be7d8922b28e8d00df16b77e315. Added 'permissions: {}' top-level block.
2. main.yml: Pinned actions/checkout@v6, actions/setup-java@v5, actions/cache@v5, and gradle/actions/setup-gradle@v5 to their full commit SHAs. Added 'permissions: {}' top-level block.
3. manually.yml: Pinned actions/checkout@v6, actions/setup-java@v5, and gradle/actions/setup-gradle@v5 to their full commit SHAs. Added 'permissions: {}' top-level block.
4. pr-comment.yml: Added 'permissions: {}' top-level block (no unpinned actions in this file).

