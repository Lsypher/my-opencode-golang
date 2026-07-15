# Go 开发指令

## Security Guidelines (CRITICAL)

### 提交前安全检查

- [ ] 无硬编码密钥（API keys、密码、tokens）
- [ ] 所有用户输入已验证
- [ ] SQL 注入防护（参数化查询）
- [ ] 认证/授权已验证
- [ ] 错误信息不泄露敏感数据

### 密钥管理

```go
// 禁止：硬编码密钥
// apiKey := "sk-proj-xxxxx"

// 正确：环境变量
apiKey := os.Getenv("API_KEY")
if apiKey == "" {
    log.Fatal("API_KEY not configured")
}
```

## Go 编码规范

### 命名规范

- 包名：小写，单个单词，无下划线（如 `handler`、`service`）
- 导出标识符：PascalCase（如 `UserService`）
- 未导出标识符：camelCase（如 `getByID`）
- 接口：单方法接口以 `-er` 结尾（如 `Reader`、`Writer`）
- 错误变量：以 `err` 或 `Err` 开头（如 `ErrNotFound`）

### 错误处理

```go
// 禁止：忽略错误
result, _ := doSomething()

// 正确：处理错误
result, err := doSomething()
if err != nil {
    return fmt.Errorf("doSomething: %w", err)
}
```

### 并发

```go
// 使用 context 传递取消信号
func (s *Service) Process(ctx context.Context, data Data) error {
    // 使用 errgroup 管理 goroutine
    g, ctx := errgroup.WithContext(ctx)
    g.Go(func() error {
        return s.step1(ctx, data)
    })
    g.Go(func() error {
        return s.step2(ctx, data)
    })
    return g.Wait()
}
```

### 包组织

- 小包优于大包，每个包职责单一
- 按功能/领域组织，不按类型
- 内部包用 `internal/` 目录
- 导出符号必须有 godoc 注释

## 测试要求

### 最低覆盖率：80%

### TDD 流程

1. 先写测试（RED）
2. 最小实现让测试通过（GREEN）
3. 重构（IMPROVE）

### Go 测试模式

```go
func TestCalculate(t *testing.T) {
    tests := []struct {
        name    string
        input   Input
        want    Output
        wantErr bool
    }{
        {
            name:  "valid input",
            input: Input{Value: 10},
            want:  Output{Result: 20},
        },
        {
            name:    "invalid input",
            input:   Input{Value: -1},
            wantErr: true,
        },
    }

    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            got, err := Calculate(tt.input)
            if (err != nil) != tt.wantErr {
                t.Fatalf("Calculate() error = %v, wantErr %v", err, tt.wantErr)
            }
            if !reflect.DeepEqual(got, tt.want) {
                t.Errorf("Calculate() = %v, want %v", got, tt.want)
            }
        })
    }
}
```

### 测试命令

```bash
go test ./...              # 运行所有测试
go test -v ./...           # 详细输出
go test -cover ./...       # 覆盖率
go test -race ./...        # 竞态检测
go test -bench=. ./...     # 基准测试
go test -coverprofile=c.out ./... && go tool cover -html=c.out  # 覆盖率报告
```

## Git 工作流

### Commit 格式

```
<type>: <description>
```

类型：feat、fix、refactor、docs、test、chore、perf、ci

## 开发流程

1. **Plan** — 复杂功能先用 /plan 创建实现计划
2. **TDD** — 使用 /tdd 或 /go-test
3. **Review** — 代码修改后立即 /code-review 或 /go-review
4. **Security** — 敏感代码变更后 /security
5. **Commit** — 遵循 conventional commits 格式

## 可用 Agent

| Agent | 用途 |
|-------|------|
| planner | 实现计划 |
| architect | 架构设计 |
| tdd-guide | 测试驱动开发 |
| code-reviewer | 代码审查 |
| security-reviewer | 安全检查 |
| build-error-resolver | 构建错误修复 |
| refactor-cleaner | 死代码清理 |
| doc-updater | 文档更新 |
| go-reviewer | Go 代码审查 |
| go-build-resolver | Go 构建修复 |
| docs-lookup | 文档查询 |
| harness-optimizer | 配置优化 |

## 可用命令

- `/plan` — 创建实现计划
- `/tdd` — TDD 工作流
- `/code-review` — 代码审查
- `/security` — 安全审查
- `/build-fix` — 修复构建错误
- `/refactor-clean` — 清理死代码
- `/update-docs` — 更新文档
- `/update-codemaps` — 更新 codemap
- `/test-coverage` — 测试覆盖率分析
- `/go-review` — Go 代码审查
- `/go-test` — Go TDD
- `/go-build` — Go 构建修复
- `/verify` — 验证循环
- `/checkpoint` — 保存进度
