# finops-Toolkit 🏦

> 金融运营技能工厂 — 互金运营全链路 Agent 工具包。运营团队即插即用，7 大角色各司其职，产出必过三纪律闸。

---

## 一句话安装

```bash
# 克隆到本地
git clone https://github.com/lj22503/finops-Toolkit.git
cd finops-Toolkit

# 查看可用的 Skill 入口
cat SKILL_INDEX.md
```

---

## 核心能力

| 能力 | 说明 |
|------|------|
| 🤖 7 大角色协同 | 从运营总监到合规审查，覆盖运营全链路 |
| 🔀 场景自动路由 | 输入任务 → 自动判断该激活哪个角色 |
| ✅ 三闸门必过 | 任何产出必须通过合规闸 → 数据闸 → 验证闸 |
| 📂 原子知识沉淀 | atoms-knowledge-base 积累每一次运营实战经验 |
| 🔄 反馈学习闭环 | 运营结果自动回流，驱动策略持续迭代 |

---

## 三层架构

```
知识层 (skills/)  →  执行层 (roles/)  →  纪律层 (gates/)
```

**数据流向：** 用户需求进入 → 路由判断角色 → 角色产出 → 三闸依次审查 → 合格后输出

---

## 7 大角色

| # | 角色 | 文件 | 核心职责 |
|---|------|------|----------|
| 1 | 运营负责人（CEO） | `roles/01-operations-director.md` | 方向制定、资源分配、go/no-go 决策 |
| 2 | 策略运营（EM） | `roles/02-strategy-ops.md` | 策略拆解、增长方案、用户分层、A/B 测试 |
| 3 | 内容运营（Engineer） | `roles/03-content-ops.md` | 金融内容生产（公众号/小红书/雪球/短视频） |
| 4 | 活动运营（Engineer） | `roles/04-campaign-ops.md` | 活动设计（新手福利/定投挑战/加仓激励） |
| 5 | 产品运营（Engineer） | `roles/05-product-ops.md` | 功能迭代、自运营机制、运营工具配置 |
| 6 | 数据运营（QA） | `roles/06-data-ops.md` | 数据监控、效果复盘、指标体系、数据质量 |
| 7 | 合规运营（Release） | `roles/07-compliance-ops.md` | 合规审查、一票否决、上线把关 |

---

## 快速命令

| 命令 | 场景 |
|------|------|
| `/campaign-plan` | 活动策划 — 输入活动目标，输出完整活动方案 |
| `/community-monitor` | 舆情监控 — 追踪社区舆情，输出风险预警 |
| `/write-copy` | 文案撰写 — 输入产品/活动信息，输出合规文案 |

---

## Skills 模块（8 个）

| 模块 | 入口文件 | 职责 |
|------|----------|------|
| `router/` | `skills/router/` | 场景路由 — 判断当前任务该激活哪个角色 |
| `orchestrator/` | `skills/orchestrator/` | 任务编排 — 多角色协作时的流程调度 |
| `doc-generator/` | `skills/doc-generator/` | 文档生成 — 自动产出结构化运营文档 |
| `feedback-learner/` | `skills/feedback-learner/` | 反馈学习 — 从运营结果中提炼经验并迭代 |
| `finops-copywriting/` | `skills/finops-copywriting/` | 文案撰写 — 金融场景专业文案 |
| `finops-community-monitor/` | `skills/finops-community-monitor/` | 舆情监控 — 社区舆情追踪与分析 |
| `knowledge/` | `skills/knowledge/` | 知识检索 — 原子化运营知识快速查询 |
| `pm-skills/` | `skills/pm-skills/` | PM 技能 — 需求管理与项目追踪 |

---

## Gates 纪律层

任何产出必须依次通过三闸，缺一不可：

```
合规闸 (gate-compliance.md)
  ↓  数据闸 (gate-data.md)
       ↓  验证闸 (gate-validation.md)
            ↓ 合格输出
```

| 闸门 | 审查内容 |
|------|----------|
| **合规闸** | 是否触及监管红线（承诺收益/推荐个股/虚假宣传） |
| **数据闸** | 数据来源是否真实、口径是否标注、异常是否有备注 |
| **验证闸** | 策略假设是否可量化、结论是否可验证 |

另有 `route-gate.md`（判断任务是否该进 Agent）、`stage-gate.md`（判断当前阶段是否可以进入下一阶段）。

---

## 核心文档索引

| 文件 | 作用 |
|------|------|
| `SKILL.md` | 路由入口 — 所有 Skill 的主入口 |
| `SKILL_INDEX.md` | 场景路由表 — 场景 → 角色/ Skill 映射 |
| `pipeline.md` | 6 阶段流水线 — 从需求到产出的完整流程 |
| `pipeline.yaml` | 流水线配置 — 各阶段的输入输出定义 |
| `manifest.yaml` | 整体架构清单 — 当前系统的完整组件清单 |
| `knowledge/atoms-knowledge-base.md` | 原子知识库 — 实战经验沉淀 |
| `plan/PROJECT_PLAN.md` | 项目计划 |
| `plan/tracking.md` | 进度追踪 |
| `feedback-rules.yaml` | 反馈学习规则 |
| `doc-config.yaml` | 文档生成配置 |

---

## 目录结构

```
finops-Toolkit/
├── commands/              # CLI 快速命令
├── data/                  # 数据文件
├── gates/                 # 纪律层（5 个 gate 文件）
│   ├── gate-compliance.md
│   ├── gate-data.md
│   ├── gate-validation.md
│   ├── route-gate.md
│   └── stage-gate.md
├── knowledge/             # 原子知识库
│   └── atoms-knowledge-base.md
├── plan/                  # 项目计划
│   ├── PROJECT_PLAN.md
│   └── tracking.md
├── plugins/               # 插件扩展
├── roles/                 # 执行层（7 个角色）
│   ├── 01-operations-director.md
│   ├── 02-strategy-ops.md
│   ├── 03-content-ops.md
│   ├── 04-campaign-ops.md
│   ├── 05-product-ops.md
│   ├── 06-data-ops.md
│   └── 07-compliance-ops.md
├── skills/                # 知识层（8 个模块）
│   ├── doc-generator/
│   ├── feedback-learner/
│   ├── finops-community-monitor/
│   ├── finops-copywriting/
│   ├── knowledge/
│   ├── orchestrator/
│   ├── pm-skills/
│   └── router/
├── SKILL.md               # 路由入口
├── SKILL_INDEX.md         # 场景路由表
├── pipeline.md            # 6 阶段流水线
├── pipeline.yaml          # 流水线配置
├── manifest.yaml          # 整体架构清单
├── feedback-rules.yaml    # 反馈学习规则
└── doc-config.yaml       # 文档生成配置
```

---

*Built by 燃冰 + ant*
