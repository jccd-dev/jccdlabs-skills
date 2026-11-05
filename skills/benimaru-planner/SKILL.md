---
name: benimaru-planner
description: Reach shared understanding of a goal and problem, ask the decisions that matter with recommended choices, then plan. Use when the user requests Benimaru or benimaru-planner, asks for a plan or proposal before code, or wants to decide whether something is worth building.
---

# Benimaru: Plan

The user and agent must understand the same outcome and problem before anyone proposes a solution. A plan built on a misread goal wastes the whole implementation, so the approach comes last.

Keep project code read-only. Write a plan file only on request.

## 1. Understand

Restate briefly, without copying the request:

- **Outcome:** what should be true when this is done.
- **Problem:** what is wrong or missing today, and for whom.
- **Done when:** the observable check that proves it works. It must be runnable; if it can't be run cheaply, the first slice creates a way to run it.

Mark assumptions. Treat the user's implementation ideas as suggestions to evaluate unless stated as requirements. When the request, docs, and code disagree, name the conflict instead of blending them.

Then read the relevant code, docs, and callers. Find facts directly: if a read or command can answer it, don't ask. Ask the user only about intent, scope, behavior, cost, or authority.

## 2. Ask before proposing

Before recommending an approach, list the open decisions that could change the approach, its scope, or its main risk. If none remain, say so in one line and continue.

Otherwise ask them, at most four per round:

- Use the host's question tool when available, otherwise numbered questions with lettered choices.
- Give each question 2–4 real choices, recommended first and marked "(Recommended)".
- Justify each choice briefly with evidence: the code, a stated constraint, or a cost. Every choice must be a workable answer to the same question; drop filler.
- Ask data-loss, authority, and significant-cost decisions on their own.

Wait for the answers. Ask another round only when an answer opens a new consequential decision. Reuse settled answers; reopen one only for new evidence, and say what changed.

## 3. Recommend

Lead with the verdict. For "is it worth it?" or "should we?", answer yes or no first, then why.

Recommend the simplest approach that meets the outcome, reusing existing patterns and dependencies. Name the main alternative and why it lost. Include affected areas, data or migration effects, and the main failure risk when they matter.

When the uncertainty is something the user could see rather than answer, such as how a UI feels or whether a state model holds, suggest a throwaway prototype if authorized.

## 4. Plan

Scale detail to the task. Small work gets a few lines.

- Ordered steps, each with the check that proves it.
- For work too large for one reliable session, split it into the fewest slices that can each be built and checked alone. Give each an outcome, dependencies, and completion check.

To save the plan, write one Markdown file at the requested path, or under `docs/plans/YYYY-MM-DD-<slug>.md` by default, with a checkbox per slice for implementation to tick:

```markdown
# <Title>

Outcome: …
Problem: …
Done when: …
Decisions: <question → answer, one line each>

## Slices
- [ ] 1. <outcome> — check: <command or observation>
- [ ] 2. <outcome> — depends on 1 — check: …
```

## Finish

A plan requested for review ends in the conversation. If implementation was already authorized, hand off the agreed plan without a new interview.
