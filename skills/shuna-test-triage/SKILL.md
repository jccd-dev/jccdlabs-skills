---
name: shuna-test-triage
description: Decide whether changed behavior needs tests and choose the smallest meaningful scope. Use when the user requests Shuna or shuna-test-triage, or before adding, changing, or declining tests.
---

# Shuna: Test Scope

Choose coverage for a realistic failure, respecting explicit requests and project requirements.

## Establish the gap

- Name the changed observable contract, the plausible regression, and the existing assertion or check that would catch it. Read the assertions; a passing suite doesn't prove coverage.
- Reuse sufficient coverage. Extend an existing test before adding a case or harness. Add only a real gap, with expectations derived independently of the implementation.
- Reproduce bugs. For new behavior, cover contracts that could break silently. For behavior-preserving refactors, reuse coverage unless a concrete gap appears.
- Judge configuration, wiring, and visual edits by their effects, using builds, typechecks, lint, or visual inspection when sufficient. Avoid tests that mirror code or duplicate enforced invariants. When automated reproduction is unreliable, explain why and choose another check.
- When an existing end-to-end flow or using the app proves the behavior, check it that way instead of writing a test. Bug fixes still get a regression test when Kurobe's TDD rule applies.

## Choose the smallest faithful scope

- **Unit:** exercise real logic through its public interface when the failure needs no external boundary. Mocks must preserve the failure condition.
- **Integration:** use real participants when their interaction is the risk, such as persistence, routing, or serialization. Run against the app's real engine in a throwaway container or the project's compose setup, not an in-memory substitute. Isolate unrelated services.
- **End to end:** use the full UI or service path when the failure or request requires it. Extend existing journeys; duplicate lower-level coverage only for a distinct risk.

Use the existing harness and the fewest cases that catch the regression. Fidelity comes before speed: a test that can't fail for the bug is insufficient. Prefer no new test over a bad test.

Test through public interfaces and mock only external system boundaries. Derive expected values from the requirement or an independent source, never from the implementation's output, and write them as literals. Keep loops and branches out of tests; a table of cases is fine. Assert what the caller or user sees, not which internals were called.

Consider property tests when correctness depends on an invariant across many inputs, such as serialization round trips. Use the existing harness and ordinary examples when sufficient; add tooling only for a demonstrated need.

## Decide and verify

State once per behavior, grouping behaviors with the same decision:

`Test decision: <reuse | extend | add | none>, <scope when relevant> — <failure caught or why new coverage adds no signal>; misses: <material blind spot, when one exists>`

Reject a test that passes when the behavior breaks or fails when only internals change.

Revise when evidence changes the decision. Confirm a bug test fails for the intended defect when safe and practical, then passes with the fix. For a non-bug test, break the protected line once, watch the test fail, and undo the break; use mutation tools only on the user's request. Triage chooses coverage; the project's TDD procedure governs implementation order.

When an existing test fails, decide whether the code or the test is wrong before changing either, and state the evidence. Never weaken an assertion to make broken behavior pass.

## Finish

Run relevant existing checks within task permissions. Confirm targets and data effects before integration or end-to-end runs, and use local or disposable environments. Report unrun checks and persistent fixture data. Skipping a new test still requires appropriate verification.
