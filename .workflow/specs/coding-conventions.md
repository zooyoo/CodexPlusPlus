---
title: "Coding Conventions"
readMode: required
priority: high
category: coding
keywords:
  - style
  - naming
  - import
  - pattern
  - convention
  - formatting
---

# Coding Conventions

Category: coding

## Detected Stack

- Rust workspace，edition `2024`，workspace members 定义在根 `Cargo.toml`。
- 桌面管理工具位于 `apps/codex-plus-manager`，使用 Tauri 2.x、React 19、TypeScript 5.8、Vite 6、Tailwind CSS 4。
- Rust 共享依赖通过 `[workspace.dependencies]` 管理；crate 内优先使用 `*.workspace = true`。

## Rust Conventions

- 按功能模块拆分文件，并在 `crates/codex-plus-core/src/lib.rs` 中导出公共模块。
- 公共数据结构使用 `serde::Serialize` / `Deserialize`，跨前后端 payload 常用 `#[serde(rename_all = "camelCase")]`。
- 错误处理优先使用 `anyhow::Result` 传递上下文，领域错误可使用 `thiserror`。
- Windows 专用逻辑使用 `#[cfg(windows)]` 或 target-specific dependencies 隔离。
- 测试放在 crate 级 `tests/` 目录，必要时也使用模块内 `tests.rs`。

## Frontend Conventions

- TypeScript 开启 `strict`，路径别名为 `@/* -> ./src/*`。
- React 组件使用函数组件；UI 基础组件位于 `src/components/ui/`。
- 样式组合使用 `cn()`，实现为 `twMerge(clsx(...))`。
- 变体样式使用 `class-variance-authority`，可组合 Radix `Slot` 支持 `asChild`。
- Vite dev server 固定 `127.0.0.1:1420` 且 `strictPort: true`。

## Formatting

- Rust 使用 `cargo fmt` 和 `cargo clippy`。
- 前端使用 TypeScript 编译检查：`npm run check`。
- 保持现有命名风格：Rust 模块和函数使用 snake_case，React 组件使用 PascalCase。
