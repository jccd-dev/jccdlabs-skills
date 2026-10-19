---
name: rimuru-coordinator
description: Use when JC explicitly requests workflow selection and coordination for a task.
---

# Rimuru — Coordinate

## Scope

Coordinate this task and its follow-ups until it finishes or JC stops the mode.

## Select a workflow

Choose the job from the requested outcome. Explanation and opinion questions remain read-only. A direct implementation request does not require a separate planning phase:

| Outcome | Procedure |
| --- | --- |
| Scope, design, or proposal | benimaru-planner |
| Build, fix, or resume implementation | kurobe-implementer |
| Evidence-backed explanation of a failure | soei-investigator |
| Defects in a supplied change | hakuro-reviewer |
| Proof of requested behavior | ranga-verifier |
| Decide new coverage and test scope | shuna-test-triage |
| Reusable project verification procedure | kaijin-verification-builder |

Read only the selected procedure through the host's supported loader or an accessible sibling `../<name>/SKILL.md`. This invocation permits reading it for this task, subject to host restrictions. Report a missing procedure and continue under project guidance. Load another only when a distinct phase needs it.

## Coordinate

Resolve factual uncertainty from code, sources, and permitted checks. Ask JC for material product, cost, or authority decisions. Use supporting skills only for a concrete requirement.

Keep straightforward work here. When delegation is authorized and useful, give each worker a bounded goal, owned files, constraints, relevant context, and deliverable. Normally use at most two; honor configured roles and model settings. Use independent review when the change's risk or unresolved uncertainty justifies it and delegation is authorized. Wait for required results, release completed workers, and own integration.

## Completion

Finish with the requested result, observed evidence, and remaining gaps.
