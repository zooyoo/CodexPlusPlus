---
title: "Review Standards"
readMode: required
priority: medium
category: review
keywords:
  - review
  - checklist
  - gate
  - approval
  - standard
---

# Review Standards

Category: review

## Review Focus

- Protect the external-launcher boundary: no Codex App installation patching, no `app.asar` modification, no DLL writes into the Codex install directory.
- Check cross-platform behavior for Windows and macOS when touching launcher, installer, paths, update, or integration code.
- Verify serde payload shape for Tauri command contracts, especially camelCase request/response fields consumed by the React UI.
- Prefer tests around filesystem, SQLite, relay, CDP bridge, worktree, installer, and update behavior because these areas have integration tests already.

## Evidence Standard

Review findings should cite file paths, line numbers where available, test output, or explicit assumptions. Avoid speculative conclusions without a verification path.
