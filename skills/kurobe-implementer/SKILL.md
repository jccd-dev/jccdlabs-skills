---
name: kurobe-implementer
description: Build, fix, or resume an authorized codebase change. Use when the user requests Kurobe or kurobe-implementer, or asks to implement a clear change or approved plan.
---

# Kurobe — Implement

## Scope

Deliver the smallest complete change authorized by the request. Derive completion from the requested behavior and project requirements; leave adjacent cleanup and speculative flexibility outside the change.

## Inspect and implement

1. For a ticket reference, fetch its full body and comments, or read the local ticket file, and state its title before starting. Follow its spec or handoff reference, reading its body and relevant comments; for local tickets also inspect the feature directory and configured spec location. Resolve ambiguous references before proceeding. Inspect both native blocking edges and any textual `Blocked by` list; reconcile contradictions and establish each blocker's status. A blocker is done when the tracker records a completed resolution, or a local ticket has Status done with completion evidence. Cancelled or not planned alone, unknown status, and conflicts remain pending. Do not reimplement a completed current ticket without a request. Work only an authorized, ready ticket; report blockers, their status, and ready authorized options without assuming authority to implement blockers. Do not modify the parent issue. Tracker mutations and commits require established authority.
2. Read the owner, callers, project instructions, and existing coverage. Identify affected contracts, tests, fixtures, configuration, and exports. Reuse valid evidence when resuming work. For wide refactors, preserve the ticket sequence: expand, migrate batches, then contract; where batches cannot stay green independently, use the authorized integration branch and final integration verification.
3. For a bug, establish failure evidence before editing. Fix the shared cause at its owning boundary. Reuse existing architecture and dependencies. Add an abstraction or dependency only when a current requirement needs it. Enforce the relevant invariant in code or types when that prevents recurrence. Preserve validation, error handling, and unrelated work.

## Tests and TDD

Use `shuna-test-triage` before adding, changing, or declining tests. If unavailable, inspect existing assertions, name the realistic regression, and reuse or extend coverage only where a meaningful gap exists. State the test decision once. Triage chooses coverage; it does not bypass the TDD sequence. Follow project test requirements and permissions.

Use TDD by default for behavior changes from a spec or tickets, and whenever requested or required. Load the available `tdd` skill using the host's skill mechanism and follow it. Before proposing or writing tests, follow the spec or handoff to find public seams and explicit user confirmation; otherwise identify seams with what each catches and misses and confirm them with the user. An approved document must identify the explicit confirmation; generic spec approval, module names, a label, ticket, or unconfirmed proposal alone is not confirmation.

If `tdd` is unavailable, report that and use its portable loop: at a confirmed seam, write one behavioral test with an independently derived expectation; observe it fail for the intended reason, implement only enough to pass, and repeat. Test through public interfaces, mocking only external system boundaries. Do not write a batch of tests first. Refactoring belongs to review after the red–green cycles.

Reuse a sufficient existing regression test: observe its intended failure before editing and its pass afterward. Claim a red–green cycle only when both were observed. If no meaningful test is needed, run appropriate checks and report the evidence without claiming a cycle. If a meaningful test is needed but a seam cannot be confirmed or the intended red cannot be observed safely, leave that behavior pending and report the blocker. Prose or configuration changes may need checks rather than new tests. Direct small work without a spec or tickets follows project requirements and any requested TDD procedure.

## Verify and converge

Run applicable safe typechecks and focused tests during implementation, and the full suite once at the end when applicable and safe. On an authorized shared integration-branch batch that cannot independently stay green, use scoped checks and identify expected cross-batch failures pending the final integrate-and-verify ticket; full green is required there. For larger changes, verify useful increments before building further. Use `ranga-verifier` to prove the requested behavior; if unavailable, say so and map each acceptance condition to observed evidence or a pending reason.

Fix failures caused by the change and rerun until checks pass or a concrete blocker remains; each retry must address evidence from the failure. For the integration-branch exception, record expected cross-batch failures instead of chasing work assigned to other batches. After two failed fixes for the same symptom, test the assumption they share instead of patching again. Report unrelated failures separately. Review through `hakuro-reviewer` or the project's relevant review procedure, including scope and data, authorization, or concurrency risks. Apply necessary refactoring at this review stage and recheck affected behavior.

## Completion

For a verified ticket, record acceptance and check results and mark the selected local ticket Status done or tracker ticket completed within existing authority. In the selected local ticket, tick only acceptance criteria observed to be met and append check results and code state. For integration batches distinguish scoped batch acceptance from final integration acceptance. If the status update or evidence cannot be recorded with authority, report the exact pending update and provide durable continuation evidence needed next session; never edit the parent issue for this. When unfinished work needs another session, update the existing continuation record using `benimaru-planner`'s handoff guidance. If unavailable, summarize the code state, completed work, checks, unresolved findings, and next action in the response. At final ticket completion, report that the shared spec or continuation record is ready to close; retain it until authorized to close it.

Finish with the implemented outcome, observed check results, and precise pending checks. If the change settled a decision that is hard to reverse, surprising without context, and a real trade-off, propose a one-paragraph ADR in the same change. Commits and live-system actions follow the authority already established for the task.
