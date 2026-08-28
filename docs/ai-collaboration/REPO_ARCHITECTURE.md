# 仓库文档架构

## 推荐结构

```text
project/
├── AGENTS.md
├── README.md
├── docs/
│   ├── PRODUCT.md
│   ├── ARCHITECTURE.md
│   ├── DECISIONS.md
│   ├── ROADMAP.md
│   └── ai-collaboration/
│       ├── README.md
│       ├── WORKFLOW.md
│       ├── REPO_ARCHITECTURE.md
│       ├── MASTER_PROMPT.md
│       ├── CHATGPT_START_PROMPT.md
│       └── CODEX_START_PROMPT.md
├── tasks/
│   ├── 001-example.md
│   ├── 002-example.md
│   └── TASK.template.md
├── src/
├── tests/
└── ...
```

## 信息架构原则

### 仓库保存当前事实

聊天历史可以解释讨论过程，但不能作为唯一项目记忆。新会话、ChatGPT、Codex 和人类协作者应能仅通过仓库恢复：

- 项目为何存在
- 当前范围是什么
- 系统怎样组织
- 为什么做过重要选择
- 当前阶段在哪里
- 下一项工作如何验收

### 一个事实，一个权威位置

不要在多个文件完整复制同一规则。例如 MVP 功能边界以 `PRODUCT.md` 为准，Task 只引用与当前工作相关的部分；模块依赖以 `ARCHITECTURE.md` 为准，`AGENTS.md` 只说明执行时必须遵守它。

### 当前状态与历史理由分离

- `ARCHITECTURE.md` 描述当前有效架构
- `DECISIONS.md` 保存选择过程、替代方案和历史理由

架构改变后，更新当前架构，并把旧 Decision 标为 `Superseded`；不要让两套架构都看起来有效。

## 各文件契约

### `AGENTS.md`

目标读者：Codex、AI Agent 和新加入的执行者。

必须简短回答：

- 开始工作前读什么
- 常用构建、测试、运行命令是什么
- 哪些目录或接口有特殊约束
- 怎样控制 Scope
- 怎样验证和汇报
- 何时更新文档

不应包含：长篇产品故事、所有历史决定、某一个 Task 的详细需求。

### `docs/PRODUCT.md`

目标读者：产品、设计、工程和 AI。

权威内容：产品定义、目标用户、JTBD、核心场景、体验原则、成功指标、MVP Scope、Non-goals。

更新触发：用户、问题、范围、体验原则或成功定义发生稳定变化。

### `docs/ARCHITECTURE.md`

目标读者：工程、架构 Review 和执行 Agent。

权威内容：系统上下文、技术栈、模块边界、依赖方向、数据流、接口、数据模型、平台集成、安全、可观测性、部署和已知限制。

更新触发：系统结构或技术边界发生稳定变化。

### `docs/DECISIONS.md`

目标读者：未来会问“为什么不选另一种方案”的人和 AI。

权威内容：重要决定的背景、选择、理由、替代方案、后果和重审条件。

更新触发：出现成本较高、影响长期或容易被反复讨论的取舍。

### `docs/ROADMAP.md`

目标读者：项目负责人和跨阶段协作者。

权威内容：阶段目标、可交付 Outcome、依赖、Exit Criteria 和当前状态。

更新触发：阶段边界、顺序、依赖或目标变化。细碎 Todo 应放到 Task 或 Issue。

### `tasks/*.md`

目标读者：单次执行工作的实现者和 Reviewer。

权威内容：本次 Goal、Context、Requirements、Constraints、Non-goals、Acceptance Criteria、Verification、Deliverables。

更新触发：任务执行前需要澄清合同；执行中如前提发生变化，先更新 Task 并说明，而不是静默改变目标。

### `docs/ai-collaboration/`

目标读者：ChatGPT、Codex / Work、项目负责人和未来维护者。

权威内容：通用协作流程、文档信息架构和启动 Prompt。

这些文件解释“如何协作”，不保存某个项目的产品、架构或当前进度。日常工作先读根 `AGENTS.md`，只有需要详细规则时才进入本目录。

## 文档依赖关系

```text
PRODUCT ────────┐
                ├──→ ROADMAP ──→ TASK ──→ CODE / TEST / EVIDENCE
ARCHITECTURE ───┤
                │
DECISIONS ──────┘

AGENTS ──→ 约束所有读取、执行、验证和汇报方式
```

依赖方向应尽量单向：Task 引用长期文档，长期文档不依赖某个临时 Task 才能成立。

## 文档状态约定

推荐使用以下状态：

- `Draft`：正在形成，不能默认当作执行要求
- `Active`：当前有效
- `Superseded`：已被新决定替代，保留供追溯
- `Deprecated`：仍可能存在，但不应新增使用
- `Completed`：Task 或 Roadmap Phase 已完成
- `Blocked`：存在已明确的外部阻塞

每个长期文档顶部可记录：

```text
Status: Active
Last Updated: YYYY-MM-DD
Owner: [人或团队]
```

不要为了形式而频繁改日期；只有内容变化时更新。

## Decision ID 与 Task ID

推荐简单、稳定、易搜索的编号：

```text
DEC-001-use-postgresql
DEC-002-desktop-runtime

tasks/001-initialize-repository.md
tasks/002-implement-login.md
```

Decision 被替代时保留原 ID，并链接到替代它的新 ID。Task 不复用已使用编号。

## 分支与 PR 建议

对需要 Review 的项目：

```text
task/002-implement-login
```

PR 描述引用：

- Task 路径
- 相关 Decision
- Acceptance Criteria 结果
- Verification evidence
- 已知限制或 Follow-ups

一个 PR 最好对应一个 Task。若实现发现需要改变产品或架构方向，先回到 Decision / Task 更新，而不是在 Diff 中隐式决定。

## 最小化变体

### 小型原型

```text
AGENTS.md
docs/PRODUCT.md
tasks/001-prototype.md
```

### 中长期产品

使用完整结构，并通过 PR 维护文档和实现。

### 多组件仓库

根 `AGENTS.md` 维护全局规则；只有子目录确实需要不同命令或约束时才新增局部 `AGENTS.md`。局部规则不得与根规则含糊冲突。
