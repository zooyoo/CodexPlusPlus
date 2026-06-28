---
title: "UI Conventions"
readMode: optional
priority: medium
category: ui
keywords:
  - ui
  - design
  - color
  - typography
  - layout
  - animation
  - component
---

# UI Conventions

Category: ui

## Manager UI Stack

- React 19 with TypeScript strict mode.
- Vite with React plugin and Tailwind CSS Vite plugin.
- UI primitives live in `apps/codex-plus-manager/src/components/ui/`.
- Icons are available through `lucide-react`.

## Component Patterns

- Use existing UI primitives before introducing new ones.
- Use `cn()` from `@/lib/utils` to merge conditional class names.
- Use `class-variance-authority` for component variants when matching existing UI primitives.
- Components that support composition may use Radix `Slot` and an `asChild` prop.

## Styling Boundaries

- Keep manager UI consistent with the existing control-panel style rather than adding landing-page or marketing layouts.
- Preserve dark/light theme behavior already described by README.
- Favor compact controls and clear operational states for launch, diagnostics, settings, updates, relay configuration, enhancements, and scripts.
