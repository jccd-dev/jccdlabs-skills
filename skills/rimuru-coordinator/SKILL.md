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
| File, check, or review a PR | shion-pr |
| Ship a change to a PR ready to merge | gobta-shipper |
| Multi-model review on request | octagram-council |
| Set up `.slime/config.md` for a repository | great-sage-setup |

Load a skill only when its phase starts, once per task. Name the transition in one line, such as "Plan agreed → Kurobe, slice 1." Skip unneeded phases: clear work goes straight to Kurobe, which sizes its own checks. If a skill is unavailable, say so and use project guidance. If the repository has no `.slime/config.md`, mention great-sage-setup once per task.

On risky work, verify before review, so review can focus on what running the code can't show.

Questions and opinion requests stay read-only: answer from evidence and list pending work instead of running it. A proposal requested for review stops before code. After approval, continue to implementation without a new interview.

When the request, docs, and code disagree, name the conflict instead of blending them.

## Ask like Benimaru

Look up facts directly. Ask the user only about behavior, scope, cost, or authority. Use the host's question tool when available, otherwise numbered questions with lettered choices. Give 2–4 real choices, recommended first, each with a reason tied to evidence. Ask data-loss, authority, and cost decisions one at a time.

## Keep it cheap

Stay in one agent for small work. Every subagent starts cold, re-reading the skill, project instructions, and code first. On small work that start-up cost exceeds the task, so a Haiku subagent can cost more than working inline with the parent model. Delegation saves money only when a large independent job returns a short result.

- When the user names a model or asks for delegation in this conversation ("use Sonnet 5.5 high", "use Haiku for the browser"), do it and confirm the model in one line.
- Follow standing delegation instructions for the host, such as T3 Code's `delegate_task`.
- Hakuro reviews a non-trivial change this agent wrote in a subagent with a fresh context window, because an author is biased toward its own work.
- Mechanical jobs with long output go to a subagent with a fresh context window on the cheapest model from this agent's provider (Haiku on Claude, Luna on Codex): mapping many files, running a full suite, lint, or build, and reading long logs. It reports facts; this agent decides.
- When the user already has an agent for the job, use it instead of a generic one.
- Pass pointers (paths, the diff command, the plan file) rather than pasted content.
- Otherwise delegate only for a large independent job, such as a long browser session, and give the reason in one line first.

A model or provider preference from an earlier session, including one saved in memory, applies only when the user said it always applies. Read [delegation preferences](references/delegation.md) before any dispatch; it covers models and host rules.

Reuse findings and checks that still hold for the current code. Repeat a check only after a change, a failure, or an evidence gap.

## Finish

Report the result, checks run, and anything pending. When the work belongs in a PR and the user asked for one, file it with shion-pr and run its check before merge.

For work continuing in another session, give a short handoff: revision and uncommitted changes, current slice or completed work, checks with results, open decisions, and next action. Save handoffs where `.slime/config.md` says if present, else in chat. Update an existing plan file or handoff instead of creating a new one; write a file only when authorized. On resume, compare the handoff with the current code before reusing its evidence.
