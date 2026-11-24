---
name: octagram-council
description: Have one or more strong models review, score, and improve the work round by round until they pass a target score or are satisfied. Use when the user requests Octagram, octagram-council, or a council.
---

# Octagram: Council

Each member works on the user's request and scores the result out of 10; the parent merges their findings, applies agreed fixes, and runs another round only when the round didn't pass. The user says what the council is for: a design, a plan, an architecture, a review, or anything else.

Each round costs one strong run per member. It pays off on frontend design and UX, plans and architecture, risky reviews (auth, payments, migrations), and large PRs. For a small fix, say it's overkill in one line and ask before running it.

## Members and target

Use the members the user names, else the Octagram section of `.slime/config.md`, else the latest flagship from each available provider at high effort (for example Claude Opus, GPT Sol, Gemini Pro). Any count of one or more works; don't add members to reach a number.

- Pass score: the user's target ("score 8"), else `Pass score` in the config. With no target, a round passes when every member says it is satisfied.
- Max rounds: the config's, else 3.
- In T3 Code, resolve the models with `orchestrator_capabilities`, then start one `delegate_task` per member in parallel.
- In Claude Code, the Claude desktop app, or any host where outside providers need permission, use outside providers only when the user explicitly asked for them in this conversation.
- If a named member is unavailable, say so and run with the rest; never substitute another model silently.

## Before the first round

Fix known issues, address outstanding comments, and run relevant checks, so members see the current work. Skip this when the user wants to discard the work and explore new ideas.

## Each round

1. Give each member the request, the goal and constraints, the relevant code or documents, and the checks already run. For visual work, give screenshots or the running URL; members can't judge UI from code alone.
2. Keep reviews read-only. Don't edit files while a member still reviews the same checkout.
3. Ask each member for a score out of 10, the reasons for it, and the changes that would raise it.
4. When a result arrives, check its findings against the code at once while the others run. If the user marked a member non-blocking, don't wait for it; treat a late result as feedback without a score.
5. Average the scores members gave. The round passes when the average meets the pass score, or, with no target, when every member is satisfied.
6. Report the round summary below before doing anything else.
7. If the round passed, stop. Otherwise apply the changes the parent agrees with and the request covers, then start the next round with a fresh review.

Stop when a round passes, the average stops rising, or max rounds is reached; say which.

Fight scope creep. Members will suggest more than the request needs. Reject additions outside the request and list them as follow-ups instead.

### Round summary

```markdown
### Round <n>: <average>/10, <passed | not passed> (target <pass score or "all satisfied">)

| Member | Score | Main points |
| --- | --- | --- |
| <member> | <score>/10 | <one line> |

Fixes applied: <list, or none>
Next: <stop, or what the next round checks>
```

Write `no score` when a member gave none, leave it out of the average, and never invent one.

## Final report

```markdown
## Council review

Result: <passed at round n | stopped at round n: scores stopped rising | max rounds reached>

| Member | Round 1 | … | Round n |
| --- | --- | --- | --- |
| <member> | <score>/10 | … | <score>/10 |
| Average | <avg>/10 | … | <avg>/10 |
```

Include only the members and rounds that actually ran. When the work ends in a PR, put this section in the PR description before the model line (shion-pr does this); edit an open PR's description rather than commenting. With no PR, put it in the final reply.

## Finish

Return the final report, the changes made, rejected suggestions as follow-ups, and unresolved disagreements. Release finished delegates through the host's completion or stop tools.
