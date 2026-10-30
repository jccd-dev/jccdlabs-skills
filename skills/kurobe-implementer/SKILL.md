---
name: kurobe-implementer
description: Build, fix, or resume an authorized codebase change. Use when the user requests Kurobe or kurobe-implementer, or asks to implement a clear change, a plan, or a plan slice.
---

# Kurobe — Implement

## Scope

Deliver the smallest complete change the request authorizes. Leave adjacent cleanup and speculative flexibility out. When JC asks for one fix, fix that and stop; mention other problems you noticed in one line instead of fixing them.

## Size the work first

The procedure scales with risk, because extra skill loads and review passes cost time and tokens on work that does not need them.

- **Small, clear change** (one owner, obvious check, no data, auth, or concurrency risk): read the code, make the change, run the focused check, and report. Do the test decision and self-review inline; do not load other skills.
- **Larger or risky change:** follow the full sections below and load `shuna-test-triage`, `ranga-verifier`, or `hakuro-reviewer` only for the part that needs it.

## Inspect and implement

1. When working from a plan file, read it, state the slice title, and work only that slice. Do not redo a slice already ticked.
2. Read the owner, callers, project instructions, and existing coverage. Identify affected contracts, tests, fixtures, configuration, and exports. Reuse valid evidence when resuming.
3. For a bug, reproduce it before editing. Fix the shared cause at its owning boundary. Reuse existing architecture and dependencies; add an abstraction or dependency only when a current requirement needs it. Preserve validation, error handling, and unrelated work.

## Tests

Use TDD for bug fixes when a failing test is cheap to write at a real public interface, and whenever JC says "use TDD". Load the available `tdd` skill when present. Otherwise: write one behavioral test with an expectation derived independently of the code, watch it fail for the intended reason, implement only enough to pass, and repeat. Do not write a batch of tests first. Claim a red–green cycle only when you observed both.

For other changes, state one test decision (reuse, extend, add, or none) with the failure it would catch. Prefer no new test over a test that cannot fail for the real bug. When an existing end-to-end flow or using the app proves the behavior, check it that way instead of adding a test.

## When a test fails

First decide which is wrong, the code or the test, and say so before editing:

- **Code wrong:** fix the code. Never edit an assertion to make a broken behavior pass.
- **Test wrong or stale:** name the evidence, such as the commit that removed the feature or the flawed setup, then fix the test.
- **Product decision:** if the test encodes behavior that was removed, possibly by mistake, ask JC before choosing.

Fix failures caused by the change and rerun until checks pass or a concrete blocker remains; each retry must address evidence from the failure. After two failed fixes for the same symptom, test the assumption they share instead of patching again. Report unrelated failures separately.

## Verify

Run applicable typechecks and focused tests while working, and the full suite once at the end when it is safe. Map each requested behavior to observed evidence or a stated reason it is pending. For larger changes, review the diff for scope, data, authorization, and concurrency risks before finishing.

## Commands JC runs

When JC must run something, such as on a server or in a dashboard, give commands that work when pasted:

- Real values, not placeholders like `<app-container>`. When a value is unknown, give the command that finds it first.
- Which user runs it and whether it needs `sudo`, matching the host's actual permissions.
- The expected output, and what to do if it differs.
- One step at a time when a step depends on the previous output.

## Completion

When a plan slice is verified, tick its checkbox and add one line of evidence (checks run, commit) in the same commit as the code, before starting the next slice. When every slice is done, say the plan file is ready to close and offer to remove it.

If work must continue in another session, give the code state, completed work, checks run, open findings, and the next action.

Finish with the outcome, observed check results, and any pending checks. Commits, pushes, and live-system actions follow the authority already given for the task.
