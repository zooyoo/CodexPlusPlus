---
title: "Test Conventions"
readMode: required
priority: high
category: test
keywords:
  - test
  - coverage
  - mock
  - fixture
  - assertion
  - framework
---

# Test Conventions

Category: test

## Rust Tests

- Integration tests live under crate-level `tests/` directories, for example `crates/codex-plus-core/tests/*.rs` and `crates/codex-plus-data/tests/*.rs`.
- Some focused module tests live near source modules, for example `crates/codex-plus-core/src/upstream_worktree/remote/tests.rs`.
- Tests use standard Rust `#[test]`; async behavior is covered where needed by project dependencies.
- Many tests use `tempfile` for isolated filesystem state.

## Frontend Checks

- No dedicated frontend test runner is configured in `apps/codex-plus-manager/package.json`.
- Frontend validation currently relies on `npm run check` and `npm run vite:build`.

## Common Commands

- Full Rust workspace: `cargo test --workspace`
- Rust all features per contributing guide: `cargo test --all-features`
- Frontend type check: `cd apps/codex-plus-manager && npm run check`
- Frontend build: `cd apps/codex-plus-manager && npm run vite:build`
