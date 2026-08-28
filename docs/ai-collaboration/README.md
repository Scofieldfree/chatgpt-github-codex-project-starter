# AI 项目协作说明

本目录保存 ChatGPT、GitHub 与 Codex / Work 的通用协作方法。项目本身的当前事实不写在这里，而是分别维护在根 `AGENTS.md`、`docs/*.md` 和 `tasks/*.md` 中。

## 入口关系

```text
AGENTS.md
├── 规定必须遵守的总协作规范
├── 指向 docs/ 中的项目事实
└── 按需引用本目录的详细流程
```

AI 开始工作时应先读根目录 `AGENTS.md`，不需要每次完整读取本目录所有文件。

## 本目录文件

| 文件 | 用途 |
| --- | --- |
| `WORKFLOW.md` | 从探索、文档沉淀、Task、实现到 Review 的完整闭环 |
| `REPO_ARCHITECTURE.md` | 各文档的权威职责、依赖关系和维护原则 |
| `MASTER_PROMPT.md` | ChatGPT 的详细讨论、决策、文档和 Review 协议 |
| `CHATGPT_START_PROMPT.md` | 新 ChatGPT 会话的短启动指令 |
| `CODEX_START_PROMPT.md` | Codex 实现、Review 和修复的启动指令 |

## 推荐使用方式

### 新项目初始化

1. 复制整个项目骨架并重命名。
2. 在根 `README.md`、`AGENTS.md` 和 `docs/` 中填写已经确认的项目信息。
3. 未知内容保留为 `TBD`，不要为了完成模板而编造。
4. 初始化 Git 并推送到 GitHub，让仓库成为长期项目记忆。

### ChatGPT 讨论与文档维护

1. 在 ChatGPT 中连接 GitHub 仓库。
2. 使用 `CHATGPT_START_PROMPT.md` 的短指令，明确要求先读取根 `AGENTS.md`。
3. 探索阶段只讨论和澄清，不把假设写成正式决定。
4. 用户确认后，ChatGPT 按 `AGENTS.md` 的信息路由更新对应项目文档。
5. 准备执行时，从 `tasks/TASK.template.md` 创建一个小型、可验证的 Task。

### Codex / Work 执行

1. 使用 `CODEX_START_PROMPT.md`，指定唯一的 Task 路径。
2. Codex 读取根 `AGENTS.md`、Task、相关项目文档和实际代码。
3. Codex 实现、测试、运行真实验证并汇报证据。
4. ChatGPT 或 Reviewer 根据 Task、Diff 和证据判断 PASS、FIX REQUIRED 或 RE-SCOPE。

## 权限边界

GitHub 中的仓库文件是共享上下文。普通 ChatGPT GitHub 连接主要用于读取、搜索和分析仓库；实际文件修改和 Git 操作需要由具备写入能力的 ChatGPT Work / Codex 环境或人工完成。

无论使用哪种执行环境，都必须遵守根 `AGENTS.md` 和用户授予的权限范围。
