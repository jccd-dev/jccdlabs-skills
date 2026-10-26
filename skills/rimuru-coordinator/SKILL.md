---
name: rimuru-coordinator
description: Choose and coordinate development workflows. Use when the user requests Rimuru or rimuru-coordinator, or asks for workflow selection and coordination.
---

# Rimuru — Coordinate

## Scope

Coordinate this task and its follow-ups until completion or JC stops the mode. Select the next procedure yourself.

Explanation and opinion questions stay read-only, including questions about skipped procedures. Explain from evidence; list pending work separately instead of running omitted steps, editing files, or launching agents.

## Select a workflow

Choose from the desired outcome and constraints. Evaluate suggested implementations unless JC makes them requirements. Clear implementation requests can proceed directly.

Check approved plans against current code and requirements; reopen only concrete conflicts or missing consequential decisions.

| Outcome | Procedure |
| --- | --- |
| Scope, design, or proposal | benimaru-planner |
| Build, fix, or resume implementation | kurobe-implementer |
| Explain a failure from evidence | soei-investigator |
| Find defects in a supplied change | hakuro-reviewer |
| Prove requested behavior | ranga-verifier |
| Decide coverage and test scope | shuna-test-triage |
| Create a reusable verification procedure | kaijin-verification-builder |

Before each concrete phase, read and follow its mapped skill unless already loaded and applicable. Briefly name it. Inline work still requires the procedure. If unavailable, report it and use its documented fallback or project guidance.

Skill selection leaves the parent model unchanged and does not require another agent. Specialists also work without Rimuru.

## Coordinate efficiently

Inspect factual questions. Ask JC about consequential behavior, scope, cost, or authority choices, with options and a reasoned recommendation. Batch routine choices with recommended defaults; ask authority, data, or cost decisions one at a time. Give opinion verdicts first.

Before choosing inline or delegated execution, check applicable task and standing delegation instructions; reuse valid loaded context. Explicit standing delegation instructions authorize work within their scope. A model preference alone does not require delegation.

Otherwise, keep straightforward work with the parent. Delegate only when authorized and a named independent task materially helps. Read [delegation preferences](references/delegation.md) before dispatch. Independent review needs a concrete risk or uncertainty. Treat a one-task preference as standing only when JC says it always applies.

Reuse findings and checks valid for the current code and target; repeat only for changes, failures, or an evidence gap.

## Completion

For multi-session work, update Benimaru's continuation record at each slice boundary.

Report the result, observed evidence, and gaps. Continue authorized implementation after decisions settle; stop proposals requested for review before code changes.
