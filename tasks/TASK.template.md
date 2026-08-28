# Task `[NNN]`: `[TASK_TITLE]`

- Status: `Draft`
- Owner: `[OWNER_OR_CODEX]`
- Created: `[YYYY-MM-DD]`
- Roadmap Phase: `[PHASE]`
- Related Decisions: `[DEC-XXX_OR_NONE]`
- Depends On: `[TASK_OR_NONE]`

## Goal

`[用一两句话描述本任务完成后产生的单一结果。]`

## Context

`[说明为什么现在做、与用户价值和现有实现的关系。只放理解任务必需的上下文，并链接长期文档。]`

Relevant references:

- `docs/PRODUCT.md#[SECTION]`
- `docs/ARCHITECTURE.md#[SECTION]`
- `docs/DECISIONS.md#[DECISION]`
- `[RELEVANT_CODE_OR_DESIGN]`

## Current Behavior

`[当前系统实际怎样工作；新项目可写 Not implemented。]`

## Requirements

1. `[MUST_HAVE_BEHAVIOR]`
2. `[MUST_HAVE_BEHAVIOR]`
3. `[ERROR_OR_EDGE_BEHAVIOR]`

使用可观察行为描述需求。确实需要固定接口或实现边界时才写内部细节。

## Architecture Constraints

- `[必须遵守的模块边界、接口、依赖方向或平台限制。]`
- `[需要保持的兼容性或数据约束。]`
- `[安全、隐私或性能边界。]`

## Allowed Change Surface

- `[DIRECTORY_OR_MODULE]`
- `[DIRECTORY_OR_MODULE]`

这不是绝对白名单；如果完成 Task 必须修改其他位置，保持最小并在报告中解释。

## Non-goals

- `[EXPLICITLY_EXCLUDED_FEATURE_OR_REFACTOR]`
- `[FOLLOW_UP_NOT_INCLUDED]`

## Acceptance Criteria

- [ ] **AC1** — Given `[PRECONDITION]`, when `[ACTION]`, then `[OBSERVABLE_RESULT]`.
- [ ] **AC2** — Given `[EDGE_OR_FAILURE_CONDITION]`, when `[ACTION]`, then `[EXPECTED_BEHAVIOR]`.
- [ ] **AC3** — Existing `[RELATED_BEHAVIOR]` continues to work.
- [ ] **AC4** — Required tests and verification complete without unexplained failures.

每条标准必须能明确判定 PASS / FAIL，避免“体验良好”“代码干净”“基本支持”等模糊表达。

## Verification

### Automated

```text
[LINT_OR_STATIC_CHECK]
[TARGET_TEST_COMMAND]
[INTEGRATION_OR_E2E_COMMAND]
```

Expected evidence:

- `[EXPECTED_TEST_OR_OUTPUT]`

### Real Behavior / Manual

1. `[SETUP]`
2. `[ACTION]`
3. `[OBSERVE]`
4. `[EXPECTED_RESULT]`

Evidence to retain:

- `[SCREENSHOT / LOG / OUTPUT / RECORD / TEST RESULT]`

### Regression Checks

- `[RELATED_EXISTING_PATH]`

## Deliverables

- `[CODE_OR_BEHAVIOR]`
- `[TESTS]`
- `[DOCUMENTATION_IF_FACTS_CHANGED]`
- `[EVIDENCE]`

## Risks and Rollback

- Risk: `[RISK]`
- Mitigation: `[MITIGATION]`
- Rollback: `[HOW_TO_REVERSE_IF_NEEDED]`

对低风险任务可以写 `No special rollback beyond reverting this isolated change`。

## Out-of-scope Follow-ups

- `[DISCOVERED_OR_EXPECTED_FOLLOW_UP]`

执行期间只记录，不自动纳入当前 Task。

## Completion Report

执行者完成后填写或在最终回复中提供：

### Outcome

`[PASS / FIX REQUIRED / BLOCKED / RE-SCOPE]`

### Changes

- `[KEY_CHANGE]`

### Acceptance Criteria Results

| Criterion | Result | Evidence |
| --- | --- | --- |
| AC1 | `[PASS/FAIL/NOT VERIFIED]` | `[EVIDENCE]` |

### Verification Results

- `[COMMAND_OR_PATH]` → `[RESULT]`

### Remaining Issues

- `[ISSUE_OR_NONE]`

### Documentation Updates

- `[FILE_AND_REASON_OR_NO_PROJECT_FACT_CHANGES]`

