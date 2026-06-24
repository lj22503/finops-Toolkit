---
name: router
description: Use when you need to route a user input to the correct role in finops-Toolkit — detects intent and selects the appropriate role
---

# Router Skill

## Overview

Routes user input to the correct role using LLM-based semantic matching. Reads manifest.yaml to get available roles and their triggers.

## When to Use

- User provides input that could map to multiple roles
- Unclear which role should handle the request
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
Match intent against role triggers in manifest
    │
    ├─ High confidence (≥ threshold) → Route to target role
    ├─ Medium confidence (< threshold) → Return candidates, ask user
    └─ No match → Route to default_role, log feedback
```

## Routing Prompt

```
You are a router for FinOps Toolkit. Given the user input, select the most appropriate role.

Available roles:
- operations-director: 定方向、资源分配、季度/年度规划、go/no-go决策
- strategy-ops: 增长策略、用户分层、竞品分析、策略方案、A/B测试
- content-ops: 写文案、做内容、投教内容、多平台分发
- campaign-ops: 设计活动、活动策划、拉新/留存活动
- product-ops: 产品功能、自运营、运营工具、PRD
- data-ops: 分析数据、复盘效果、数据监控、指标体系
- compliance-ops: 检查合规、合规审查（高置信度直接过）

User input: {user_input}

Output format:
- Role: [role_name]
- Confidence: [high/medium/low]
- Reasoning: [brief explanation]
```

## Hard Gate

**GATE: Manifest Required**
- If manifest.yaml is missing → BLOCK, generate one first
- If user input doesn't match any role → route to default_role, log to feedback-log

## Anti-Patterns

- Routing without reading manifest.yaml
- Forcing a route when confidence is low
- Ignoring the feedback system when routing fails
