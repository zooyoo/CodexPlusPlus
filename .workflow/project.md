# Project: Codex++

## What This Is

Codex++ 是面向 Codex App 的外部增强启动器和管理工具。它通过外部 launcher 启动 Codex，并使用 Chromium DevTools Protocol 注入增强脚本，不修改 Codex App 原始安装文件。

## Core Value

在不破坏 Codex App 原始安装的前提下，为用户提供稳定的启动、增强注入、配置管理、更新和修复能力。

## Requirements

### Validated

<!-- Shipped and confirmed valuable. -->

- Rust 后端和静默 launcher，启动时不依赖额外运行时。
- Tauri + React 管理工具，支持深色/浅色切换。
- 外部 CDP 注入，不改 `app.asar`，不向 Codex 安装目录写入 DLL。
- 中转注入模式：支持多个中转配置，写入 `CodexPlusPlus` provider，并可切回官方 ChatGPT 登录态。
- 传统增强模式：插件入口解锁、特殊插件强制安装、会话删除、Markdown 导出、项目移动、Timeline 等。
- 用户脚本独立管理，可在启动时注入自定义脚本。
- GitHub Release 自动更新，管理工具和静默启动器都会检测可用更新。
- Windows 和 macOS 安装产物支持。

### Active

<!-- Current scope being built toward. These are hypotheses until shipped. -->

- [ ] 维护 Codex++ launcher、manager、core、data 各模块的现有能力。
- [ ] 保持 Windows 与 macOS 构建、测试和安装包流程可用。
- [ ] 在新增增强能力时保持不修改 Codex 原始安装文件的边界。

### Out of Scope

<!-- Explicit boundaries. Include reasoning to prevent re-adding. -->

- 修改 Codex App 原始安装文件或直接 patch `app.asar` — 项目定位是外部 launcher 和 CDP 注入。
- 把中转配置绑定到特定供应商 — README 明确兼容 API provider 只需匹配所选 upstream protocol 和 Codex configuration。

## Context

初始化依据：`README.md`、`README_EN.md`、`Cargo.toml`、`.github/workflows/pr-build.yml`、`CONTRIBUTING.md`。仓库是 Rust workspace，包含核心库、数据库和多个 app；管理工具前端位于 `apps/codex-plus-manager`，CI 使用 Node 22、Rust stable、TypeScript check、frontend build、`cargo test --workspace`、release build 和安装包构建。

## Constraints

- **Compatibility**: 不修改 Codex App 原始安装文件 — 这是 README 中声明的核心边界。
- **Packaging**: 需要支持 Windows installer 和 macOS x64/arm64 DMG — CI workflow 中存在对应构建任务。
- **Runtime**: launcher 启动时不依赖额外运行时 — README 的主要功能明确说明。
- **Quality**: 变更应通过 Rust 测试、前端 TypeScript 检查和构建验证 — `.github/workflows/pr-build.yml` 执行这些检查。

## Tech Stack

- **Language**: Rust 2024 edition，TypeScript
- **Framework**: Tauri 2.x，React，Vite
- **Database**: SQLite via `rusqlite`
- **Runtime / Tooling**: Node 22，Cargo workspace，NSIS，macOS DMG packaging scripts

## Key Decisions

<!-- Decisions that constrain future work. Add throughout project lifecycle. -->

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| 使用外部 launcher + Chromium DevTools Protocol 注入 | README 明确项目不修改 Codex App 原始安装文件 | Active |
| 使用 Rust workspace 管理 core、data、launcher、mobile relay、manager tauri 后端 | `Cargo.toml` 声明 workspace members | Active |
| 管理工具采用 Tauri + React | README 和 CI workflow 均体现该技术栈 | Active |
| 使用 GitHub Actions 构建 Windows 和 macOS 发布产物 | `.github/workflows/pr-build.yml` 定义对应 jobs | Active |

## Stakeholders

- Codex++ 维护者
- Codex++ 桌面用户
- 使用中转配置、增强功能、用户脚本和跨平台安装包的贡献者与用户

---
*Last updated: 2026-06-28 after forced initialization*
