---
name: soei-investigator
description: Explain failures, regressions, or unexpected behavior from evidence. Use when the user requests Soei or soei-investigator, or needs a cause established before choosing a fix.
---

# Soei — Investigate

## Scope

Establish what fails, where it fails, and the best-supported cause. Keep project changes read-only unless a fix is authorized.

## Workflow

1. Preserve symptoms, relevant output, environment, and recent changes. Read the owning code and callers.
2. Reproduce the smallest safe case within test permissions, or inspect existing evidence when execution is unavailable. Choose the next check that distinguishes plausible causes; seek evidence that could disprove the preferred explanation. A repeated check needs a changed condition or a reason to expect new evidence. When earlier fixes failed, write down the premise they shared and test it directly.
3. Trace the failure to the shared boundary and affected consumers. For intermittent behavior, identify the conditions and evidence still missing.

## Completion

Report observations separately from inference, the likely cause and confidence, and the smallest fix or next discriminating check.

Finish with a supported cause or an explicit unknown and the exact evidence needed to resolve it. Apply a fix only within the user's request.
