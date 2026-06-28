---
title: "Learnings"
readMode: optional
priority: medium
category: learning
keywords:
  - bug
  - lesson
  - gotcha
  - learning
---

# Learnings

Category: learning

## How To Add Entries

Use this file for durable project lessons discovered during implementation, debugging, reviews, and releases. Each entry should include:

- Date
- Context
- Evidence
- Decision or lesson
- Follow-up, if any

## Current Baseline

- 2026-06-28: Forced initialization established project knowledge from `README.md`, `README_EN.md`, `Cargo.toml`, `.github/workflows/pr-build.yml`, `CONTRIBUTING.md`, and representative source files.
- 2026-06-28: `maestro explore` could not run because no endpoints were configured in `~/.maestro/api-explore.json`; codebase scanning used direct file reads and `rg` output instead.
