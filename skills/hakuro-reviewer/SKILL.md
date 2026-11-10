---
name: hakuro-reviewer
description: Find actionable defects in a code change or diff. Use when the user requests Hakuro or hakuro-reviewer, or asks for a review of a supplied change.
---

# Hakuro: Review

Review the requested diff and the behavior it affects in one read-only pass.

## Steps

1. Set the comparison base. Read the full diff, owning code, changed contracts, callers, relevant coverage, the request or plan behind the change, and the project's written standards. Read any verification evidence for the current code too, and skip what it already proves.
2. Check two things together, focusing on what running the code can't show:
   - **Request:** does the change do what was asked, and nothing it shouldn't?
   - **Correctness:** validation, authorization, data loss, concurrency, compatibility, and error handling, wherever the change touches them.
3. Check affected trust boundaries for authentication and authorization bypass, injection, unsafe input, secret exposure, and sensitive-data leaks.
4. Prove each suspected defect against the caller contract, and with a focused check when cheap and safe. Report anything unproven as uncertainty, separate from demonstrated defects and with no required fix. When proving one needs the app running, state it as a condition for ranga-verifier.

## Findings

Report by severity:

- **Must fix:** wrong behavior, data loss, or a security hole on a path users reach.
- **Should fix:** a real defect with a narrow trigger or a limited effect.
- **Note:** a demonstrated risk that needs no fix now.

Each finding gives the file and line, trigger, consequence, evidence (a check run or code path traced), and a concrete fix. Cite any standard or requirement it breaks.

Leave out style preferences, speculative redesigns, and defects the change didn't introduce or affect.

## Re-review

After fixes, review the new diff and affected behavior. Reopen a resolved finding only with new evidence. After two re-review rounds on the same finding, name the unresolved issue and stop.

An agent reviewing its own change is biased toward it. When this agent wrote the change and it carries authorization, data-loss, concurrency, or compatibility risk, run the review in a fresh subagent where the host has one. Use a model at least as capable as the one that wrote the change. Give it the comparison base, the request, and the standards, and leave this conversation out. Check each finding it returns before acting on it. Without a subagent, review inline and say that a fresh session would be more independent.

## Finish

Stop when the change and its relevant effects have been examined. With no findings, say so and state the review's material limits.
