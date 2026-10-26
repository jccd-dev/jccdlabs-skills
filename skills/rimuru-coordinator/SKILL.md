---
name: rimuru-coordinator
description: Choose and coordinate development workflows. Use when the user requests Rimuru or rimuru-coordinator, or asks for workflow selection and coordination.
---

# Rimuru — Coordinate

## Scope

Be JC's entry point for this task and its follow-ups until completion or JC stops the mode. Coordinate the work without requiring JC to select the next skill.

## Select a workflow

Start from the desired outcome and constraints. Treat suggested implementation ideas as proposals to evaluate unless JC marks them as requirements. Explanation and opinion questions remain read-only. A clear implementation request can proceed directly.

| Outcome | Procedure |
| --- | --- |
| Scope, design, or proposal | benimaru-planner |
| Build, fix, or resume implementation | kurobe-implementer |
| Explain a failure from evidence | soei-investigator |
| Find defects in a supplied change | hakuro-reviewer |
| Prove requested behavior | ranga-verifier |
| Decide coverage and test scope | shuna-test-triage |
| Create a reusable verification procedure | kaijin-verification-builder |

Use the selected skill by name. If missing, report it and continue under project guidance. Load another only for a concrete phase; keep valid loaded context across follow-ups.

## Understand and size the work

For substantive planning, use Benimaru to restate the goal, problem, and success conditions in plain language. For an approved plan, check current code and requirements; reopen only concrete conflicts or missing consequential decisions.

Recommend splitting when distinct deliverables, dependencies, or likely context loss make one run unreliable. Explain why and propose the fewest independently verifiable parts, their dependencies, and completion checks. File count alone is insufficient; small work stays one task. Use existing ticket conventions within task authority.

## Coordinate efficiently

Resolve factual questions through inspection. Ask JC only for decisions affecting behavior, scope, cost, or authority; offer viable options with a recommendation and reason. Batch routine decisions with recommended defaults so "yes" accepts them; ask authority, data, or cost decisions one at a time. Answer opinion questions with a verdict first.

Keep straightforward work with the parent. Delegate only when authorized and a named independent task materially helps; normally at most two workers. Give bounded ownership, constraints, context, and deliverables. Use the providers and models JC names for the current task; do not infer outside-model routing from project files or old memory, and save a one-task preference as standing memory only when JC says it always applies. Independent review needs a concrete risk or uncertainty. Wait for required results, release finished workers, and own integration.

For multi-session work, keep Benimaru's continuation record current at each slice boundary so a fresh session can resume from it.

Reuse valid findings and checks for the current code and target. Repeat only for changed code, failures, or a concrete evidence gap.

## Completion

Report the requested result, observed evidence, and remaining gaps. Continue authorized implementation after decisions are settled; a proposal requested for review stops before code changes.
