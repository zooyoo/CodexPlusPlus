---
title: "Quality Rules"
readMode: required
priority: medium
category: review
keywords:
  - quality
  - lint
  - rule
  - enforcement
---

# Quality Rules

Category: review

## CI Gates

The PR build workflow runs these checks:

- Install frontend dependencies in `apps/codex-plus-manager` with Node 22.
- TypeScript check: `npm run check`.
- Frontend build: `npm run vite:build`.
- Rust tests: `cargo test --workspace`.
- Release build: `cargo build --release`.
- Package Windows installer and macOS DMG artifacts.

## Local Expectations

- For Rust-only changes, run the narrow crate test first when possible, then `cargo test --workspace` for shared behavior.
- For manager frontend changes, run `npm run check` and `npm run vite:build` in `apps/codex-plus-manager`.
- For packaging or installer changes, inspect the relevant scripts under `scripts/installer/` and run the closest platform-specific build command available.
- Do not hide failures with skipped tests, broad ignores, `as any`, or empty error handling.
