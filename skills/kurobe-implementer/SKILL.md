---
name: kurobe-implementer
description: Build, fix, or resume an authorized codebase change. Use when the user requests Kurobe or kurobe-implementer, or asks to implement a clear change or approved plan.
---

# Kurobe — Implement

## Scope

Deliver the smallest complete change authorized by the request. Derive completion from the requested behavior and project requirements; leave adjacent cleanup and speculative flexibility outside the change.

## Inspect and implement

1. Read the owner, callers, project instructions, and existing coverage. Identify affected contracts, tests, fixtures, configuration, and exports. Reuse valid evidence when resuming work.
2. For a bug, establish failure evidence before editing. Fix the shared cause at its owning boundary. Reuse existing architecture and dependencies. Add an abstraction or dependency only when a current requirement needs it. Enforce the relevant invariant in code or types when that prevents recurrence. Preserve validation, error handling, and unrelated work.

## Tests and TDD

Use `shuna-test-triage` before adding, changing, or declining tests. If unavailable, inspect existing assertions, name the realistic regression, and reuse or extend coverage only where a meaningful gap exists. State the test decision once. Follow project test requirements and permissions.

When TDD is requested or required, read an available TDD skill, such as `tdd`. If unavailable, use one behavior test at a time: observe failure for the intended reason, implement the minimum, and confirm it passes. Refactor only with green checks. Testing remains part of implementation when TDD is not selected.

## Verify and converge

For larger changes, verify useful increments before building further. Use `ranga-verifier` to prove the requested behavior; if unavailable, say so and map each acceptance condition to observed evidence or a pending reason.

Fix failures caused by the change and rerun until checks pass or a concrete blocker remains; each retry must address evidence from the failure. After two failed fixes for the same symptom, test the assumption they share instead of patching again. Report unrelated failures separately, then review the diff for scope and data, authorization, or concurrency risks.

## Completion

When unfinished work needs another session, update the existing continuation record using `benimaru-planner`'s handoff guidance. If unavailable, summarize the code state, completed work, checks, unresolved findings, and next action in the response.

Finish with the implemented outcome, observed check results, and precise pending checks. If the change settled a decision that is hard to reverse, surprising without context, and a real trade-off, propose a one-paragraph ADR in the same change. Commits and live-system actions follow the authority already established for the task.
