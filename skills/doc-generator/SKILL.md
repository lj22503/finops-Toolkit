---
name: doc-generator
description: Use when you need to generate user-facing and AI-facing documentation for finops-Toolkit — creates README.user.md, README.ai.md, and README.meta.md
---

# Doc Generator Skill

## Overview

Generates three README files from skill package configuration:
- `README.user.md` — 面向互金运营从业者，产品宣传风格
- `README.ai.md` — 面向 AI Agent，嵌入 manifest + pipeline
- `README.meta.md` — 发布用元信息

## When to Use

- After creating a new skill package
- Before publishing a skill package
- When updating skill package (regenerate docs)

## Input Files

Required:
- `manifest.yaml` — skill 列表和触发词
- `doc-config.yaml` — 文档配置

Optional:
- `pipeline.yaml` — pipeline 定义（用于 README.ai.md）

## Output Files

### README.user.md（面向用户）

```markdown
# FinOps Toolkit

互金运营全链路 Agent 团队 — 让你专注策略，把执行交给 AI

## 这个工具能做什么

覆盖内容生产、活动策划、用户触达、数据分析、舆情监控、合规审查的全链路运营团队。

## 核心功能

- **运营线**: 写文案、做内容、设计活动、用户增长
- **数据线**: 分析数据、复盘效果、监控舆情
- **合规线**: 合规审查、一票否决

## 快速开始

1. 说"帮我写一篇基金推广文案"开始
2. AI 自动路由到对应技能线
3. 合规审查后输出最终内容

## 触发词

你可以用以下方式开始：
- "写文案" → 运营线
- "分析数据" → 数据线
- "检查合规" → 合规线
```

### README.ai.md（面向 AI）

```markdown
# AI README

This file provides AI agents with the information needed to use FinOps Toolkit.

## Manifest

```yaml
{manifest.yaml content}
```

## Pipeline

```yaml
{pipeline.yaml content}
```

## Routing Instructions

When user input matches triggers in manifest, route to the corresponding skill line.
If no match, use `default_skill`.
If ambiguous, present candidates and ask for confirmation.
```

### README.meta.md（发布用）

```markdown
---
name: finops-toolkit
description: 金融运营技能工具包 - 互金运营全链路 Agent 团队
version: 1.0.0
target_users:
  - 互金运营从业者
  - 基金/理财运营团队
---
```

## Hard Gate

**GATE: Config Required**
- If doc-config.yaml missing → generate from manifest
- If manifest.yaml missing → BLOCK, cannot generate docs

## Anti-Patterns

- Generating docs without reading manifest.yaml
- Using placeholder text instead of real content
- Including internal implementation details in user README
