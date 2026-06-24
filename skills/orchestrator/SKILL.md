---
name: orchestrator
description: Use when you need to execute a multi-step pipeline of finops roles with defined order, dependencies, and validation gates between stages
---

# Pipeline Orchestrator Skill

## Overview

Executes a pipeline of FinOps roles in defined order, passing context between stages, and enforcing hard gates at each stage boundary.

## When to Use

- Complex task requiring multiple roles in sequence
- Task with parallel branches that must converge
- Task where each stage output feeds into the next

## Execution Rules

### Stage Order
1. Execute stages in defined order
2. If stage has `depends`, wait for dependencies to complete
3. If stage has `parallel`, execute all in parallel, wait for all to complete

### Data Passing
- Reference previous stage output: `stage://stage-name/variable-name`
- All stage outputs stored in pipeline context
- Missing reference → BLOCK at gate

### Gate Rules

| Condition | Action |
|-----------|--------|
| Previous stage output missing | BLOCK, require retry |
| Required field empty | BLOCK, require 补充 |
| Stage execution error | Allow 2 retries, then BLOCK |

## FinOps Pipeline

```yaml
stages:
  - route-intent: 路由到正确角色
  - strategy-formulation: 策略制定（串行）
  - execution: 策略/内容/活动/产品并行执行
  - compliance-check: 合规审查（必须在上线前）
  - data-review: 数据复盘
```

## FinOps-Specific Rules

1. **合规线永远在发布前最后一步**: 不提前、不跳过
2. **运营产出必须过合规闸**: 不允许先发后补
3. **数据线是监控和反馈**: 不直接触达用户

## Hard Gates

1. **Pre-Stage Gate**: Verify all inputs available before stage execution
2. **Post-Stage Gate**: Verify stage output complete before proceeding
3. **Compliance Gate**: Verify compliance-ops has approved before publishing

## Anti-Patterns

- Skipping a stage because "it's obvious what to do"
- Proceeding when a previous stage output is missing
- Skipping compliance gate before publishing
- Hardcoding stage order instead of reading pipeline.yaml
