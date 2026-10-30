---
name: hakuro-reviewer
description: Find actionable defects in a code change or diff. Use when the user requests Hakuro or hakuro-reviewer, or asks for a review of a supplied change.
---

# Hakuro — Review

## Scope

Review the requested diff and the behavior it affects, in one pass. Keep the review read-only.

## Workflow

1. Establish the comparison base. Read the full diff, the owning code, changed contracts, callers, and relevant coverage. Read the request or plan the change was meant to satisfy, and the project's written standards.
2. Check two things together:
   - **Request:** does the change do what was asked, and nothing it should not?
   - **Correctness:** validation, authorization, data loss, concurrency, compatibility, and error handling, wherever the change touches them.
3. Check affected trust boundaries for authentication and authorization bypass, injection, unsafe input, secret exposure, and sensitive-data leaks.
4. Prove each suspected defect before reporting it: check it against the caller contract, and run a focused check when that is cheap and safe. Separate demonstrated defects from uncertainty.

## Findings

Report findings by severity. Each one gives the file and line, the triggering condition, the consequence, the evidence (a check you ran or the code path you traced), and a concrete fix. Cite the standard or requirement it breaks when one applies.

Leave out style preferences, speculative redesigns, and defects the change did not introduce or affect.

## Re-review

After fixes, review the new diff and affected behavior. Reopen a resolved finding only with new evidence. If rounds repeat without progress, name the unresolved issue instead of producing more edits.

An agent reviewing its own change is biased toward it. For a consequential change, say when a fresh session would give a more independent review.

## Completion

Stop when the change and its relevant effects have been examined. If there are no findings, say so and state the material limits of the review.
