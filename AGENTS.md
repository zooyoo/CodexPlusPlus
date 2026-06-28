# Repository Guidelines

## 项目结构与模块组织

这是 Rust workspace，根 `Cargo.toml` 管理成员和共享依赖。核心逻辑在 `crates/codex-plus-core`，数据处理和 provider sync 在 `crates/codex-plus-data`。应用入口位于 `apps/`：`codex-plus-launcher` 是静默启动器，`codex-plus-mobile-relay` 是移动 relay，`codex-plus-manager` 是 Tauri + React 管理工具，其中前端在 `apps/codex-plus-manager/src`，Tauri 后端在 `apps/codex-plus-manager/src-tauri`。注入脚本和图片资源分别在 `assets/`、`docs/images/`，安装脚本在 `scripts/installer/`。

## 构建、测试与开发命令

- `cargo build --release`：构建 Rust workspace release 产物。
- `cargo test --workspace`：运行 CI 使用的 Rust workspace 测试。
- `cargo fmt`：格式化 Rust 代码。
- `cargo clippy`：执行 Rust lint 检查。
- `cd apps/codex-plus-manager && npm install --package-lock=false`：安装管理工具前端依赖，CI 使用 Node 22。
- `cd apps/codex-plus-manager && npm run check`：运行 TypeScript 类型检查。
- `cd apps/codex-plus-manager && npm run vite:build`：构建管理工具前端。
- `cd apps/codex-plus-manager && npm run vite:dev`：在 `127.0.0.1:1420` 启动 Vite dev server。

## 编码风格与命名约定

Rust 使用 edition 2024，模块和函数使用 `snake_case`，公共结构体和 enum 使用 `PascalCase`。共享依赖优先放在 workspace dependencies。跨前后端 JSON payload 使用 serde，并保持 `camelCase` 字段。前端开启 TypeScript `strict`，使用 `@/*` 路径别名；React 组件使用 `PascalCase`，基础 UI 组件放入 `src/components/ui/`。样式组合优先使用 `cn()`、`clsx`、`tailwind-merge` 和 `class-variance-authority`。

## 测试指南

Rust 集成测试放在各 crate 的 `tests/` 目录，例如 `crates/codex-plus-core/tests/*.rs`、`crates/codex-plus-data/tests/*.rs`；局部模块测试可放在源码旁的 `tests.rs`。新增文件系统、SQLite、relay、CDP bridge、installer、update 或 worktree 行为时，应补充相邻测试。前端当前没有独立 test runner，至少运行 `npm run check` 和 `npm run vite:build`。

## 提交与 Pull Request 要求

近期历史包含 `feat(...)`、`fix:`、`docs:`、`test:` 等 Conventional Commits，也有少量 `Add files via upload`。新提交请优先使用清晰类型前缀，例如 `feat: 添加中转配置校验`、`fix: 修复更新架构选择`。PR 应说明变更目的、影响范围、验证命令；涉及 UI 时附截图，涉及 issue 时链接对应编号。提交前确认相关测试通过，不要用跳过测试或忽略错误掩盖问题。

## 架构与配置边界

Codex++ 的核心边界是外部 launcher + Chromium DevTools Protocol 注入：不要修改 Codex App 原始安装文件，不要直接 patch `app.asar`，不要向 Codex 安装目录写入 DLL。平台相关逻辑应使用 `#[cfg(...)]` 或平台模块隔离。
