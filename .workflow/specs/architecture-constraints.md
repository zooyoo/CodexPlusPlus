---
title: "Architecture Constraints"
readMode: required
priority: high
category: arch
keywords:
  - architecture
  - module
  - layer
  - boundary
  - dependency
  - structure
---

# Architecture Constraints

Category: arch

## Product Boundary

Codex++ 是 Codex App 的外部增强 launcher 和管理工具。核心边界是通过外部 launcher 和 Chromium DevTools Protocol 注入增强脚本，不修改 Codex App 原始安装文件，不直接 patch `app.asar`，不向 Codex 安装目录写入 DLL。

## Repository Structure

- `crates/codex-plus-core`：核心 Codex++ 逻辑，包括 launcher、CDP、bridge、relay、settings、update、install、watcher、zed remote 等模块。
- `crates/codex-plus-data`：本地数据处理、provider sync、Markdown 导出和 SQLite 相关逻辑，依赖 `codex-plus-core`。
- `apps/codex-plus-launcher`：静默 launcher 入口。
- `apps/codex-plus-manager`：Tauri + React 管理工具，前端在 `src/`，Tauri 后端在 `src-tauri/`。
- `apps/codex-plus-mobile-relay`：移动 relay 应用入口。
- `assets/inject`：注入脚本资产。
- `scripts/installer`：Windows NSIS 和 macOS DMG 打包脚本。

## Integration Rules

- 跨前后端命令 payload 应保持 camelCase JSON 形状，Rust 侧通过 serde 属性表达。
- 平台相关能力应隔离在 platform-specific 模块或 `#[cfg(...)]` 分支中。
- Manager UI 通过 Tauri commands 调用 Rust 能力；避免在前端复制核心业务规则。
- Relay injection 必须保持“官方登录态拥有账户能力，中转 profile 只控制 Base URL、key、model names”的边界。

## Packaging Constraints

- CI 需要 Windows artifacts、Windows installer、macOS x64 DMG、macOS arm64 DMG。
- Windows 构建依赖 NSIS；macOS bundle 需要校验 `Info.plist`、`PkgInfo`、可执行文件和签名信息。
