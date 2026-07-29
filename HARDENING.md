<!-- markdownlint-disable -->

# Hardening Report: benmatselby--gollum-page-watcher-action/v1.11.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **benmatselby--gollum-page-watcher-action/v1.11.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/build.yml references three Actions by mutable version tags instead of pinned 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks if those tags are moved: (1) actions/setup-go@v5, (2) actions/checkout@v4, (3) golangci/golangci-lint-action@v6.3.1. Each should be pinned to a full SHA, e.g. actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4.

Locations:

- `.github/workflows/build.yml:10`
- `.github/workflows/build.yml:17`
- `.github/workflows/build.yml:21`

### missing-permissions (severity: medium)

The workflow file .github/workflows/build.yml has no top-level `permissions:` key and the only job (`build`) also has no job-level `permissions:` key. Without explicit permissions the workflow inherits the repository default (typically write-all for private repos), granting unnecessarily broad access. A minimal permissions block (e.g. `contents: read`) should be added.

Locations:

- `.github/workflows/build.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/build.yml: (1) Pinned all three action references to full commit SHAs — actions/setup-go@v5 → @40f1582b2485089dde7abd97c1529aa768e1baff, actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262, golangci/golangci-lint-action@v6.3.1 → @2e788936b09dd82dc280e845628a40d2ba6b204c — with original tags preserved as inline comments. (2) Added top-level `permissions: contents: read` block to restrict the workflow to the minimum permissions needed.

