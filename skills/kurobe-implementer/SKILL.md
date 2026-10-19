---
name: kurobe-implementer
description: Use when explicitly asked to build, fix, or resume an authorized change in a codebase.
---

# Kurobe — Implement

Deliver the smallest complete change authorized by the request. Derive completion from the requested behavior and project requirements; leave adjacent cleanup and speculative flexibility outside the change.

1. Read the owner, callers, project instructions, and existing coverage. Identify affected contracts, tests, fixtures, configuration, and exports. Reuse valid evidence when resuming work.
2. For a bug, establish failure evidence before editing. Fix the shared cause at its owning boundary. Reuse existing architecture and dependencies. Add an abstraction or dependency only when a current requirement needs it. Enforce the relevant invariant in code or types when that prevents recurrence. Preserve validation, error handling, and unrelated work.
3. Read `shuna-test-triage` before adding, changing, or declining tests, through the host loader or an accessible `../shuna-test-triage/SKILL.md`. If unavailable, inspect existing assertions, name the realistic regression, and reuse or extend coverage only where a meaningful gap exists. State the test decision once. Follow project test requirements and permissions.
   When TDD is requested or required, read an available TDD skill, such as `tdd`. If unavailable, use one behavior test at a time: observe failure for the intended reason, implement the minimum, and confirm it passes. Refactor only with green checks. Testing remains part of implementation when TDD is not selected.
4. Run required checks and focused behavior verification on confirmed safe targets. Fix failures caused by the change and rerun affected checks until they pass or a concrete blocker remains. Each retry must address evidence from the failure; if progress requires missing access, information, or scope, report that blocker. Preserve valid assertions; report unrelated failures separately. Once required checks pass, repeat only for new changes or concrete unresolved concerns. Then review the diff for scope and relevant data, authorization, or concurrency risks.

Finish with the implemented outcome, observed check results, and precise pending checks. Commits and live-system actions follow the authority already established for the task.
