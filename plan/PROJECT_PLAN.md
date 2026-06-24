# 金融运营技能工厂 · 项目计划

**状态：** 🟢 启动
**开始：** 2026-06-23
**基于：** [lj22503/vertical-skill-factory](https://github.com/lj22503/vertical-skill-factory)
**元技能约束：** 必须过3层（知识层+执行层+纪律层），纪律层硬门禁一票否决

---

## 项目结构

```
finops-skill-factory/
├── plan/
│   ├── PROJECT_PLAN.md     ← 本文件
│   ├── tracking.md         ← 执行进度追踪
│   └── gates/              ← 纪律层门禁检查记录
├── skills/                  ← 知识层（pm-skills风格）
│   ├── finops-aarrr/
│   ├── user-lifecycle/
│   ├── competitor-analysis/
│   ├── campaign-design/
│   ├── data-metrics/
│   └── content-strategy/
├── roles/                   ← 执行层（3+1架构：3个Agent+1个人类）
│   ├── 01-ops-line.md       🟢 运营线（原03+04+05合并）
│   ├── 02-data-line.md      🔵 数据线（原02+06+策略合并）
│   ├── 03-compliance-line.md 🔴 合规线（原07保留）
│   └── archive/             📦 旧7角色文件（参考用）
├── gates/                   ← 纪律层（Superpowers风格）
│   ├── gate-compliance.md
│   ├── gate-data.md
│   └── gate-validation.md
├── pipeline.md              ← 整体工作流编排
└── SKILL_INDEX.md
```

---

## 执行计划（分5个Phase）

### Phase 1：纪律层（P0）🛡️ ← 先做，因为其他阶段输出必须过闸

| # | 任务 | 预估 | 依赖 |
|---|------|------|------|
| 1.1 | 合规闸 gate-compliance.md | 复用既有 `finance-marketing-compliance` | 无 |
| 1.2 | 数据闸 gate-data.md | 新建 | 无 |
| 1.3 | 验证闸 gate-validation.md | 新建 | 无 |

**门禁规则：** 纪律层 gate 未通过 → ❌ BLOCKED（一票否决，不允许绕过）

### Phase 2：知识层 - 核心6skill（P1）📚

| # | 任务 | 预估 | 依赖 |
|---|------|------|------|
| 2.1 | 金融运营AARRR | pm-skills风格 | 无 |
| 2.2 | 用户分层与生命周期 | pm-skills风格 | 无 |
| 2.3 | 竞品分析（金融产品版） | pm-skills风格 | 无 |
| 2.4 | 活动运营设计 | pm-skills风格 | 无 |
| 2.5 | 数据指标体系 | pm-skills风格 | 无 |
| 2.6 | 内容策略框架 | pm-skills风格 | 无 |

**每个skill完成后过纪律层3道闸才进入下一个**
**门禁规则：** 缺失任意skill → 知识层覆盖率不达标 → ❌ BLOCKED

### Phase 3：执行层 - 角色定义 + Pipeline（P2）👥 ✅ 已完成3+1精简

| # | 任务 | 状态 | 说明 |
|---|------|------|------|
| 3.1 | ~~7个角色~~ → **3+1精简** | ✅ 已重构 | 7角色→3Agent角色(运营线/数据线/合规线)+燃冰(决策者) |
| 3.2 | pipeline.md | ✅ 已更新 | 按3+1架构重写全流程 |

**2026-06-24 重构说明：**
- 旧7角色（按人头切）→ 新3+1（按能力体切）
- 运营负责人角色删除 → 燃冰直接担任
- 旧7文件已归档至 `roles/archive/`

**门禁规则：** 缺少任意角色PRD或pipeline → ❌ BLOCKED

### Phase 4：ClawHub/GitHub补充安装（P2）🔌

| # | 任务 | 说明 |
|---|------|------|
| 4.1 | content-writer (2.97) | 内容生产增强 |
| 4.2 | a-b-test-planner (3.0) | 策略验证 |
| 4.3 | user-growth-gungun (2.9) | 增长策略参考 |
| 4.4 | 竞品分析助手 (1.72) | 收集节点增强 |
| 4.5 | data-analysis-skill (1.58) | 数据运营辅助 |

### Phase 5：整合发版（P3）🚀

| # | 任务 | 说明 |
|---|------|------|
| 5.1 | SKILL_INDEX.md | AI路由：什么场景调哪个skill |
| 5.2 | 所有产出过纪律层3闸 | 终验 |
| 5.3 | 提 PR / 发布 | 可发布到 ClawHub 或 GitHub |

---

## 纪律层门禁（各Phase通用）

### Gate 1: 合规闸
激活：每创建一个skill或角色文件后
检查：
- [ ] 金融合规表述是否正确
- [ ] 是否包含风险提示
- [ ] 是否明确禁止推销/承诺收益类话术
失败：❌ BLOCKED - 修改后再过

### Gate 2: 数据闸
激活：每次提交涉及数据判断的内容
检查：
- [ ] 所有数据结论是否标注来源
- [ ] 是否有"待更新"占位符（禁止）
- [ ] 是否可验证
失败：❌ BLOCKED - 补来源或删除不可验证内容

### Gate 3: 验证闸
激活：每个Phase产出后
检查：
- [ ] 产出物是否符合该Phase质量标准
- [ ] 产出物是否可被AI直接使用
- [ ] 是否有关键遗漏
失败：❌ BLOCKED - 修复后再进入下一Phase

---

## 执行约束

1. 一次一个Phase，完成后再进入下一个
2. 每个Phase完成后过3道闸（合规+数据+验证）
3. 闸不过 → 向燃冰报告原因 → 修复后再过
4. 每完成一个文件反馈一次结果
5. 不猜测、不跳过、不"之后补"
