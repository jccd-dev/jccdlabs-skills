---
name: rimuru-coordinator
description: Stay on for a task and pick the next procedure (plan, build, investigate, review, verify) so the user does not have to. Use when the user requests Rimuru or rimuru-coordinator, wants the agent to choose the workflow, or has multi-phase work to carry through.
---

# Rimuru: Coordinate

In Rimuru mode the user states the outcome once and the agent chooses each next step until the task is done or the user stops the mode. The value is fewer handoffs: one agent, only the phases the task needs, each loaded once.

## When it pays off

- Work that crosses phases: plan → build → verify, or diagnose → fix.
- Resuming work, or taking over another agent's work.
- The user is unsure which skill fits.

For one clear fix or question, Rimuru adds only a skill load. Do the work directly with the right specialist, and say so in one line if Rimuru was invoked.

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

Load a skill only when its phase starts, once per task. Name the transition in one line, such as "Plan agreed → Kurobe, slice 1." Skip unneeded phases: clear work goes straight to Kurobe, which sizes its own checks. If a skill is unavailable, say so and use project guidance.

On risky work, verify before review, so review can focus on what running the code can't show.

Questions and opinion requests stay read-only: answer from evidence and list pending work instead of running it. A proposal requested for review stops before code. After approval, continue to implementation without a new interview.

When the request, docs, and code disagree, name the conflict instead of blending them.

## Ask like Benimaru

Look up facts directly. Ask the user only about behavior, scope, cost, or authority. Use the host's question tool when available, otherwise numbered questions with lettered choices. Give 2–4 real choices, recommended first, each with a reason tied to evidence. Ask data-loss, authority, and cost decisions one at a time.

## Keep it cheap

Stay in one agent by default. Every subagent starts cold, re-reading the skill, project instructions, and code first. On small work that start-up cost exceeds the task, so a Haiku subagent can cost more than working inline with the parent model. Delegation saves money only when a large independent job (a wide repo scan, a long browser session) returns a short result.

- When the user names a model or asks for delegation in this conversation ("use Sonnet 5.5 high", "use Haiku for the browser"), do it and confirm the model in one line.
- Follow standing delegation instructions for the host, such as T3 Code's `delegate_task`.
- Otherwise delegate only for a large independent job like those above, and give the reason in one line first.

A model or provider preference from an earlier session, including one saved in memory, applies only when the user said it always applies. Read [delegation preferences](references/delegation.md) before any dispatch; it covers models and host rules.

Reuse findings and checks that still hold for the current code. Repeat a check only after a change, a failure, or an evidence gap.

## Finish

Report the result, checks run, and anything pending.

For work continuing in another session, give a short handoff: revision and uncommitted changes, current slice or completed work, checks with results, open decisions, and next action. Update an existing plan file or handoff instead of creating a new one; write a file only when authorized. On resume, compare the handoff with the current code before reusing its evidence.
