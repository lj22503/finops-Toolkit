---
name: route-gate
description: Hard gate that blocks execution until router has successfully selected a role with acceptable confidence
---

# Hard Gate: Route Validation

## Trigger

Before executing any role, this gate MUST be passed.

## Checklist

- [ ] manifest.yaml has been loaded
- [ ] User intent has been extracted
- [ ] At least one role matched (or default_role used)
- [ ] Confidence level is acceptable OR user confirmed

## If Fails

**BLOCKING:** Do not proceed to role execution. Either:
1. Request clarification from user
2. Route to default_role and log the ambiguity

## Confidence Thresholds

| Level | Threshold | Action |
|-------|-----------|--------|
| High | ≥ 0.7 | Proceed directly |
| Medium | 0.4-0.7 | Present candidates, ask user to confirm |
| Low | < 0.4 | Route to default_role, log feedback |

## Anti-Rationalization

- "I'm pretty sure" ≠ High confidence. Use the manifest threshold.
- "User didn't object" ≠ User confirmed. Explicit confirmation required.
- "This is close enough" → Route to correct role, don't guess.
