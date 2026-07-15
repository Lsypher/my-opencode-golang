# my-opencode-golang

面向 Go 后端开发的 opencode 项目级配置，开箱即用。

## 功能

| 类别 | 数量 | 说明 |
|------|------|------|
| Agents | 13 | build、planner、architect、code-reviewer、security-reviewer、tdd-guide、go-reviewer 等 |
| Commands | 14 | /plan、/tdd、/code-review、/go-review、/go-test、/go-build 等 |
| Skills | 8 | golang-patterns、backend-patterns、api-design、tdd-workflow、security-review 等 |

## 使用方式

将 `opencode.json` 和 `.opencode/` 复制到你的 Go 项目根目录，运行 `opencode` 即可：

```bash
cp -r opencode.json .opencode/ /path/to/your-go-project/
cd /path/to/your-go-project
opencode
```

## 项目结构

```
opencode.json              # 根配置
.opencode/
├── opencode.json          # 主配置（agents/commands/skills）
├── AGENTS.md              # agent 使用说明
├── commands/              # 14 个命令模板
├── prompts/agents/        # 12 个 agent prompt
├── instructions/          # Go 开发指令
└── skills/                # 8 个精选技能
```

## 可用 Agent

| Agent | 用途 |
|-------|------|
| build | 日常编码 |
| planner | 实现计划 |
| architect | 架构设计 |
| code-reviewer | 代码审查 |
| security-reviewer | 安全检查 |
| tdd-guide | 测试驱动开发 |
| build-error-resolver | 构建错误修复 |
| refactor-cleaner | 死代码清理 |
| doc-updater | 文档更新 |
| docs-lookup | API 文档查询 |
| harness-optimizer | 配置优化 |
| go-reviewer | Go 代码审查 |
| go-build-resolver | Go 构建修复 |

## 可用命令

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

## 无外部依赖

纯配置文件，不需要 npm、Node.js 或其他运行时依赖。
