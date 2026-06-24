---
name: feedback-learner
description: Use when you need to capture user corrections and maintain a feedback log for finops-Toolkit — detects negation signals, records routing mismatches, and queues confirmed corrections for manifest update
---

# Feedback Learner Skill

## Overview

后台静默捕获用户否定信号，记录路由错误，生成待确认的 trigger 映射更新队列。

**用户无感知**，完全后台运行。

## When to Use

- After any router or orchestrator execution
- When monitoring finops-Toolkit in production
- During skill package iteration

## Feedback Data Format

**feedback-log.jsonl**

```jsonl
{"ts": "2026-06-24T10:00:00Z", "user_expr": "写个文案", "routed_skill": "data-line", "negation": false}
{"ts": "2026-06-24T10:01:00Z", "user_expr": "不对，是写文案", "routed_skill": "data-line", "negation": true, "correct_skill": "ops-line"}
```

## Negation Signal Detection

Monitor user input for these signals:

**Chinese:**
- 不对
- 不是
- 换个
- 重来
- 不是这个意思
- 不行

**English:**
- no
- not that
- wrong
- different

## Capture Logic

When negation signal detected:

```
1. Extract from context:
   - user_expression: current user message
   - previous_ai_response: what AI said/did
   - routed_skill: what skill line was routed to

2. Prompt user for correction (if not obvious):
   "Did you mean [alternative skill]?"

3. If correction confirmed or obvious:
   Write to feedback-log.jsonl with:
   - negation: true
   - correct_skill: the right skill
   - user_expr: what user said
```

## Batch Update Process

Run daily or on-demand:

```
1. Read feedback-log.jsonl
2. Group by (user_expr, routed_skill)
3. Count negation frequency
4. For each (user_expr, routed_skill) with count ≥ threshold:
   - Add to review_queue
5. Generate review_queue report
```

## Review Queue Output

```markdown
# Feedback Review Queue

## Pending Updates

| User Expression | Was Routed To | Correction Count | Suggested Action |
|-----------------|---------------|-----------------|------------------|
| "写文案"       | data-line     | 5               | Add "写文案" to ops-line triggers |
| "看数据"       | ops-line      | 3               | Add "看数据" to data-line triggers |

## High Confidence Mappings (auto-flagged)

| User Expression | Suggested Skill | Negation Rate |
|-----------------|-----------------|---------------|
| "帮我写"       | ops-line        | 95%           |

---

Review and apply changes to manifest.yaml manually.
```

## FinOps-Specific Triggers to Watch

Common routing errors in FinOps:
- "写文案" → sometimes routed to data-line instead of ops-line
- "分析" → ambiguous (could be data analysis or content analysis)
- "检查" → ambiguous (compliance check vs quality check)

## Hard Gate

**GATE: Learning Without Disruption**
- Feedback capture must NOT interrupt user flow
- All corrections require user confirmation before applying to manifest
- Manifest updates require manual review

## Anti-Patterns

- Updating manifest without user confirmation
- Capturing feedback without storing to log
- Ignoring low-frequency corrections (might become high-frequency)
- Treating user preference as routing error
