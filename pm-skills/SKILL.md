---
name: pm-skills
description: 项目管理技能包。提供竞品分析、用户洞察、增长飞轮、A/B测试等 PM 核心能力，对接 finops-Toolkit 各角色的策略制定和效果验证阶段。
---

# PM Skills

finops-Toolkit 的 PM 技能层，为各角色提供专业的项目管理与分析工具。

## Skill 清单

| Skill 目录 | 用途 | 对接角色 |
|-----------|------|---------|
| `competitor-analysis/` | 竞品分析 | 策略运营 |
| `customer-journey-map/` | 用户旅程地图 | 策略运营、内容运营 |
| `user-personas/` | 用户画像 | 策略运营 |
| `growth-loops/` | 增长飞轮设计 | 策略运营、活动运营 |
| `gtm-strategy/` | GTM 策略 | 策略运营 |
| `marketing-ideas/` | 营销创意发散 | 活动运营、内容运营 |
| `ab-test-analysis/` | A/B 测试分析 | 数据运营、策略运营 |
| `cohort-analysis/` | 同期群分析 | 数据运营 |
| `opportunity-solution-tree/` | 机会解决方案树 | 策略运营 |

## 调用规范

各 role 文件通过 `skills/pm-skills/<skill-name>/SKILL.md` 调用对应的 PM skill。

示例：
```
内容运营 → 读取 `skills/pm-skills/user-personas/SKILL.md` 获得用户画像支持
策略运营 → 读取 `skills/pm-skills/competitor-analysis/SKILL.md` 获得竞品分析支持
数据运营 → 读取 `skills/pm-skills/ab-test-analysis/SKILL.md` 进行测试结果分析
```
