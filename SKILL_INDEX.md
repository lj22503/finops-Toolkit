# SKILL_INDEX.md — 路由索引

> AI 路由表：根据用户输入匹配 finops-Toolkit 角色和 skill。

---

## 前置规则

**所有角色开始工作前，必须先读取 `skills/knowledge/` 下对应的知识文档作为参考，输入来自 `knowledge/atoms-knowledge-base.md` 中的原子知识模块。**

---

## 路由矩阵

| 用户场景 | 触发关键词 | 路由角色 | 涉及文件 | 前置读取的知识文档 | 最终产出 |
|----------|-----------|---------|---------|------------------|---------|
| 制定运营方向 | `运营周期` `新季度` `月度计划` `运营规划` `定方向` `资源分配` | 运营负责人 | `roles/01-operations-director.md` + `pipeline.yaml` | `skills/knowledge/atoms-knowledge-base.md` | 运营方向文档+策略方案+执行产出+复盘报告 |
| 内容生产 | `写文案` `写文章` `小红书` `公众号` `投教` `Push` `Banner` | 内容运营 | `roles/03-content-ops.md` + `commands/write-copy.md` + `skills/finops-copywriting/` | `skills/knowledge/content-long-short.md` + `skills/knowledge/compliance-red-line.md` | 合规的运营内容 |
| 活动策划 | `设计活动` `用户增长` `拉新` `促活` `留存` `福利` `活动策划` | 活动运营 | `roles/04-campaign-ops.md` + `commands/campaign-plan.md` | `skills/knowledge/campaign-5w1h.md` + `skills/knowledge/aarrr-funnel.md` + `skills/knowledge/compliance-red-line.md` | 活动方案文档+合规审批结果 |
| 数据分析 | `分析数据` `复盘` `效果` `指标` `增长` `ROI` `归因` `数据监控` | 数据运营 | `roles/06-data-ops.md` + `gates/gate-data.md` + `gates/gate-validation.md` | `skills/knowledge/data-attribution.md` + `skills/knowledge/aarrr-funnel.md` | 数据分析报告+策略建议 |
| 舆情监控 | `舆情` `社区` `情绪` `热点` `动态` `天天基金` `蚂蚁` | 数据运营 | `roles/06-data-ops.md` + `commands/community-monitor.md` + `skills/finops-community-monitor/` | `skills/knowledge/data-attribution.md` | 舆情简报+预警 |
| 合规审查 | `合规` `能发吗` `违规` `审查` `检查` `把关` `合规审查` | 合规运营 | `roles/07-compliance-ops.md` + `gates/gate-compliance.md` | `skills/knowledge/finance-compliance-review.md` + `skills/knowledge/compliance-red-line.md` | 合规审查报告+放行/驳回 |
| 策略制定 | `增长策略` `竞品分析` `用户分层` `策略方案` `A/B测试` `测试方案` | 策略运营 | `roles/02-strategy-ops.md` + `gates/gate-validation.md` | `skills/knowledge/aarrr-funnel.md` + `skills/knowledge/dual-value-positioning.md` | 策略方案+A/B测试方案 |
| 产品运营 | `产品功能` `运营工具` `PRD` `产品需求` `自运营` | 产品运营 | `roles/05-product-ops.md` | `skills/knowledge/campaign-5w1h.md` | PRD文档+自运营方案 |

---

## 路由入口

触发路由 skill：
```
skills/router/SKILL.md — 读取 manifest.yaml，匹配用户意图 → 路由到对应 role
```

**manifest.yaml 中的 7 个角色（英文 slug）：**
- `operations-director` — 运营负责人
- `strategy-ops` — 策略运营
- `content-ops` — 内容运营
- `campaign-ops` — 活动运营
- `product-ops` — 产品运营
- `data-ops` — 数据运营
- `compliance-ops` — 合规运营

---

## 多角色串行原则

多角色场景严格按 pipeline.yaml 执行：

```
router（skill）→ 策略运营（role）→ 内容/活动/产品运营（并行 role）
    → 合规运营（role，过合规闸）→ 数据运营（role，数据追踪）
```

禁止在合规闸前跳过任何角色。

---

## 失败处理

| 场景 | 处理 |
|------|------|
| 合规闸驳回 | 退回给上一个角色，标注违规条款，修改后重新提交 |
| 数据异常 | 锁定当前阶段，标记"数据异常，原因待查"，等待确认后继续 |
| 方向变更 | 从策略运营重新开始 |
| 跨线争议 | 上报运营负责人裁决，暂停流程直到收到拍板 |

---

## 角色切换规范

角色切换时，必须传递`上下文包裹`：

```json
{
  "from": "策略运营",
  "to": "活动运营",
  "input": "本周期策略方案（用户分层+增长策略+目标拆解）",
  "context": "运营负责人确认的方向文档 + 历史数据基线"
}
```

接收方必须基于输入工作，不得要求重新输入或重新理解。
