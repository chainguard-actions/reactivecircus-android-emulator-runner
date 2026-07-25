<!-- markdownlint-disable -->

# Hardening Report: ReactiveCircus--android-emulator-runner/v2.38.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **ReactiveCircus--android-emulator-runner/v2.38.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference GitHub Actions using mutable version tags instead of pinned 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the referenced action tag is moved or compromised.

.github/workflows/action-types.yml:
  - uses: actions/checkout@v6
  - uses: krzema12/github-actions-typing@v2

.github/workflows/main.yml:
  - uses: actions/checkout@v6
  - uses: actions/setup-java@v5
  - uses: actions/cache@v5
  - uses: gradle/actions/setup-gradle@v5

.github/workflows/manually.yml:
  - uses: actions/checkout@v6
  - uses: actions/setup-java@v5
  - uses: gradle/actions/setup-gradle@v5

Locations:

- `.github/workflows/action-types.yml:12`
- `.github/workflows/action-types.yml:13`
- `.github/workflows/main.yml:46`
- `.github/workflows/main.yml:52`
- `.github/workflows/main.yml:56`
- `.github/workflows/main.yml:64`
- `.github/workflows/manually.yml:42`
- `.github/workflows/manually.yml:50`
- `.github/workflows/manually.yml:54`

### missing-permissions (severity: medium)

None of the workflow files define a top-level `permissions:` block, and no job in any file defines job-level permissions. Without explicit permissions, workflows run with the default token permissions (which may be read-write depending on repository settings), granting broader access than necessary. This is especially concerning for pr-comment.yml which triggers on `issue_comment` events (which can be triggered by untrusted contributors on pull requests) and main.yml which triggers on `pull_request` events.

Locations:

- `.github/workflows/main.yml:1`
- `.github/workflows/manually.yml:1`
- `.github/workflows/pr-comment.yml:1`
- `.github/workflows/action-types.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Pinned all action references to full 40-character commit SHAs in action-types.yml, main.yml, and manually.yml. Added top-level `permissions: {}` blocks to all four workflow files (action-types.yml, main.yml, manually.yml, pr-comment.yml) to enforce least-privilege access. The pr-comment.yml file is especially important as it triggers on issue_comment events which can be initiated by untrusted contributors.

