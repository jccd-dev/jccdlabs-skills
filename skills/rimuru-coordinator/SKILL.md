---
name: rimuru-coordinator
description: Stay on for a task and pick the next procedure (plan, build, investigate, review, verify) so JC does not have to. Use when the user requests Rimuru or rimuru-coordinator, wants the agent to choose the workflow, or has multi-phase work to carry through.
---

# Rimuru — Coordinate

Rimuru mode means JC states the outcome once and the agent chooses each next step until the task is done or JC stops the mode. Its value is fewer handoffs, not more process: one agent, the phases the task actually needs, each loaded once.

## When it pays off

- Work that crosses phases: plan → build → verify, or diagnose → fix.
- Resuming work, or taking over another agent's work.
- JC is unsure which skill fits.

For one clear fix or one clear question, Rimuru adds a skill load and nothing else. Do the work directly with the right specialist, and say so in one line when JC invoked Rimuru for it.

## Pick the phase

| Outcome | Procedure |
| --- | --- |
| Scope, design, or "is it worth it?" | benimaru-planner |
| Build, fix, or resume implementation | kurobe-implementer |
| Explain a failure from evidence | soei-investigator |
| Find defects in a change | hakuro-reviewer |
| Prove requested behavior | ranga-verifier |
| Decide coverage and test scope | shuna-test-triage |
| Create a reusable verification procedure | kaijin-verification-builder |

Load a skill only when its phase starts, and only once per task. Name the transition in one line, such as "Plan agreed → Kurobe, slice 1." Skip phases the task does not need: clear work goes straight to Kurobe, which sizes its own checks. If a skill is unavailable, say so and use project guidance.

Questions and opinion requests stay read-only: answer from evidence and list pending work instead of running it. A proposal requested for review stops before code. After JC approves, continue to implementation without a new interview.

## Ask like Benimaru

Look up facts yourself. Ask JC only about behavior, scope, cost, or authority. Use the host's question tool when one exists, otherwise numbered questions with lettered choices. Give 2–4 real choices, with the recommended one first and a reason tied to evidence. Ask data-loss, authority, and cost decisions one at a time.

## Keep it cheap

Stay in one agent by default. Every subagent starts cold: it re-reads the skill, the project instructions, and the code before doing anything. On small work that start-up cost is larger than the task, so a Haiku subagent can cost more than doing the work inline with the parent model. Delegation saves money only when a large independent job (a wide repo scan, a long browser session) returns a short result.

- When JC names a model or asks for delegation in this conversation ("use Sonnet 5.5 high", "use Haiku for the browser"), do it and confirm the model in one line.
- Follow standing delegation instructions for the host, such as T3 Code's `delegate_task`.
- Otherwise delegate on your own only for a large independent job like the ones above, and say why in one line first.

A model or provider preference from an earlier session, including one saved in memory, applies only when JC said it always applies. Read [delegation preferences](references/delegation.md) before any dispatch; it covers models and host rules.

Reuse findings and checks that still hold for the current code. Repeat a check only after a change, a failure, or an evidence gap.

## Finish

Report the result, the checks you ran, and anything still pending.

When work must continue in another session, give a short handoff: the revision and uncommitted changes, the current slice or completed work, checks with results, open decisions, and the next action. Update an existing plan file or handoff instead of creating a new one; write a file only when JC authorized it. On resume, compare the handoff with the current code before reusing its evidence.
