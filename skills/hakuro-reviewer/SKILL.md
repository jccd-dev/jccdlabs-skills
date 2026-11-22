---
name: hakuro-reviewer
description: Find actionable defects in a code change or diff, or audit code comments. Use when the user requests Hakuro or hakuro-reviewer, asks for a review of a supplied change, or asks to audit or clean up comments.
---

# Hakuro: Review

Review the requested diff and the behavior it affects in one read-only pass.

## Steps

1. Set the comparison base. Read the full diff, owning code, changed contracts, callers, relevant coverage, the request or plan behind the change, and the project's written standards. Read any verification evidence for the current code too, and skip what it already proves.
2. Check two things together, focusing on what running the code can't show:
   - **Request:** does the change do what was asked, and nothing it shouldn't?
   - **Correctness:** validation, authorization, data loss, concurrency, compatibility, and error handling, wherever the change touches them.
3. Check affected trust boundaries for authentication and authorization bypass, injection, unsafe input, secret exposure, and sensitive-data leaks. In each changed file, list user inputs, database queries, auth checks, session state, external calls, and cryptography first. Report a security finding only when the value is attacker-controlled: request data, headers, unsigned cookies, URL segments, uploads, or other users' stored content. Settings, environment variables, and constants are not, and neither are patterns the framework already mitigates, such as auto-escaped templates or parameterized ORM queries. When a `security-review` skill is installed and the change touches a trust boundary, load it for this step.
4. Sort each comment the change adds or leaves behind as a tautology (repeats the code), excuse (covers a hack), stale (describes code that changed), or decision record (a non-obvious why). An excuse is a should-fix finding against the hack it covers; a tautology or stale comment is a note. Apply the comment policy in `.slime/config.md` if present; the default is why-only.
5. Prove each suspected defect against the caller contract, and with a focused check when cheap and safe. Report anything unproven as uncertainty, separate from demonstrated defects and with no required fix. When proving one needs the app running, state it as a condition for ranga-verifier.

## Findings

Report by severity:

- **Must fix:** wrong behavior, data loss, or a security hole on a path users reach.
- **Should fix:** a real defect with a narrow trigger or a limited effect.
- **Note:** a demonstrated risk that needs no fix now.

Each finding gives the file and line, trigger, consequence, evidence (a check run or code path traced), and a concrete fix. Cite any standard or requirement it breaks.

Leave out style preferences, speculative redesigns, and defects the change didn't introduce or affect.

## Comment audit

When asked to audit comments in a folder or the repository, sort every comment into the four kinds above, then:

- Delete tautologies and stale comments.
- Delete excuses and list each hack as a follow-up. File issues only when the user asks.
- List decision records with a recommended home (ADR, commit note, or keep under why-only) and move them after the user chooses.
- Report counts per kind and lines removed.

Leave license headers, directives (`eslint-disable`, `@ts-expect-error`, type annotations in comments), and generated files alone. A lint rule banning comments is per-repository tooling; recommend it only when comments keep returning after cleanup.

## Re-review

After fixes, review the new diff and affected behavior. Reopen a resolved finding only with new evidence. After two re-review rounds on the same finding, name the unresolved issue and stop.

An agent reviewing its own change is biased toward it. When this agent wrote the change and it is more than a few lines in one file, or carries authorization, data-loss, concurrency, or compatibility risk, run the review in a subagent with a fresh context window where the host has one. Use a model at least as capable as the one that wrote the change. Give it pointers, not this conversation: the comparison base or diff command, the request or plan file, and the standards files. Check each finding it returns before acting on it. Without a subagent, review inline and say that a fresh session would be more independent.

## Finish

Stop when the change and its relevant effects have been examined. List the files read and the areas that couldn't be verified. With no findings, say so and state the review's material limits.
