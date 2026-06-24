---
name: router
description: Use when you need to route a user input to the correct skill in finops-Toolkit — detects intent (运营/数据/合规) and selects the appropriate skill line
---

# Router Skill

## Overview

Routes user input to the correct skill line (运营线/数据线/合规线) using LLM-based semantic matching. Reads manifest.yaml to get available skills and their triggers.

## When to Use

- User provides input that could map to multiple skill lines
- Unclear which skill line should handle the request
- Starting a new session with finops-Toolkit

## Routing Flow

```
User Input
    │
    ▼
Load manifest.yaml
    │
    ▼
Extract intent from user input using LLM
    │
    ▼
Match intent against skill triggers in manifest
    │
    ├─ High confidence (≥ threshold) → Route to target skill
    ├─ Medium confidence (< threshold) → Return candidates, ask user
    └─ No match → Route to default_skill, log feedback
```

## FinOps Manifest

```yaml
skills:
  - name: ops-line
    triggers:
      - "写文案" / "做内容" / "设计活动" / "用户增长"
      - "活动策划" / "启动运营周期" / "新季度规划"
    description: "运营线 - 全栈触达：内容+活动+渠道"

  - name: data-line
    triggers:
      - "分析数据" / "复盘效果" / "监控舆情"
      - "社区动态" / "数据报告"
    description: "数据线 - 大脑：分析+策略+验证"

  - name: compliance-line
    triggers:
      - "检查合规" / "这个能发吗" / "合规审查"
      - "审核内容"
    description: "合规线 - 门禁：审查+一票否决"

  - name: full-cycle
    triggers:
      - "启动运营周期" / "新季度规划" / "完整流程"
    description: "完整运营周期 - 6步串行"

default_skill: ops-line
```

## Routing Prompt

When routing, use this prompt structure:

```
You are a router for FinOps Toolkit. Given the user input, select the most appropriate skill line.

Available skill lines:
- ops-line (运营线): 写文案、做内容、设计活动、用户增长、活动策划、启动运营周期
- data-line (数据线): 分析数据、复盘效果、监控舆情、社区动态、数据报告
- compliance-line (合规线): 检查合规、审核内容、合规审查

User input: {user_input}

Analyze:
1. What is the user trying to accomplish?
2. Which skill line best matches this intent?
3. What is your confidence level (high/medium/low)?

Output format:
- Skill: [skill_name]
- Confidence: [high/medium/low]
- Reasoning: [brief explanation]
```

## Hard Gate

**GATE: Manifest Required**
- If manifest.yaml is missing → BLOCK, generate one first
- If user input doesn't match any skill → route to default_skill, log to feedback-log

## Anti-Patterns

- Routing without reading manifest.yaml
- Forcing a route when confidence is low
- Ignoring the feedback system when routing fails
