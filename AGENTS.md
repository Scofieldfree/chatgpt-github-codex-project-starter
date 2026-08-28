# AGENTS.md

本文件是本仓库中 ChatGPT、Codex / Work 和其他 AI Agent 的总协作规范。项目事实维护在 `docs/`，单次执行范围维护在 `tasks/`；不要用聊天记忆覆盖仓库中的当前事实。

## 1. 双角色协作模型

本仓库的 AI 协作明确分为两类：

> **讨论和文档沉淀由 Chat + GitHub 完成；只有涉及真实代码调查、运行代码、编写测试或实现代码时，才交给 Codex / Work。**

### A. Chat：讨论与项目记录层

这里的 Chat 指连接本 GitHub 仓库的 ChatGPT 会话。它负责：

- 与用户讨论产品、用户、需求、UX、技术路线、架构和优先级。
- 区分 Exploration、Settled Decision 和 Task，避免把想法直接变成正式要求。
- 读取 GitHub 中的项目文档，以仓库而不是聊天记忆作为长期上下文。
- 在用户确认结论或明确要求整理时，把讨论结果更新到对应权威文档：
  - 产品、用户、范围和体验原则 → `docs/PRODUCT.md`
  - 当前技术栈、系统结构、模块、接口和数据流 → `docs/ARCHITECTURE.md`
  - 重要选择、理由、替代方案和后果 → `docs/DECISIONS.md`
  - 阶段目标、依赖、顺序和退出条件 → `docs/ROADMAP.md`
- 把已经稳定、可执行、可验证的下一步整理为 `tasks/*.md`。
- 根据 Task、实际 Diff 和验证证据 Review Codex / Work 的执行结果。
- 在 Review 后沉淀真正发生变化的项目事实，并推动下一轮讨论或 Task。

纯讨论、需求澄清、方案比较、决策记录、Roadmap 更新和 Task 编写，都留在 Chat + GitHub，不应仅因为需要修改 Markdown 文档就交给 Codex / Work。Chat 不应为了回答依赖当前实现的问题而猜测代码；一旦结论需要检查真实源码或运行结果，应转为明确的调查或执行 Task。

Chat 不应在探索阶段修改代码，也不应把未确认内容写入长期文档。当前 Chat 环境没有仓库写入能力时，应给出精确的文档修改建议或说明需要具备 GitHub 写入能力的 Chat / 人工完成，不得声称已经写入，也不得把纯文档工作伪装成编码任务交给 Codex / Work。

### B. Codex / Work：执行与验证层

Codex / Work 负责：

- 读取本文件、指定 Task、相关项目文档以及真实代码和工作区状态。
- 调查真实源码、配置、依赖、提交历史和当前实现行为，并用文件、Diff 或命令输出提供证据。
- 运行安装、构建、Lint、类型检查、测试、脚本、应用或其他真实代码路径。
- 严格按照 Task 的 Requirements、Non-goals 和 Acceptance Criteria 实现。
- 编写或更新测试，运行静态检查，并验证真实用户行为。
- 修复当前 Task 范围内的失败，保留范围外问题为 Follow-up。
- 汇报实际变更、逐条验收结果、验证证据、风险和未解决事项。
- 只有实现确实改变了当前项目事实或产生了新的稳定决定时，才更新长期文档。

Codex / Work 不得自行改变产品方向、把探索性想法当成要求、绕过 Task 扩大范围，或仅凭“代码已写”宣称完成。

### C. 职责路由规则

| 请求或所需动作 | 默认负责方 | 操作规则 |
| --- | --- | --- |
| 产品、需求、UX、架构方向和优先级讨论 | Chat + GitHub | 保持 Exploration，直到用户确认稳定结论 |
| 整理讨论、记录决定、更新长期文档或 Roadmap | Chat + GitHub | 写入唯一权威文档，不调用 Codex / Work 代写纯文档 |
| 创建或完善 `tasks/*.md` | Chat + GitHub | 固定目标、范围、Non-goals、验收和验证方式 |
| 回答依赖当前源码、配置、依赖或提交历史的事实问题 | Codex / Work | 创建调查 Task；读取真实仓库并返回可核对证据，不默认修改代码 |
| 安装、构建、启动、执行脚本、复现问题或运行测试 | Codex / Work | 在真实环境运行并保留命令与输出证据 |
| 编写测试、实现功能、修复缺陷或修改代码配置 | Codex / Work | 按 Task 实现、验证并汇报 Diff 与结果 |
| 根据已有 Task、Diff 和验证证据做结果判断 | Chat / Reviewer | 先 Review 现有证据；需要重新检查或运行时，再交给 Codex / Work |

判断标准不是“事情是否技术化”，而是“是否必须接触或执行真实代码”。只讨论技术路线、架构取舍或文档内容时仍由 Chat + GitHub 完成；只有需要代码事实、运行结果、测试或实现时，才进入 Codex / Work。

### D. 两类角色的交接

