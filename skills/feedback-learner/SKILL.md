---
name: feedback-learner
description: Use when you need to capture user corrections and maintain a feedback log for finops-Toolkit
---

# Feedback Learner Skill

## Overview

后台静默捕获用户否定信号，记录路由错误，生成待确认的 trigger 映射更新队列。

**用户无感知**，完全后台运行。

## When to Use

- After any router or orchestrator execution
- When monitoring finops-Toolkit in production

## Negation Signal Detection

Monitor user input for:
- Chinese: 不对/不是/换个/重来/不是这个意思/不行
- English: no/not that/wrong/different

## Capture Logic

When negation signal detected:
1. Extract: user_expression, previous_ai_response, routed_role
2. Prompt for correction if not obvious
3. Write to feedback-log.jsonl

## Batch Update Process

```
1. Read feedback-log.jsonl
2. Group by (user_expr, routed_role)
3. Count negation frequency
4. For each with count ≥ threshold → add to review_queue
5. Generate review_queue report
```

## Review Queue Output

```markdown
# Feedback Review Queue

| User Expression | Was Routed To | Correction Count | Suggested Action |
|-----------------|---------------|-----------------|------------------|
| "写文案"       | data-ops      | 5               | Add to content-ops triggers |

Review and apply changes to manifest.yaml manually.
```

## Hard Gate

**GATE: Learning Without Disruption**
- Feedback capture must NOT interrupt user flow
- All corrections require user confirmation before applying to manifest
- Manifest updates require manual review

## Anti-Patterns

- Updating manifest without user confirmation
- Capturing feedback without storing to log
- Ignoring low-frequency corrections
