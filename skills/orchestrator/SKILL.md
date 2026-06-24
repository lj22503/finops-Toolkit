---
name: orchestrator
description: Use when you need to execute a multi-step pipeline of finops skill lines with defined order, dependencies, and validation gates between stages
---

# Pipeline Orchestrator Skill

## Overview

Executes a pipeline of FinOps skill lines in defined order, passing context between stages, and enforcing hard gates at each stage boundary.

## When to Use

- Complex task requiring multiple skill lines in sequence
- Task with parallel branches that must converge
- Task where each stage output feeds into the next

## FinOps Pipeline Format

Place `pipeline.yaml` in the skill package root:

```yaml
name: finops-full-cycle
entry_skill: router

stages:
  - name: route-intent
    skill: router
    output_var: routed-skill

  - name: load-atoms
    skill: ops-line
    depends: [route-intent]
    gate:
      requires: [routed-skill]

  - name: ops-execution
    skill: ops-line
    depends: [load-atoms]
    output_var: ops-result

  - name: compliance-check
    skill: compliance-line
    depends: [ops-execution]
    input:
      content: stage://ops-execution/ops-result
    output_var: compliance-result

  - name: data-analysis
    skill: data-line
    depends: [compliance-check]
    output_var: data-result

  - name: final-review
    skill: data-line
    depends: [data-analysis]
    output_var: final-result
```

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

## Stage Gate Prompt

Before executing each stage, verify:

```
Stage: {stage_name}
Required input: {stage.input}
Dependencies: {stage.depends}

Check:
1. All dependencies completed successfully?
2. Required input variables available?
3. Previous stage output format valid?

If all checks pass → Proceed to execute stage
If any check fails → BLOCK, do not proceed
```

## FinOps-Specific Rules

1. **合规线永远在发布前最后一步**: 不提前、不跳过
2. **原子知识库为所有产出的前置输入**: 任何角色开始工作前，必须先读取 `knowledge/atoms-knowledge-base.md`
3. **燃冰只在"定方向"和"拍板"时介入**: 执行过程不需要他

## Hard Gates

1. **Pre-Stage Gate**: Verify all inputs available before stage execution
2. **Post-Stage Gate**: Verify stage output complete before proceeding
3. **Compliance Gate**: Verify compliance-line has approved before publishing

## Anti-Patterns

- Skipping a stage because "it's obvious what to do"
- Proceeding when a previous stage output is missing
- Merging parallel results incorrectly
- Hardcoding stage order instead of reading pipeline.yaml
- Skipping compliance gate before publishing
