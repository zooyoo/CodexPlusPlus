---
title: "Debug Notes"
readMode: optional
priority: medium
category: debug
keywords:
  - debug
  - issue
  - workaround
  - root-cause
  - gotcha
---

# Debug Notes

Category: debug

## Known Tooling State

- 2026-06-28: `maestro explore "project overview"` failed with `No endpoints configured. Configure ~/.maestro/api-explore.json with "endpoints" or legacy fields.` Use direct file reads and `rg` until explore endpoints are configured.
- 2026-06-28: No `.codegraph/` directory was detected at repository root, so CodeGraph should be skipped unless the user initializes it later.

## Entry Format

Add future debug notes with:

- Symptom
- Reproduction command
- Root cause evidence
- Fix
- Regression test
