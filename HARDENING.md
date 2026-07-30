<!-- markdownlint-disable -->

# Hardening Report: ReactiveCircus--android-emulator-runner/v2.37.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **ReactiveCircus--android-emulator-runner/v2.37.0** was hardened automatically. 7 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Workflow uses action references pinned to mutable tags instead of full 40-character commit SHAs. Failing references: `actions/checkout@v6`, `krzema12/github-actions-typing@v2`.

Locations:

- `.github/workflows/action-types.yml:9`
- `.github/workflows/action-types.yml:10`

### unpinned-uses (severity: high)

Workflow uses action references pinned to mutable tags instead of full 40-character commit SHAs. Failing references: `actions/checkout@v6`, `actions/setup-java@v5`, `actions/cache@v5`, `gradle/actions/setup-gradle@v5`.

Locations:

- `.github/workflows/main.yml:38`
- `.github/workflows/main.yml:46`
- `.github/workflows/main.yml:51`
- `.github/workflows/main.yml:57`

### unpinned-uses (severity: high)

Workflow uses action references pinned to mutable tags instead of full 40-character commit SHAs. Failing references: `actions/checkout@v6`, `actions/setup-java@v5`, `gradle/actions/setup-gradle@v5`.

Locations:

- `.github/workflows/manually.yml:38`
- `.github/workflows/manually.yml:44`
- `.github/workflows/manually.yml:48`

### missing-permissions (severity: medium)

Workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the GITHUB_TOKEN is granted default (potentially write) permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/main.yml:1`

### missing-permissions (severity: medium)

Workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the GITHUB_TOKEN is granted default (potentially write) permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/manually.yml:1`

### missing-permissions (severity: medium)

Workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the GITHUB_TOKEN is granted default (potentially write) permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/action-types.yml:1`

### missing-permissions (severity: medium)

Workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the GITHUB_TOKEN is granted default (potentially write) permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/pr-comment.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 4 workflow files:
- action-types.yml: Pinned actions/checkout@v6 → SHA d23441a48e516b6c34aea4fa41551a30e30af803 and krzema12/github-actions-typing@v2 → SHA 9ddf35b71a482be7d8922b28e8d00df16b77e315; added `permissions: {}`
- main.yml: Pinned actions/checkout@v6, actions/setup-java@v5, actions/cache@v5, gradle/actions/setup-gradle@v5 to full SHAs; added `permissions: {}`
- manually.yml: Pinned actions/checkout@v6, actions/setup-java@v5, gradle/actions/setup-gradle@v5 to full SHAs; added `permissions: {}`
- pr-comment.yml: Added `permissions: {}` (no action references to pin)

