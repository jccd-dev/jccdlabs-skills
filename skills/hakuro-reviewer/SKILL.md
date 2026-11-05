---
name: hakuro-reviewer
description: Find actionable defects in a code change or diff. Use when the user requests Hakuro or hakuro-reviewer, or asks for a review of a supplied change.
---

# Hakuro: Review

Review the requested diff and the behavior it affects in one read-only pass.

## Steps

1. Set the comparison base. Read the full diff, owning code, changed contracts, callers, relevant coverage, the request or plan behind the change, and the project's written standards.
2. Check two things together, focusing on what running the code can't show:
   - **Request:** does the change do what was asked, and nothing it shouldn't?
   - **Correctness:** validation, authorization, data loss, concurrency, compatibility, and error handling, wherever the change touches them.
3. Check affected trust boundaries for authentication and authorization bypass, injection, unsafe input, secret exposure, and sensitive-data leaks.
4. Prove each suspected defect against the caller contract, and with a focused check when cheap and safe. Report anything unproven as uncertainty, separate from demonstrated defects and with no required fix.

## Findings

Report by severity. Each finding gives the file and line, trigger, consequence, evidence (a check run or code path traced), and a concrete fix. Cite any standard or requirement it breaks.

Leave out style preferences, speculative redesigns, and defects the change didn't introduce or affect.

## Re-review

After fixes, review the new diff and affected behavior. Reopen a resolved finding only with new evidence. If rounds repeat without progress, name the unresolved issue instead of producing more edits.

An agent reviewing its own change is biased toward it. For a consequential change, say when a fresh session would give a more independent review.

## Finish

Stop when the change and its relevant effects have been examined. With no findings, say so and state the review's material limits.
