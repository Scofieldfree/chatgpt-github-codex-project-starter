# Architecture

Status: Draft  
Last Updated: `[YYYY-MM-DD]`  
Owner: `[OWNER]`

本文件描述当前有效架构。历史理由和被替代方案记录在 `DECISIONS.md`。

## 1. Architecture Goals

- `[GOAL_1]`
- `[GOAL_2]`

### Non-goals

- `[ARCHITECTURE_NON_GOAL]`

## 2. System Context

```text
[USER / EXTERNAL_SYSTEM]
        ↓
[OUR_SYSTEM]
        ↓
[DEPENDENCY / DATA STORE / PLATFORM]
```

### System Boundary

- 系统负责：`[RESPONSIBILITIES]`
- 系统不负责：`[EXCLUSIONS]`
- 外部依赖：`[DEPENDENCIES]`

## 3. Tech Stack

| Area | Choice | Version / Constraint | Decision |
| --- | --- | --- | --- |
| Runtime | `[CHOICE]` | `[VERSION]` | `[DEC-XXX]` |
| UI | `[CHOICE]` | `[VERSION]` | `[DEC-XXX]` |
| Storage | `[CHOICE]` | `[VERSION]` | `[DEC-XXX]` |
| Testing | `[CHOICE]` | `[VERSION]` | `[DEC-XXX]` |

只列当前采用的技术。候选方案放入 Decision 或 Open Questions。

## 4. Runtime / Process Model

```text
[PROCESS_A] ──[IPC/API]──> [PROCESS_B]
     │                         │
     └──────> [STORAGE] <──────┘
```

- 生命周期：`[STARTUP_SHUTDOWN]`
- 并发模型：`[CONCURRENCY]`
- 失败隔离：`[FAILURE_BOUNDARIES]`

## 5. Module Boundaries

| Module | Responsibility | Owns | May Depend On | Must Not Depend On |
| --- | --- | --- | --- | --- |
| `[MODULE]` | `[RESPONSIBILITY]` | `[DATA_OR_BEHAVIOR]` | `[ALLOWED]` | `[FORBIDDEN]` |

### Dependency Direction

```text
[OUTER / ADAPTER] → [APPLICATION] → [DOMAIN / CORE]
```

`[补充必须遵守的依赖规则。]`

## 6. Key Data Flows

### `[FLOW_NAME]`

```text
1. [SOURCE]
2. [VALIDATION / TRANSFORMATION]
3. [CORE OPERATION]
4. [PERSISTENCE / OUTPUT]
5. [OBSERVABLE RESULT]
```

失败路径：`[FAILURE_HANDLING]`

## 7. Interfaces and Contracts

### `[API / IPC / EVENT]`

- Producer / Caller：`[OWNER]`
- Consumer：`[CONSUMER]`
- Input：`[SCHEMA_OR_LINK]`
- Output：`[SCHEMA_OR_LINK]`
- Errors：`[ERROR_CONTRACT]`
- Compatibility：`[VERSIONING_RULE]`

## 8. Data Model and Storage

- 权威数据源：`[SOURCE_OF_TRUTH]`
- 数据模型：`[MODEL_OR_LINK]`
- 持久化策略：`[PERSISTENCE]`
- Migration：`[MIGRATION_POLICY]`
- Retention：`[RETENTION]`
- 敏感数据：`[SENSITIVE_DATA_HANDLING]`

## 9. Platform and External Integration

| Integration | Purpose | Auth / Permission | Failure Behavior |
| --- | --- | --- | --- |
| `[SYSTEM]` | `[PURPOSE]` | `[AUTH]` | `[DEGRADATION]` |

## 10. Security and Privacy Boundaries

- Trust boundaries：`[BOUNDARIES]`
- Authentication / authorization：`[MODEL]`
- Secret management：`[STRATEGY]`
- Input validation：`[RULES]`
- Logging redaction：`[RULES]`
- User data controls：`[RULES]`

## 11. Reliability and Error Handling

- 可恢复错误：`[RECOVERY]`
- 不可恢复错误：`[FAIL_CLOSED_OR_OPEN]`
- Retry / timeout / idempotency：`[POLICY]`
- Resource cleanup：`[POLICY]`
- Offline / degraded mode：`[BEHAVIOR]`

## 12. Observability

- Logs：`[LOGGING_STRATEGY]`
- Metrics：`[KEY_METRICS]`
- Tracing：`[TRACING]`
- Diagnostics：`[USER_OR_DEV_DIAGNOSTICS]`
- Privacy constraints：`[REDACTION]`

## 13. Build, Deployment and Distribution

- Build pipeline：`[PIPELINE]`
- Environments：`[ENVIRONMENTS]`
- Configuration：`[CONFIG_STRATEGY]`
- Release：`[RELEASE_FLOW]`
- Rollback：`[ROLLBACK]`

## 14. Testing Strategy

| Layer | What It Proves | Tool / Method | Required For |
| --- | --- | --- | --- |
| Unit | `[BEHAVIOR]` | `[TOOL]` | `[CHANGES]` |
| Integration | `[BEHAVIOR]` | `[TOOL]` | `[CHANGES]` |
| E2E | `[USER_PATH]` | `[TOOL]` | `[CHANGES]` |

## 15. Known Constraints and Technical Debt

- `[CONSTRAINT_OR_DEBT]` — Impact: `[IMPACT]`; Revisit: `[CONDITION]`

## 16. Open Architecture Questions

- `[QUESTION]`

## 17. Related Decisions

- `[DEC-XXX: TITLE]`

