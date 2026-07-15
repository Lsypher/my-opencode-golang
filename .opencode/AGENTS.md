# OpenCode Golang — Agent Instructions

Go 后端开发的独立 opencode 配置。

## Core Principles

1. **Agent-First** — Delegate domain tasks to specialized agents
2. **Test-Driven** — Write tests before implementation, 80%+ coverage
3. **Security-First** — Validate all inputs, no hardcoded secrets
4. **Plan Before Execute** — Plan complex features before coding

## Agent Orchestration

Use agents proactively without user prompt:
- Complex features → **planner**
- Code just modified → **code-reviewer** or **go-reviewer**
- Bug fix or new feature → **tdd-guide** or **go-test**
- Architectural decision → **architect**
- Security-sensitive code → **security-reviewer**
- Go build errors → **go-build-resolver**
- Config reliability/cost → **harness-optimizer**

Run independent operations in parallel — launch multiple agents simultaneously.
