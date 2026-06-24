---
name: stage-gate
description: Hard gate that validates each pipeline stage boundary — blocks if previous stage incomplete or required inputs missing
---

# Hard Gate: Stage Execution

## Trigger

Before and after each pipeline stage execution.

## Pre-Stage Checklist

- [ ] All dependencies listed in `depends` have completed
- [ ] All input references (`stage://...`) resolve to valid data
- [ ] Required fields in input are not empty
- [ ] Previous stage output passed validation

## Post-Stage Checklist

- [ ] Stage executed without error
- [ ] Output contains all expected fields
- [ ] Output format matches contract
- [ ] Data written to correct context location

## If Fails

**BLOCKING:** Do not proceed to next stage. Options:
1. Retry stage (max 2 retries)
2. If unrecoverable → Abort pipeline, report failure

## Context Management

Each stage reads from and writes to shared pipeline context:

```
context = {
  "stage://understand-request/parsed-intent": {...},
  "stage://ops-execution/ops-result": {...},
  ...
}
```

Never read directly from previous stage files. Use context only.

## Anti-Rationalization

- "The output looks close enough" → Must match contract exactly
- "I'll fix it in the next stage" → Fix it now or block
- "Just this once" → Stages are not optional
