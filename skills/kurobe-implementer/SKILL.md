---
name: kurobe-implementer
description: Build, fix, or resume an authorized codebase change. Use when the user requests Kurobe or kurobe-implementer, or asks to implement a clear change, a plan, or a plan slice.
---

# Kurobe: Implement

Deliver the smallest complete change the request authorizes, without adjacent cleanup or speculative flexibility. When one fix is requested, make that fix and stop; note other problems in one line.

## Size the work first

Extra skill loads and review passes cost time and tokens, so scale the procedure to the risk.

- **Small, clear change** (one owner, obvious check, no data, auth, or concurrency risk): read the code, make the change, run the focused check, and report. Decide tests and self-review inline, without loading other skills. A bug fix still follows the TDD rule below.
- **Larger or risky change:** follow the sections below, loading `shuna-test-triage`, `ranga-verifier`, or `hakuro-reviewer` only for the part that needs it.

## Inspect and implement

1. With a plan file, read it, state the slice title, and work only that slice. Don't redo a ticked slice.
2. Read the owner, callers, project instructions, and existing coverage. Identify affected contracts, tests, fixtures, configuration, and exports. Reuse valid evidence when resuming.
3. Reproduce a bug before editing. Fix the shared cause at its owning boundary. Reuse existing architecture and dependencies; add an abstraction or dependency only for a current requirement. Preserve validation, error handling, and unrelated work.

## Tests

Use TDD for bug fixes when a failing test is cheap to write at a real public interface, and whenever the user says "use TDD". Running the fix by hand doesn't replace that test. Load the `tdd` skill when available. Otherwise write one behavioral test with an expectation derived independently of the code, watch it fail for the intended reason, implement just enough to pass, and repeat. Don't batch tests first. Claim a red-green cycle only when both were observed.

For other changes, state one test decision (reuse, extend, add, or none) and the failure it would catch. Prefer no new test over one that can't fail for the real bug. When an existing end-to-end flow or using the app proves the behavior, check it that way instead of adding a test.

## When a test fails

First decide and state which is wrong, the code or the test:

- **Code wrong:** fix the code. Never edit an assertion to make broken behavior pass.
- **Test wrong or stale:** name the evidence, such as the commit that removed the feature or the flawed setup, then fix the test.
- **Product decision:** if the test encodes behavior that was removed, possibly by mistake, ask the user first.

Fix failures the change caused and rerun until checks pass or a concrete blocker remains. Each retry must use evidence from the failure. After two failed fixes for the same symptom, test their shared assumption instead of patching again. Report unrelated failures separately.

## Verify

Run applicable typechecks and focused tests while working, and the full suite once at the end when safe. Map each requested behavior to observed evidence or a stated pending reason. For larger changes, check the diff for scope, data, authorization, and concurrency risks before finishing.

## Commands the user runs

When the user must run something, such as on a server or in a dashboard, give commands that work when pasted:

- Real values, not placeholders like `<app-container>`. For an unknown value, give the command that finds it first.
- Which user runs it and whether it needs `sudo`, matching the host's permissions.
- The expected output, and what to do if it differs.
- One step at a time when a step depends on earlier output.

## Finish

When a plan slice is verified, tick its checkbox and add one line of evidence (checks run, commit) in the same commit as the code, before the next slice. When every slice is done, say the plan file is ready to close and offer to remove it.

For work continuing in another session, give the code state, completed work, checks run, open findings, and next action.

End with the outcome, observed check results, and pending checks. Commits, pushes, and live-system actions follow the authority already given for the task.
