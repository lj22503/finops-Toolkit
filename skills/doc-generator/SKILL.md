---
name: doc-generator
description: Use when you need to generate user-facing and AI-facing documentation for finops-Toolkit
---

# Doc Generator Skill

## Overview

Generates README files from skill package configuration:
- `README.user.md` — 面向互金运营从业者
- `README.ai.md` — 面向 AI Agent
- `README.meta.md` — 发布用元信息

## When to Use

- After creating a new skill package
- Before publishing a skill package
- When updating skill package (regenerate docs)

## Input Files

Required:
- `manifest.yaml` — role 列表和触发词
- `doc-config.yaml` — 文档配置

Optional:
- `pipeline.yaml` — pipeline 定义

## Output Files

### README.user.md

```markdown
# FinOps Toolkit

金融运营全链路 Agent 团队

## 这个工具能做什么

7角色分工，覆盖内容生产、活动策划、产品运营、数据分析、合规审查。

## 角色

- 运营负责人: 定方向、资源分配
- 策略运营: 增长策略、竞品分析
- 内容运营: 文案、内容、投教
- 活动运营: 活动策划与执行
- 产品运营: 功能需求、运营工具
- 数据运营: 数据监控、效果复盘
- 合规运营: 合规审查、一票否决

## 快速开始

1. 说"帮我制定季度运营规划"开始
2. AI 自动分配到对应角色
3. 合规审查后输出最终方案
```

### README.ai.md

```markdown
# AI README

## Manifest

[manifest.yaml content]

## Pipeline

[pipeline.yaml content]

## Routing Instructions

When user input matches triggers in manifest, route to corresponding role.
If no match, use default_role.
If ambiguous, present candidates and ask for confirmation.
```

## Hard Gate

**GATE: Config Required**
- If doc-config.yaml missing → generate from manifest
- If manifest.yaml missing → BLOCK, cannot generate docs