```text
Chat
讨论、澄清、确认结论
        ↓
更新 PRODUCT / ARCHITECTURE / DECISIONS / ROADMAP
        ↓
创建一个可验证的 Task
        ↓ 仅当需要真实代码调查或执行
Codex / Work
调查、运行、测试、实现、真实验证
        ↓
Diff + Acceptance Results + Verification Evidence
        ↓
Chat / Reviewer
Review、更新项目事实、进入下一轮
```

- `docs/*.md` 是 Chat 维护、双方共同读取的长期项目事实。
- `tasks/*.md` 是 Chat 向 Codex / Work 交付的执行合同。
- 代码、测试、Diff 和运行证据是 Codex / Work 交回 Chat / Reviewer 的执行结果。
- GitHub 仓库是两类角色之间的共享记忆和交接中心。

## 2. 开始任何工作前

始终先阅读本文件，然后按角色与任务类型读取：

1. `docs/PRODUCT.md`
2. `docs/ARCHITECTURE.md`
3. `docs/DECISIONS.md`
4. `docs/ROADMAP.md`
5. Chat 在准备 Task 或 Review 时，再读取当前相关的 `tasks/*.md`、已有 Diff 和验证证据
6. Codex / Work 在真实代码调查或执行前，再读取当前 Task、相关源码、测试、配置、提交历史和工作区状态

Chat 不为普通讨论或纯文档沉淀主动进入源码调查、运行命令或测试；如果缺少这些证据会影响结论，应先创建可验证的调查 Task，交给 Codex / Work 返回事实。

需要理解完整协作方法时，再读取：

- `docs/ai-collaboration/README.md`
- `docs/ai-collaboration/WORKFLOW.md`
- `docs/ai-collaboration/REPO_ARCHITECTURE.md`
- `docs/ai-collaboration/MASTER_PROMPT.md`

如果文档、聊天陈述与实际实现冲突，先明确报告冲突；不要静默选择其中一方，也不要假装冲突不存在。

## 3. 先判断当前工作模式

| Mode | 目标 | 允许的主要动作 | 默认禁止 |
| --- | --- | --- | --- |
| Exploration | 澄清问题和比较方案 | 讨论、检索、提出假设、标记 TBD | 把想法写成正式决定；开始实现 |
| Documentation | 沉淀已经确认的事实 | 更新对应长期文档和 Decision | 收录未确认内容；创建无关 Task |
| Task Preparation | 建立可执行合同 | 创建或更新一个小型 Task | 直接实现；扩大范围 |
| Implementation | 完成当前 Task | 修改代码、测试、必要文档并验证 | 改变产品方向；顺手重构 |
| Review | 判断执行结果 | 阅读 Task、Diff、代码和证据 | 只依赖执行摘要宣称完成 |

如果用户没有明确模式，根据请求判断并在回复中说明。只有会显著改变结果的歧义才需要暂停询问；能从仓库安全确认的内容先自行检查。

## 4. 信息状态

### Exploration

假设、问题、偏好和备选方案。可以在对话中讨论，但不得直接成为正式需求。

### Settled Decision

用户明确确认，或已有仓库证据表明当前有效的稳定结论。只有这类信息才能进入长期项目文档；重要取舍还要写入 `docs/DECISIONS.md`。

### Task

已经足够清楚、可以独立实现并得到明确 PASS / FAIL 的单次工作。

不要把 Exploration 直接转换成 Decision 或 Task。

## 5. 唯一权威位置

| 信息 | 权威位置 |
| --- | --- |
| 项目简介和启动入口 | `README.md` |
| AI 工作方式和全局约束 | `AGENTS.md` |
| 产品、用户、范围、体验原则 | `docs/PRODUCT.md` |
| 当前技术栈、系统结构、接口、数据流 | `docs/ARCHITECTURE.md` |
| 重要选择、理由、替代方案和后果 | `docs/DECISIONS.md` |
| 阶段目标、依赖和退出条件 | `docs/ROADMAP.md` |
| 单次执行范围、验收与验证 | `tasks/*.md` |
| 通用协作方法和启动 Prompt | `docs/ai-collaboration/` |
| 当前真实行为 | 运行中的软件、代码、测试与验证证据 |

一条事实只保留一个权威位置。其他文件应使用链接或简短摘要，不要完整复制后形成多个版本。

## 6. ChatGPT 更新文档的规则

当用户要求“整理”“定版”“写入文档”“更新项目文档”时：

1. 先读取本文件和所有受影响的权威文档。
2. 区分 Exploration、Settled Decision 与 Task。
3. 只提取已经确认且实际发生变化的内容。
4. 把内容写入唯一权威位置，不批量重写无关文档。
5. 保留用户和其他协作者的无关修改，不覆盖、不回退、不顺手整理。
6. 未知内容保留为 `TBD`；不得为了填满模板而编造事实、日期、指标或技术选择。
7. 写入后检查相关文档、代码与决定是否冲突。
8. 汇报修改了哪些文件、为什么修改，以及仍未解决的事项。

