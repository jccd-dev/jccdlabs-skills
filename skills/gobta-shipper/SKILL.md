---
name: gobta-shipper
description: Take a change from finished code to a PR ready to merge without stopping between steps, then stop at the merge gate. Use when the user requests Gobta or gobta-shipper, or says to ship a change.
---

# Gobta: Ship

Carry a change through proof, review, push, and PR without asking between steps. Stop when the PR is ready to merge.

## Permission

Invoking Gobta authorizes, for this change only: creating a branch, committing, pushing that branch, `git push --force-with-lease` on that branch only, and opening or updating its PR. It never authorizes merging, pushing to the base branch, deploying, or changing live data. Read `.slime/config.md` if present for checks, base branch, reviewer, and who merges.

Ask questions with the host's question tool, and only when a step can't continue without the user.

## Steps

1. If the work isn't finished, finish it with kurobe-implementer. On the base branch, create a branch first.
2. Prove it with ranga-verifier. On a failure, fix and rerun; after two failed fixes for the same symptom, stop and report.
3. Review it with hakuro-reviewer in a fresh subagent. Use octagram-council instead when the user asked for it or the config allows it for this kind of change. Fix must-fix findings and return to step 2.
4. Commit and push the branch.
5. File the PR with shion-pr, including the evidence from step 2 and any council table.
6. Run shion-pr's check before merge. Fix what this change caused and repeat from step 2.
7. Stop at **ready**. Report the PR URL, checks, and review result. Merge only when the user says to.

If a check fails for a reason this change didn't cause, report it and stop instead of fixing unrelated code.
