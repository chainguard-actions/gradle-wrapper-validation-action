<!-- markdownlint-disable -->

# Hardening Report: gradle--wrapper-validation-action/v3.5.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **gradle--wrapper-validation-action/v3.5.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The composite action step uses `gradle/actions/wrapper-validation@v3.5.0`, which is pinned to a mutable version tag rather than an immutable 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit, enabling supply-chain attacks. It should be pinned to a full SHA, e.g. `gradle/actions/wrapper-validation@<40-char-sha> # v3.5.0`.

Locations:

- `action.yml:30`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced `gradle/actions/wrapper-validation@v3.5.0` with the pinned SHA reference `gradle/actions/wrapper-validation@d9c87d481d55275bb5441eef3fe0e46805f9ef70 # v3.5.0` in action.yml line 30. The mutable tag was resolved to its immutable 40-character commit SHA using the GitHub API.