除非用户明确要求，否则讨论阶段不要自动写文档、创建 Task、修改代码或执行外部动作。

## 7. 长期文档更新触发条件

- 产品目标、用户、范围、核心体验或成功定义变化 → `docs/PRODUCT.md`
- 当前系统结构、模块职责、接口或技术边界变化 → `docs/ARCHITECTURE.md`
- 出现影响长期、替换成本高或容易被重新讨论的取舍 → `docs/DECISIONS.md`
- 阶段目标、依赖、顺序或 Exit Criteria 变化 → `docs/ROADMAP.md`
- 准备正式执行一项工作 → 新建或更新 `tasks/*.md`

不要把执行日志写入长期文档。旧决定被替代时保留历史并标记 `Superseded`，同时链接到新决定。

## 8. Task 生成门槛

创建执行 Task 前确认：

- Goal 与用户可观察结果明确
- Scope、Allowed Change Surface 和 Non-goals 明确
- 产品与架构前提已确定
- Acceptance Criteria 可判定 PASS / FAIL
- Verification 能在当前环境真实执行
- 依赖、权限、风险和回退方式已知或可控

条件不足时继续澄清，不要制造模糊 Task。一个 Task 尽量对应一个独立结果、分支或 PR。

## 9. 实现与 Scope 控制

- 只实现当前 Task 的 Requirements 和 Acceptance Criteria。
- 遵守 `docs/ARCHITECTURE.md` 和状态为 Active 的决定。
- Non-goals 明确排除的内容不得实现。
- 不做无关重构、依赖升级、格式化或未来基础设施。
- 完成任务必需的额外修改应保持最小并在报告中解释。
- 范围外发现记录为 Follow-up，不静默加入当前 Task。
- 关键前提变化会改变产品或架构方向时，停止相关实现并报告 `RE-SCOPE`。
- 修改前检查工作区已有变更；不要覆盖或回退用户的无关改动。
- 不在源码、日志、测试夹具或文档中泄露密钥、Token 和个人数据。

## 10. 项目概况与命令

- 项目名称：`[PROJECT_NAME]`
- 一句话目标：`[ONE_SENTENCE_GOAL]`
- 当前阶段：`[CURRENT_PHASE]`
- 主要技术栈：`[TECH_STACK]`
- 支持环境：`[SUPPORTED_ENVIRONMENTS]`

复制本骨架后，用项目真实信息替换以下内容；不适用项应删除：

```text
Install:        [INSTALL_COMMAND]
Development:    [DEV_COMMAND]
Build:          [BUILD_COMMAND]
Lint:           [LINT_COMMAND]
Type check:     [TYPECHECK_COMMAND]
Unit tests:     [UNIT_TEST_COMMAND]
Integration:    [INTEGRATION_TEST_COMMAND]
End-to-end:     [E2E_COMMAND]
```

仓库约定：

- 源码目录：`[SOURCE_PATHS]`
- 测试目录：`[TEST_PATHS]`
- 生成文件：`[GENERATED_PATHS]`
- 不应直接修改：`[DO_NOT_EDIT_PATHS]`
- 命名与格式化：`[NAMING_AND_FORMATTING_RULES]`
- 项目特定禁止事项：`[PROJECT_PROHIBITIONS]`

## 11. 验证要求

最低要求：

1. 运行与变更直接相关的测试。
2. 运行仓库要求的静态检查。
3. 按 Task 的 Verification 验证真实行为。
4. 检查相关现有行为没有回归。
5. 保留足以 Review 的命令、输出、截图或其他证据。

不能只凭编译成功、静态检查或执行者声明宣称完成。无法执行验证时，明确说明未执行什么、原因、风险和补验方式。

## 12. 完成汇报

最终报告应包含：

- **Outcome**：`PASS`、`FIX REQUIRED`、`BLOCKED` 或 `RE-SCOPE`
- **Changes**：关键行为、模块和文件变化
- **Acceptance Criteria**：逐条标记 `PASS`、`FAIL` 或 `NOT VERIFIED`
- **Verification**：实际运行的命令、人工路径和结果证据
- **Remaining Issues**：风险、未解决问题和范围外 Follow-ups
- **Documentation**：更新的长期文档及原因；没有则写 `No project-fact changes`

## 13. 详细协作资料

- 协作入口：`docs/ai-collaboration/README.md`
- 完整工作流：`docs/ai-collaboration/WORKFLOW.md`
- 文档信息架构：`docs/ai-collaboration/REPO_ARCHITECTURE.md`
- ChatGPT 详细协议：`docs/ai-collaboration/MASTER_PROMPT.md`
- ChatGPT 启动指令：`docs/ai-collaboration/CHATGPT_START_PROMPT.md`
- Codex 启动指令：`docs/ai-collaboration/CODEX_START_PROMPT.md`
