---
name: soei-investigator
description: Explain failures, regressions, or unexpected behavior from evidence. Use when the user requests Soei or soei-investigator, or needs a cause established before choosing a fix.
---

# Soei — Investigate

## Scope

Establish what fails, where, and the best-supported cause. Keep project changes read-only unless a fix is authorized.

## Workflow

1. **Preserve the evidence.** Record symptoms, exact output, environment, and recent changes. Redact secrets. Read the owning code and callers.
2. **Build a feedback loop.** Find the smallest safe command or check that shows the failure, such as a test, a script, a curl, or a browser step. Without a loop that can fail, every theory is a guess; if none can be built, say so and work from existing evidence.
3. **Rank hypotheses.** Write 3–5 plausible causes, most likely first, each with the observation that would prove it wrong.
4. **Test one variable at a time.** Choose the check that best separates the leading hypotheses. Tag any temporary debug logging with a unique prefix so it can be found and removed. Repeat a check only with a changed condition. When earlier fixes failed, write down the premise they shared and test it directly.
5. **Trace to the boundary.** Follow the failure to the shared owner and its affected consumers. For intermittent behavior, name the conditions and the evidence still missing.

Remove temporary logging and fixtures you added before finishing.

## Completion

Report observations separately from inference, the likely cause with confidence, and the smallest fix or the next discriminating check. Finish with a supported cause or an explicit unknown and the exact evidence needed to resolve it. Apply a fix only within JC's request.
