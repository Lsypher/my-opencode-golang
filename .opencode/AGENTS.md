# OpenCode Golang — Agent Instructions

Go 后端开发的独立 opencode 配置。

## Core Principles

1. **Agent-First** — Delegate domain tasks to specialized agents
2. **Test-Driven** — Write tests before implementation, 80%+ coverage
3. **Security-First** — Validate all inputs, no hardcoded secrets
4. **Plan Before Execute** — Plan complex features before coding

## Anti-Patterns (Go Specific)

These are unconditionally forbidden:

- **No catch-all files.** Never create `utils.go`, `helpers.go`, `common.go` — use descriptive filenames.
- **No `panic` for error handling.** Return errors instead of panicking.
- **No `init()` function abuse.** Prefer explicit initialization.
- **No exported functions without godoc.** Every exported symbol must have a comment.
- **No `interface{}` or `any` without clear reason.** Prefer concrete types.
- **No commented-out code.** Dead code belongs in git history, not in the source file.
- **No AI filler comments.** Comments explain WHY, not WHAT.

## Comment Discipline (Go)

- Exported functions: `// FunctionName does X` (godoc format)
- Unexported functions: explain why, not what
- No commented-out code — git history preserves it
- No AI boilerplate ("Initialize", "Set up", "Create") — the code speaks for itself

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
