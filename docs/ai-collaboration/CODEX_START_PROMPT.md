# Codex / Work 启动 Prompt

## 默认短版

替换任务路径后直接使用：

```text
Read AGENTS.md first.
Then read the relevant project documents and inspect the existing implementation.

Implement:
tasks/XXX-task-name.md

Follow the current architecture and settled decisions.
Do not expand scope beyond the task.

After implementation:
1. run every required verification,
2. fix in-scope failures,
3. report what changed,
4. map results to each acceptance criterion,
5. provide verification evidence,
6. report unresolved issues and out-of-scope follow-ups,
7. update documentation only if current project facts changed or a genuinely new decision was introduced.
```

## 中文版

```text
先阅读 AGENTS.md，再阅读与本任务相关的项目文档并检查现有实现。

执行：
tasks/XXX-task-name.md

遵守当前架构和已经确认的决定，不要扩大任务范围。

完成实现后：
1. 执行 Task 要求的全部验证；
2. 修复本次范围内的失败；
3. 汇报关键变更；
4. 逐条对应 Acceptance Criteria 给出结果；
5. 提供验证证据；
6. 说明未解决问题和范围外 Follow-ups；
7. 只有当前项目事实发生变化或出现真正的新决定时才更新长期文档。
```

## Review 版

用于让 Codex / Work 检查已有实现或 PR：

```text
Read AGENTS.md, the referenced task, relevant project documents, and the actual diff.

Review the implementation against every acceptance criterion.
Check scope, architecture consistency, regressions, security-relevant behavior, and verification quality.

Do not rely only on the implementation summary.
Run safe, relevant verification when available.

Report:
1. blocking findings first,
2. acceptance criteria status,
3. verification performed and evidence,
4. non-blocking follow-ups,
5. whether the task is PASS, FIX REQUIRED, or RE-SCOPE.
```

## Fix 版

用于修复 Review 中已经明确的问题：

```text
Read AGENTS.md, the original task, and the review findings.

Fix only the blocking findings that are within the original task scope.
Preserve unrelated user changes and do not perform opportunistic refactors.

Re-run the relevant verification and report the evidence.
If a finding requires a product or architecture decision beyond the task, stop that part and report it as RE-SCOPE instead of guessing.
```

## 使用原则

- 启动 Prompt 保持短小；项目事实应放在仓库文档中。
- 一次只指定一个主要 Task。
- 不要在启动 Prompt 里临时覆盖已确认架构；需要改变时先更新 Decision 和 Task。
- 需要截图、设备、账号或人工检查时，在 Task 的 Verification 中明确写出。
- 对高风险操作，在 Task 中写明权限、目标和回退方式。

