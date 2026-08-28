# `[PROJECT_NAME]`

`[用一句话说明项目为谁解决什么问题。]`

- Status: `Draft`
- Current Phase: `[CURRENT_PHASE]`
- Owner: `[OWNER]`

## 项目目标

`[说明项目的核心目标、预期用户结果和当前边界。未知内容保留为 TBD。]`

## 快速开始

这是一个可直接复制使用的 ChatGPT → GitHub → Codex / Work 项目骨架。

1. 将整个目录复制并重命名为新项目。
2. 替换 `AGENTS.md`、本文件和 `docs/` 中已知的项目占位符；未知内容保留为 `TBD`。
3. 初始化 Git 仓库并推送到 GitHub。
4. 在 ChatGPT 中连接 GitHub，并先要求它读取 `AGENTS.md`。
5. 使用 ChatGPT 探索与沉淀稳定决定，使用 Task 固定执行范围，再由 Codex / Work 实现和验证。

建议给 ChatGPT 的第一条短指令见：

- `docs/ai-collaboration/CHATGPT_START_PROMPT.md`

## 项目事实

| 文档 | 作用 |
| --- | --- |
| `AGENTS.md` | AI 总协作规范、阅读顺序、写入规则和执行约束 |
| `docs/PRODUCT.md` | 产品、用户、范围、体验原则和成功定义 |
| `docs/ARCHITECTURE.md` | 当前技术栈、系统结构、模块、接口和数据流 |
| `docs/DECISIONS.md` | 重要选择、理由、替代方案、后果和重审条件 |
| `docs/ROADMAP.md` | 阶段目标、依赖、状态和退出条件 |
| `tasks/*.md` | 单次执行工作的范围、验收标准和验证方式 |

## 协作说明

通用协作方法集中存放在 `docs/ai-collaboration/`：

- `README.md`：协作入口与使用方式
- `WORKFLOW.md`：从讨论到验证的完整流程
- `REPO_ARCHITECTURE.md`：仓库文档信息架构
- `MASTER_PROMPT.md`：ChatGPT 完整协作协议
- `CHATGPT_START_PROMPT.md`：ChatGPT 短启动指令
- `CODEX_START_PROMPT.md`：Codex 实现、Review 与修复指令

## 开发

```text
Install:        [INSTALL_COMMAND]
Development:    [DEV_COMMAND]
Build:          [BUILD_COMMAND]
Test:           [TEST_COMMAND]
```

详细技术说明见 `docs/ARCHITECTURE.md`。
