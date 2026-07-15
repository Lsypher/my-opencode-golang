# my-opencode-golang

面向 Go 后端开发的 opencode 项目级配置，开箱即用。

基于 [ECC (Everything Claude Code)](https://github.com/affaan-m/ECC) 裁剪改造，仅保留 Go 后端开发所需的 agents、commands 和 skills。

主配置文件 `opencode.jsonc` 位于项目根目录（JSONC 格式支持注释）。

## 功能统计

| 类别 | 数量 | 说明 |
|------|------|------|
| Agents | 15 | 1 primary + 14 subagent |
| Commands | 14 | 斜杠命令 |
| Skills | 9 | 自动加载的领域知识 |

## 使用方式

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
| 主力模型 | `opencode/mimo-v2-5-free` | 主力 agent |
| 轻量模型 | `opencode/deepseek-v4-flash-free` | explore agent |

两者均为 OpenCode 免费模型。

## Agent 一览

| Agent | 用途 | 模型 |
|-------|------|------|
| build | 日常编码（primary） | 主力模型 |
| general | 调研分析、查资料（只读） | 主力模型 |
| explore | 代码库探索、文件搜索 | 轻量模型 |
| planner | 实现计划 | 主力模型 |
| architect | 架构设计 | 主力模型 |
| code-reviewer | 代码审查 | 主力模型 |
| security-reviewer | 安全检查 | 主力模型 |
| tdd-guide | 测试驱动开发 | 主力模型 |
| build-error-resolver | 构建错误修复 | 主力模型 |
| refactor-cleaner | 死代码清理 | 主力模型 |
| doc-updater | 文档更新 | 主力模型 |
| docs-lookup | API 文档查询 | 主力模型 |
| harness-optimizer | 配置优化 | 主力模型 |
| go-reviewer | Go 代码审查 | 主力模型 |
| go-build-resolver | Go 构建修复 | 主力模型 |

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
