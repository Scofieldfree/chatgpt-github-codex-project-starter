# Task 001: 添加服务健康检查接口

> 本文件是一个填写完成的示例 Task,展示每个字段的期望粒度。启动真实项目时删除本文件,从 `TASK.template.md` 创建你的 001。

- Status: `Ready`
- Owner: `Codex`
- Created: `2026-08-28`
- Roadmap Phase: `Phase 0 — Foundation`
- Related Decisions: `None`
- Depends On: `None`

## Goal

后端服务暴露 `GET /health` 接口,返回服务运行状态,供部署平台和监控探活使用。

## Context

部署平台需要一个稳定的探活地址判断服务是否就绪;当前服务没有任何可探测端点,导致滚动发布时无法自动判断新实例是否可用。本任务只解决探活,不涉及依赖项(数据库、缓存)的深度健康诊断。

Relevant references:

- `docs/ARCHITECTURE.md#接口`
- `src/server/routes/`(现有路由注册方式)

## Current Behavior

服务无 `/health` 路由,请求返回 404。

## Requirements

1. `GET /health` 返回 HTTP 200,响应体为 JSON:`{"status":"ok","version":"<当前应用版本>"}`。
2. 接口不要求认证,不读取数据库,响应时间应稳定在毫秒级。
3. 未知路径的现有 404 行为保持不变。

## Architecture Constraints

- 路由必须通过现有路由注册机制挂载,不引入新的 Web 框架或中间件。
- 版本号从现有构建元数据读取,不硬编码。
- 不新增任何外部依赖。

## Allowed Change Surface

- `src/server/routes/`
- `tests/server/`

这不是绝对白名单;如果完成 Task 必须修改其他位置,保持最小并在报告中解释。

## Non-goals

- 不实现依赖项深度检查(数据库、缓存连通性)。
- 不实现 `/metrics` 或任何监控指标输出。
- 不调整现有日志或中间件。

## Acceptance Criteria

- [ ] **AC1** — Given 服务已启动, when 请求 `GET /health`, then 返回 200 且响应体包含 `status: "ok"` 和非空 `version` 字段。
- [ ] **AC2** — Given 服务已启动, when 请求 `GET /health-unknown` 等未注册路径, then 仍返回 404。
- [ ] **AC3** — 现有全部路由行为不变,既有测试全部通过。
- [ ] **AC4** — 新增测试覆盖 AC1 与 AC2,运行无未解释失败。

## Verification

### Automated

```text
npm run lint
npm test -- tests/server/health.test.ts
npm test
```

Expected evidence:

- 新增 health 测试通过的输出
- 全量测试套件通过的输出

### Real Behavior / Manual

1. 本地启动服务:`npm run dev`。
2. 执行 `curl -i http://localhost:3000/health`。
3. 观察响应状态码与 JSON 内容。
4. 预期:HTTP 200,响应体 `{"status":"ok","version":"x.y.z"}`。

Evidence to retain:

- curl 输出(状态码 + 响应体)

### Regression Checks

- 现有任一业务路由(如 `GET /api/...`)仍正常响应。

## Deliverables

- `/health` 路由实现
- 对应自动化测试
- 无需文档更新(不改变产品事实)
- curl 输出与测试结果证据

## Risks and Rollback

- Risk: 无认证端点被滥用扫描。
- Mitigation: 接口不暴露内部信息,仅返回状态与版本。
- Rollback: No special rollback beyond reverting this isolated change.

## Out-of-scope Follow-ups

- 依赖项深度健康检查(数据库/缓存)可作为后续 Task。

## Completion Report

执行者完成后填写或在最终回复中提供:

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
