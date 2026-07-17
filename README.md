# my-opencode-golang

面向 Go 后端开发的 opencode 项目级配置，开箱即用。

> **注意：本仓库是纯配置项目，不含 Go 源代码。** 请将配置复制到你自己的 Go 项目中使用。本配置面向个人开发，非团队协作场景。

基于 [ECC (Everything Claude Code)](https://github.com/affaan-m/ECC) 的 opencode 配置裁剪定制、改进优化，专注 Go 后端开发。

主配置文件 `opencode.jsonc` 位于项目根目录（JSONC 格式支持注释）。

## 功能统计

| 类别 | 数量 | 说明 |
|------|------|------|
| Agents | 15 | 1 primary + 14 subagent |
| Commands | 14 | 斜杠命令 |
| Skills | 9 | 自动加载的领域知识 |

## 使用方式

直接将 `.opencode/` 目录和 `opencode.jsonc` 复制到你的 Go 项目根目录即可：

```bash
cp -r opencode.jsonc .opencode/ /path/to/your-go-project/
cd /path/to/your-go-project
opencode
```

## 项目结构

```
opencode.jsonc             # 主配置
.opencode/
├── AGENTS.md              # AI 行为指令
├── commands/              # 命令模板
├── prompts/agents/        # agent prompt
├── instructions/          # Go 开发指令
└── skills/                # 领域知识
```

## 模型配置

| 角色 | 模型 | 用途 |
|------|------|------|
| 主力模型 | `opencode/mimo-v2.5-free` | 主力 agent |
| 轻量模型 | `opencode/deepseek-v4-flash-free` | 大部分 subagent |
| 文档模型 | `opencode/big-pickle` | doc-updater、docs-lookup |

三者均为 OpenCode 免费模型。

## Agent 一览

| Agent | 用途 | 模型 |
|-------|------|------|
| build | 日常编码（primary） | 主力模型 |
| general | 调研分析、查资料（只读） | 主力模型 |
| explore | 代码库探索、文件搜索 | 轻量模型 |
| planner | 实现计划 | 主力模型 |
| architect | 架构设计 | 主力模型 |
| code-reviewer | 代码审查 | 轻量模型 |
| security-reviewer | 安全检查 | 轻量模型 |
| tdd-guide | 测试驱动开发 | 轻量模型 |
| build-error-resolver | 构建错误修复 | 轻量模型 |
| refactor-cleaner | 死代码清理 | 轻量模型 |
| doc-updater | 文档更新 | 文档模型 |
| docs-lookup | API 文档查询 | 文档模型 |
| harness-optimizer | 配置优化 | 轻量模型 |
| go-reviewer | Go 代码审查 | 轻量模型 |
| go-build-resolver | Go 构建修复 | 轻量模型 |

## 命令一览

| 命令 | 说明 |
|------|------|
| `/plan` | 创建实现计划 |
| `/tdd` | TDD 工作流 |
| `/code-review` | 代码审查 |
| `/security` | 安全审查 |
| `/build-fix` | 修复构建错误 |
| `/refactor-clean` | 清理死代码 |
| `/update-docs` | 更新文档 |
| `/update-codemaps` | 更新 codemap |
| `/test-coverage` | 测试覆盖率分析 |
| `/go-review` | Go 代码审查 |
| `/go-test` | Go TDD |
| `/go-build` | Go 构建修复 |
| `/verify` | 验证循环 |
| `/checkpoint` | 保存进度 |

## 模型切换说明

OpenCode TUI 中切换模型（`/models` → 选择模型）**仅影响 primary agent（build）**，build 模式和 plan 模式共用 primary agent，因此两者都会被 TUI 切换覆盖。

所有 subagent（planner、explore、code-reviewer 等）不受 TUI 切换影响，始终使用 `opencode.jsonc` 中显式指定的 `model`。

根据实际开发需求和预算，可自行编辑 `opencode.jsonc` 调整每个 agent 使用的模型。例如为 explore 更换其他免费或付费模型，或为特定 agent 指定更高性能的模型。

## 推荐 MCP

以下 MCP 服务器可增强 opencode 能力，可按需安装：

### Context7 — 文档查询

检索最新库和框架的官方文档，避免依赖训练数据的过时信息。

### CodeGraph — 代码知识图谱

将本地代码索引为图结构，帮助 AI 理解跨文件的调用链、类型引用和依赖关系，减少不必要的文件读取。

### agent-browser — 浏览器自动化

控制 Chrome/Edge 浏览器，支持导航、点击、表单填充、截图和页面内容提取，适合 Web 测试和数据抓取。

