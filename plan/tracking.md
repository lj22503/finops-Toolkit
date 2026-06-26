# 执行追踪

## 整体状态

| Phase | 描述 | 状态 | 完成 |
|-------|-----|------|------|
| P1 | 纪律层（5道闸） | ✅ | 5/5 |
| P2 | 知识层（6个可执行 skill 包 + 11个知识文档 + 9个 PM skill） | ✅ | 26/26 |
| P3 | 执行层（7角色 + pipeline） | ✅ | 8/8 |
| P4 | 命令入口（commands/） | ✅ | 3/3 |
| P5 | 文档一致性修复 + PM skill 迁移 | ✅ | — |

## Phase 1 子任务（纪律层 — 5道闸）

| # | 文件 | 状态 |
|---|------|------|
| 1.1 | `gates/gate-compliance.md` | ✅ |
| 1.2 | `gates/gate-data.md` | ✅ |
| 1.3 | `gates/gate-validation.md` | ✅ |
| 1.4 | `gates/route-gate.md` | ✅ |
| 1.5 | `gates/stage-gate.md` | ✅ |

## Phase 2 子任务（知识层）

### 可执行 Skill 包（skills/ 下有 SKILL.md）

| # | Skill 包 | 状态 |
|---|----------|------|
| 2.1 | `skills/router/` | ✅ |
| 2.2 | `skills/orchestrator/` | ✅ |
| 2.3 | `skills/doc-generator/` | ✅ |
| 2.4 | `skills/feedback-learner/` | ✅ |
| 2.5 | `skills/finops-copywriting/` | ✅ |
| 2.6 | `skills/finops-community-monitor/` | ✅ |

### 知识文档（skills/knowledge/ — AI 参考，不直接执行）

| # | 文件 | 状态 |
|---|------|------|
| 2.7 | `skills/knowledge/aarrr-funnel.md` | ✅ |
| 2.8 | `skills/knowledge/campaign-5w1h.md` | ✅ |
| 2.9 | `skills/knowledge/compliance-red-line.md` | ✅ |
| 2.10 | `skills/knowledge/content-long-short.md` | ✅ |
| 2.11 | `skills/knowledge/data-attribution.md` | ✅ |
| 2.12 | `skills/knowledge/dual-value-positioning.md` | ✅ |
| 2.13 | `skills/knowledge/ecosystem-design.md` | ✅ |
| 2.14 | `skills/knowledge/finance-compliance-review.md` | ✅ |
| 2.15 | `skills/knowledge/mvp-breakthrough.md` | ✅ |
| 2.16 | `skills/knowledge/return-first.md` | ✅ |
| 2.17 | `skills/knowledge/six-repositories.md` | ✅ |

### PM Skill 包（pm-skills/ — 从 D:\仓库\pm-skills 迁移）

| # | Skill 包 | 来源 | 状态 |
|---|----------|------|------|
| 2.18 | `pm-skills/competitor-analysis/` | pm-market-research | ✅ |
| 2.19 | `pm-skills/customer-journey-map/` | pm-market-research | ✅ |
| 2.20 | `pm-skills/user-personas/` | pm-market-research | ✅ |
| 2.21 | `pm-skills/growth-loops/` | pm-go-to-market | ✅ |
| 2.22 | `pm-skills/gtm-strategy/` | pm-go-to-market | ✅ |
| 2.23 | `pm-skills/marketing-ideas/` | pm-marketing-growth | ✅ |
| 2.24 | `pm-skills/ab-test-analysis/` | pm-data-analytics | ✅ |
| 2.25 | `pm-skills/cohort-analysis/` | pm-data-analytics | ✅ |
| 2.26 | `pm-skills/opportunity-solution-tree/` | pm-product-discovery | ✅ |

## Phase 3 子任务（执行层 — 7角色 + Pipeline）

| # | 文件 | 状态 |
|---|------|------|
| 3.1 | `roles/01-operations-director.md` | ✅ |
| 3.2 | `roles/02-strategy-ops.md` | ✅ |
| 3.3 | `roles/03-content-ops.md` | ✅ |
| 3.4 | `roles/04-campaign-ops.md` | ✅ |
| 3.5 | `roles/05-product-ops.md` | ✅ |
| 3.6 | `roles/06-data-ops.md` | ✅ |
| 3.7 | `roles/07-compliance-ops.md` | ✅ |
| 3.8 | `pipeline.yaml` | ✅ |

## Phase 4 子任务（命令入口）

| # | 命令 | 文件 | 状态 |
|---|------|------|------|
| 4.1 | `/campaign-plan` | `commands/campaign-plan.md` | ✅ |
| 4.2 | `/write-copy` | `commands/write-copy.md` | ✅ |
| 4.3 | `/community-monitor` | `commands/community-monitor.md` | ✅ |

## 架构说明

**Skill 包 vs 知识文档的区别：**
- **Skill 包**（有 SKILL.md）：可被 AI 直接调用执行，有输入输出定义
- **知识文档**（.md）：AI 执行 role 时作为参考知识，不直接调用

**Pipeline 执行流程：**
```
router（skill）→ 路由到具体 role
    ↓
orchestrator（skill）→ 按 pipeline.yaml 调度各 role
    ↓
各 role 执行 → 产出过三闸（gates/）
    ↓
feedback-learner（skill）→ 捕获反馈并学习
```

## 待办事项

- [x] `pm-skills/` 9个 skill 从 `D:\仓库\pm-skills` 迁移完成
- [ ] `data/feedback-log.jsonl` 随 feedback-learner 运行自动生成
