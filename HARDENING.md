<!-- markdownlint-disable -->

# Hardening Report: gradle--wrapper-validation-action/v3.5.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **gradle--wrapper-validation-action/v3.5.0** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

action.yml references `gradle/actions/wrapper-validation@v3.5.0` using a mutable version tag instead of a pinned 40-character commit SHA. This exposes the action to supply-chain attacks if the tag is moved or the upstream repository is compromised.

Locations:

- `action.yml:30`

### unpinned-uses (severity: high)

.github/workflows/ci.yml references `actions/checkout@v4` (used in two jobs) using a mutable version tag instead of a pinned 40-character commit SHA. This exposes the workflow to supply-chain attacks.

Locations:

- `.github/workflows/ci.yml:16`
- `.github/workflows/ci.yml:36`

### missing-permissions (severity: medium)

.github/workflows/ci.yml has no top-level `permissions:` key and neither job (`test-validation-success`, `test-validation-error`) defines its own `permissions:` block. Without explicit permissions, the workflow inherits the repository default (which may be `write-all`), granting broader access than necessary.

Locations:

- `.github/workflows/ci.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed 3 findings across 2 files:
1. hardened/action/action.yml: Pinned `gradle/actions/wrapper-validation@v3.5.0` → `@d9c87d481d55275bb5441eef3fe0e46805f9ef70 # v3.5.0`.
2. hardened/action/.github/workflows/ci.yml: Pinned both `actions/checkout@v4` references → `@11d5960a326750d5838078e36cf38b85af677262 # v4`.
3. hardened/action/.github/workflows/ci.yml: Added `permissions: {}` at the workflow top level and `permissions: contents: read` to each job (`test-validation-success` and `test-validation-error`), which is the minimum required for `actions/checkout` to clone the repository.

