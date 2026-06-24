---
name: finops-toolkit
description: "金融运营技能工具包 - 7角色分工，覆盖内容生产、活动策划、产品运营、数据分析、合规审查的全链路运营团队。当用户需要制定运营规划、分析数据、设计活动、撰写内容、审查合规时激活。"
---

# FinOps Toolkit

**版本：** 3.0.0
**最后更新：** 2026-06-24

---

## 定位

金融运营全链路 Agent 团队工具包。7 角色分工，覆盖：
- 内容生产
- 活动策划
- 产品运营
- 数据分析
- 合规审查

---

## 7 角色

| 角色 | 文件 | 核心职责 |
|------|------|---------|
| 运营负责人 | `roles/01-operations-director.md` | 定方向、资源分配、go/no-go |
| 策略运营 | `roles/02-strategy-ops.md` | 增长策略、竞品分析、用户分层 |
| 内容运营 | `roles/03-content-ops.md` | 文案、内容、投教、多平台分发 |
| 活动运营 | `roles/04-campaign-ops.md` | 活动策划与执行 |
| 产品运营 | `roles/05-product-ops.md` | 功能需求、自运营机制、运营工具 |
| 数据运营 | `roles/06-data-ops.md` | 数据监控、效果复盘、指标维护 |
| 合规运营 | `roles/07-compliance-ops.md` | 合规审查、一票否决 |

---

## 知识层

### 运营方法论 (`skills/knowledge/`)
| Skill | 用途 |
|-------|------|
| `dual-value-positioning` | 双向价值定位法 |
| `six-repositories` | 六库资产沉淀法 |
| `compliance-red-line` | 合规红线意识 |
| `aarrr-funnel` | AARRR 漏斗实操 |
| `content-long-short` | 长短线内容结合 |
| `campaign-5w1h` | 活动运营 5W1H |
| `mvp-breakthrough` | MVP 最小可行性破局 |
| `data-attribution` | 数据导航与归因 |
| `ecosystem-design` | 生态化做局 |
| `return-first` | 回报后置信任逻辑 |
| `finance-compliance-review` | 金融营销合规审查 |

### pm-skills 引入 (`skills/pm-skills/`)
| Skill | 用途 |
|-------|------|
| `competitor-analysis` | 竞品分析 |
| `customer-journey-map` | 用户旅程地图 |
| `user-personas` | 用户画像 |
| `growth-loops` | 增长飞轮 |
| `gtm-strategy` | GT M策略 |
| `marketing-ideas` | 营销创意 |
| `ab-test-analysis` | A/B测试分析 |
| `cohort-analysis` | 同期群分析 |
| `opportunity-solution-tree` | 机会解决方案树 |

---

## 门禁层 (`gates/`)

| 门禁 | 触发条件 |
|------|---------|
| `route-gate` | 路由验证 - 执行前必过 |
| `compliance-gate` | 内容/活动合规审查 - 发布前必过 |
| `data-gate` | 数据判断产出 - 必过 |
| `validation-gate` | 阶段转换 - 必过 |
| `stage-gate` | Pipeline阶段边界 - 必过 |

---

## 路由入口

**触发条件：** 用户提到以下场景时激活：
- 制定运营规划/季度规划/年度规划
- 分析数据/效果复盘/监控舆情
- 设计活动/用户增长/活动策划
- 撰写内容/文案/投教
- 合规审查/检查合规

**路由决策：**

```
用户输入
    │
    ├─ "定方向"/"资源分配"/"季度规划" → 运营负责人
    │
    ├─ "增长策略"/"竞品分析"/"用户分层" → 策略运营
    │
    ├─ "写文案"/"做内容"/"投教" → 内容运营
    │
    ├─ "设计活动"/"活动策划" → 活动运营
    │
    ├─ "产品功能"/"运营工具"/"PRD" → 产品运营
    │
    ├─ "分析数据"/"复盘效果"/"监控" → 数据运营
    │
    ├─ "检查合规"/"合规审查"/"能发吗" → 合规运营
    │
    └─ 其他 → 匹配最相关角色，或问用户
```

---

## 核心规则

1. **合规永远在发布前最后一步**
2. **数据判断必须过数据闸**
3. **阶段转换必须过验证闸**
4. **运营产出必须先过合规闸再发布**

---

## 依赖知识

执行任何角色前，必须先读取相关知识：
- 内容运营 → `dual-value-positioning`, `content-long-short`, `compliance-red-line`
- 活动运营 → `campaign-5w1h`, `aarrr-funnel`, `compliance-red-line`
- 数据运营 → `data-attribution`, `aarrr-funnel`
- 合规运营 → `finance-compliance-review`, `compliance-red-line`

---

## 版本历史

| 版本 | 日期 | 更新内容 |
|------|------|---------|
| v3.0.0 | 2026-06-24 | 全面重构：7角色 + 知识拆分 + 4模块 |
| v2.0.0 | 2026-03-26 | 初始版本（3线结构） |
