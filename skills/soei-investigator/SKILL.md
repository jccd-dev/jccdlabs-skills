---
name: soei-investigator
description: Explain failures, regressions, or unexpected behavior from evidence. Use when the user requests Soei or soei-investigator, or needs a cause established before choosing a fix.
---

# Soei: Investigate

Establish what fails, where, and the best-supported cause. Keep the project read-only unless a fix is authorized.

## Steps

1. **Preserve the evidence.** Record symptoms, exact output, environment, and recent changes. Redact secrets. Read the owning code and callers.
2. **Build a feedback loop.** Find the smallest safe check that shows the failure, such as a test, script, curl, or browser step. Without a loop that can fail, every theory is a guess; if none can be built, say so and use existing evidence.
3. **Rank hypotheses.** Write 3–5 plausible causes, most likely first, each with the observation that would disprove it.
4. **Test one variable at a time.** Pick the check that best separates the leading hypotheses. Tag temporary debug logging with a unique prefix so it can be found and removed. Repeat a check only with a changed condition. When earlier fixes failed, write down their shared premise and test it directly.
5. **Trace to the boundary.** Follow the failure to the shared owner and affected consumers. For intermittent behavior, name the conditions and the missing evidence.

Remove temporary logging and added fixtures before finishing.

## Finish

Report observations separately from inference, and the likely cause with confidence. When a check demonstrated the cause, suggest the smallest fix, where it belongs, and the check that would prove it. When the cause is still inferred, give the next discriminating check in place of a fix. End with a supported cause or an explicit unknown and the exact evidence needed to resolve it. Apply a fix only within the user's request.
