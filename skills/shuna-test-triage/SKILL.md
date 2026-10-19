---
name: shuna-test-triage
description: Decide whether changed behavior needs new test coverage and choose the smallest scope that catches its realistic failure. Use before adding, changing, or deciding against tests.
---

# Shuna — Test Scope

## Scope

Choose coverage for a realistic failure, respecting explicit requests and project requirements.

## Establish the gap

- Name the changed observable contract, plausible regression, and existing assertion or check that would detect it. Inspect assertions; a passing suite alone does not establish coverage.
- Reuse sufficient coverage. Extend an existing test before adding a separate case or harness. Add only a meaningful gap; derive expectations independently of the implementation.
- For bugs, reproduce the failure. For new behavior, cover contracts that could break silently. For behavior-preserving refactors, reuse coverage unless a concrete gap appears.
- Judge configuration, wiring, and visual edits by their effects. Use builds, typechecks, lint, or visual inspection when sufficient. Avoid tests that mirror code or duplicate enforced invariants. Explain unreliable automated reproduction and choose another check.

## Choose the smallest faithful scope

- **Unit:** Exercise real logic through its public interface when the failure requires no external boundary. Mocks must preserve the failure condition.
- **Integration:** Use real participants when their interaction is the risk, such as persistence, routing, or serialization. Isolate unrelated services.
- **End to end:** Use the full UI or service path when required by the failure or request. Extend existing journeys; duplicate lower-level coverage only for a distinct risk.

Use the existing harness and fewest cases that catch the regression. Fidelity comes before speed: a test that cannot fail for the bug is insufficient.

Consider property tests when correctness depends on an invariant across many inputs, such as serialization round trips. Use the existing harness and ordinary examples when sufficient; add tooling only for a demonstrated need.

## Decide and verify

State once per behavior; group behaviors sharing the same decision:

`Test decision: <reuse | extend | add | none>, <scope when relevant> — <failure caught or why new coverage adds no signal>`

Revise when evidence changes the decision. Confirm a bug test fails for the intended defect when safe and practical, then passes with the fix. Triage chooses coverage; the project's TDD procedure governs implementation order.

## Completion

Run relevant existing checks within task permissions. Confirm targets and data effects before integration or end-to-end execution; use local or disposable environments. Report unrun checks and persistent fixture data. Skipping a new test still requires appropriate verification.
