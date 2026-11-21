---
name: octagram-council
description: Have three strong models from different providers review, score, and improve the work until they are satisfied. Use when the user requests Octagram, octagram-council, or a council.
---

# Octagram: Council

Three members from different providers each work on the user's request, score the result out of 10, and the parent merges their findings. Repeat until the members are satisfied or the round limit is reached. The user says what the council is for: a design, a plan, an architecture, a review, or anything else.

It costs three strong runs per round. It pays off on frontend design and UX, plans and architecture, risky reviews (auth, payments, migrations), and large PRs. For a small fix, say it's overkill in one line and ask before running it.

## Members

Read `.slime/config.md` if present for members, effort, allowed hosts, and max rounds. Otherwise use the user's named members, or the latest flagship from each of three providers at high effort (for example Claude Opus, GPT Sol, Gemini Pro), and 3 rounds.

- In T3 Code, resolve the models with `orchestrator_capabilities`, then start one `delegate_task` per member in parallel.
- In Claude Code, the Claude desktop app, or any host where outside providers need permission, run only when the user explicitly asked for these providers in this conversation.
- If three providers can't be reached or a named member is unavailable, report it instead of substituting.

## Before the first round

Fix known issues, address outstanding comments, and run relevant checks, so members see the current work. Skip this when the user wants to discard the work and explore new ideas.

## Each round

1. Give each member the request, the goal and constraints, the relevant code or documents, and the checks already run. For visual work, give screenshots or the running URL; members can't judge UI from code alone.
2. Keep reviews read-only. Don't edit files while a member still reviews the same checkout.
3. Ask each member for a score out of 10, the reasons for it, and the changes that would raise it.
4. When a result arrives, check its findings against the code at once while the others run. If the user marked a member non-blocking, don't wait for it; treat a late result as feedback without a score.
5. Merge the findings: agreements, disagreements, and the recommended next step. Apply the changes the parent agrees with and the request covers.

A fresh review after fixes starts a new round. Stop when every member is satisfied, the scores stop rising, or the round limit is reached; report which.

Fight scope creep. Members will suggest more than the request needs. Reject additions outside the request and list them as follow-ups instead.

## Report

```markdown
## Council review

Rounds: 2

| Member | Round 1 | Round 2 |
| --- | --- | --- |
| Claude Opus | 7/10 | 9/10 |
| GPT Sol | 8/10 | 10/10 |
| Gemini Pro | 7/10 | 9/10 |
```

Write `no score` when a member gave none; never invent one. When the work ends in a PR, put this section in the PR description before the model line (shion-pr does this); edit an open PR's description rather than commenting. With no PR, put it in the final reply.

## Finish

Return the table, the changes made, rejected suggestions as follow-ups, and unresolved disagreements. Release finished delegates through the host's completion or stop tools.
