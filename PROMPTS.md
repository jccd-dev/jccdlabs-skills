# JCCDLabs Scenario Prompts

Copy the closest prompt, replace its brackets, and remove lines that do not apply. Supply facts you know; the agent should inspect missing technical details rather than make you design the solution. One suitable prompt is enough. You do not need to run every skill.

See the [usage guide](GUIDE.md) for each skill's purpose and adjustment guidance. These examples use ordinary skill names for Codex, Claude Code, OpenCode, and other Agent Skills-compatible harnesses. Short names such as "Use Kaijin" also match the descriptions. Install the skills for your harness first; native skill selectors remain available when you need explicit loading.

## Choose the situation

| Situation | Start with |
| --- | --- |
| Unsure which workflow fits | [Rimuru Coordinator](#rimuru-coordinator) |
| Need shared understanding, choices, or a plan | [Benimaru Planner](#benimaru-planner) |
| Ready to build, fix, or continue implementation | [Kurobe Implementer](#kurobe-implementer) |
| Need to understand why something fails | [Soei Investigator](#soei-investigator) |
| Need defects found in a particular change | [Hakuro Reviewer](#hakuro-reviewer) |
| Unsure which tests add value | [Shuna Test Triage](#shuna-test-triage) |
| Need proof that existing work meets the outcome | [Ranga Verifier](#ranga-verifier) |
| Need a reusable project verification procedure | [Kaijin Verification Builder](#kaijin-verification-builder) |

## State what the agent may do

- **Propose:** explain the approach and wait before implementation.
- **Check:** inspect and run permitted safe checks; keep application code unchanged.
- **Implement:** make the requested change and verify it.
- **Check and fix:** repair confirmed gaps required for the stated outcome; propose optional improvements separately.

These scopes still follow project requirements and established permissions. Publishing, deployment, credentials, and live data changes need their own applicable authority.

For a new agent taking over work, include the outcome, branch/PR or files, plan or handoff, current symptoms, and completed checks when available. Previous summaries are evidence to inspect. Verification must apply to the current code and target; missing proof stays pending.

## Rimuru Coordinator

Use Rimuru to choose the relevant procedure and manage transitions. A specialist procedure does not automatically require a separate agent.

### Start from an outcome, proposal first

```text
Use rimuru-coordinator.
Outcome: [what I should be able to do].
Problem: [why the current experience is inadequate].
Constraints: [requirements and limits].
Restate your understanding and propose the simplest approach before editing code.
Give me viable options and a recommendation for consequential decisions.
```

### Continue work started by another agent

```text
Use rimuru-coordinator to continue [feature/task].
Outcome: [desired result]. Existing work: [branch/PR/files and plan or handoff].
Inspect what is implemented, what remains, and which recorded checks still apply.
Complete the remaining authorized work and verify it. Reuse settled decisions,
preserve unrelated changes, and reopen planning only for concrete conflicts.
```

### Check whether a claimed completion solves the problem

```text
Use rimuru-coordinator.
Outcome: [desired result]. Problem: [problem this should solve].
Another agent reports completion in [branch/PR/files]. Evidence supplied: [if any].
Verify the current implementation against the outcome. Report what is met,
missing, incorrect, or unverified, with evidence and the smallest recommended fix.
Keep application code unchanged for now.
```

### Verify and fix confirmed gaps

```text
Use rimuru-coordinator.
Outcome: [desired result]. Existing work: [branch/PR/files].
Check the implementation, fix confirmed gaps needed for this outcome, and verify
the result on [safe local/disposable target, if known]. Preserve unrelated work.
Propose optional improvements separately. Report evidence and remaining limits.
```

### Evaluate improvements without starting a redesign

```text
Use rimuru-coordinator to assess [existing feature].
Outcome: [desired result]. Current difficulty: [specific example].
Determine whether this is a defect, missing behavior, or a usability improvement.
Recommend the smallest useful change and explain the tradeoff in plain language.
Give me options where a decision matters; wait before implementation.
```

**Expect:** appropriate routing, continuity, proportionate work, and clear evidence. If you request checking only, an implementation proposal should remain a proposal.

## Benimaru Planner

Use Benimaru when understanding or choices are unresolved. It should restate your goal and problem before developing the plan.

### Explore an outcome without prescribing the solution

```text
Use benimaru-planner.
I want [outcome] because [problem]. Constraints: [limits].
Restate my goal, the problem, and what success would look like.
Inspect the relevant code and recommend the smallest approach. Ask one important
decision at a time with viable options, your recommendation, and its reason.
Keep project code unchanged.
```

### Assess an existing plan or suggested approach

```text
Use benimaru-planner to assess [plan/reference].
The required outcome is [result]. Requirements: [non-negotiable constraints].
My suggested approach is [idea]; you may recommend a simpler alternative.
Reuse settled decisions. Explain concrete conflicts, missing decisions, and the
smallest necessary plan changes. Keep this a proposal before implementation.
```

### Decide whether the work should be split

```text
Use benimaru-planner for [outcome and current plan].
Assess the actual scope and dependencies before deciding whether to split it.
If one run would be unreliable, propose the fewest complete, independently
verifiable parts. For each, give the result, dependencies, and completion checks.
Make each understandable to a fresh agent. Keep small work as one task.
Draft the breakdown here; do not publish tracker issues yet.
```

**Expect:** shared understanding, justified choices, and a plan sized to the work. A ticket count or long document alone is not evidence of a good plan.

## Kurobe Implementer

Use Kurobe when implementation is authorized. It includes test selection and verification, so you usually do not need to request those skills separately.

### Implement an approved plan

```text
Use kurobe-implementer to implement [approved plan/reference].
Outcome: [required behavior]. Constraints: [limits].
Inspect current code and relevant coverage, then deliver the smallest complete
change. Reuse settled decisions and existing patterns. Fix failures caused by
the change and verify the result; report concrete blockers and unrun checks.
```

### Fix a known regression

```text
Use kurobe-implementer to fix [observed failure].
Expected: [behavior]. Actual: [behavior]. Reproduction or evidence: [details].
Establish the failure, inspect callers, and fix the shared cause at its owner.
Reuse or extend meaningful coverage for the regression. Preserve surrounding
behavior and valid assertions, then rerun the affected checks.
```

### Finish one part after a handoff

```text
Use kurobe-implementer to finish [specific slice] from [plan/ticket].
Current code: [branch/files]. Completed: [work and checks]. Remaining: [known gaps].
Inspect this state and complete only the named slice. Verify its outcome and
record the result and next action so another agent can continue the larger task.
```

### Use TDD for changed behavior

```text
Use kurobe-implementer with TDD for [behavior].
Use an available tdd skill or the implementation skill's fallback.
Choose meaningful coverage first. Work one behavior at a time: observe the test
fail for the intended reason, implement the minimum, and confirm it passes.
Refactor with green checks; avoid tests that merely mirror the implementation.
```

**Expect:** the authorized behavior, focused changes, and observed verification. Optional cleanup and hypothetical flexibility should stay outside the change.

## Soei Investigator

Use Soei to establish the cause before choosing a repair. These prompts authorize diagnosis, not application code edits.

### Investigate a reproducible failure

```text
Use soei-investigator to diagnose [failure].
Expected: [behavior]. Actual: [behavior]. Reproduction: [steps].
Relevant output and environment: [details, without secrets].
Trace the failure to its owning boundary. Report observations, likely cause,
confidence, and the smallest fix or next discriminating check. Keep code unchanged.
```

### Investigate an intermittent or slow path

```text
Use soei-investigator for [intermittent failure or slow behavior].
Observed conditions: [when it occurs]. Evidence: [logs/timings/examples].
Compare plausible causes using focused safe checks. Identify what changes between
successful and failing cases; do not guess a cause from one observation.
Keep code unchanged and report the evidence still needed.
```

### Reconcile conflicting results from agents or environments

```text
Use soei-investigator.
Agent/environment A reported [result, revision, target, command if known].
Agent/environment B reported [different result and context].
Inspect differences in code, fixtures, configuration, and execution conditions.
Explain the discrepancy or the next check that can distinguish its causes.
Keep application code unchanged; do not rerun unrelated checks.
```

**Expect:** a supported explanation or a precise unknown. If you want the supported fix implemented afterward, authorize that follow-up explicitly or ask Rimuru to diagnose and fix from the start.

## Hakuro Reviewer

Use Hakuro for a bounded diff review. Checking whether a complete feature meets an outcome belongs with Ranga or Rimuru.

### Review work produced by another agent

```text
Use hakuro-reviewer on [branch/PR/commit range] against [comparison base].
Intent: [problem and expected behavior]. Requirements: [plan/reference].
Find actionable defects introduced or affected by this change. Verify findings
against callers and contracts. Report severity, location, trigger, consequence,
and evidence. Keep the review read-only; state material limits if no defects appear.
```

### Re-review fixes without restarting the whole review

```text
Use hakuro-reviewer to review the fixes since [previously reviewed revision].
Prior findings: [references]. Current changes: [branch/commit range].
Check the fixes and affected behavior. Reopen resolved findings only with new
evidence. Report unresolved defects without repeating settled findings or
introducing unrelated cleanup. Keep the review read-only.
```

### Check whether a disputed finding is real

```text
Use hakuro-reviewer to assess this finding in [diff/reference]: [finding].
Inspect the actual caller contract, triggering condition, and existing checks.
Confirm a concrete defect or explain why the finding is unsupported or intentional.
State any uncertainty and the smallest confirming check. Do not edit code.
```

**Expect:** evidenced defects, useful corrections, and review that converges. To implement accepted fixes, hand the findings to Kurobe or authorize Rimuru to review and fix within the outcome.

## Shuna Test Triage

Use Shuna to decide which coverage has value. The prompts below request a decision, not permission to rewrite tests.

### Decide whether new coverage is needed

```text
Use shuna-test-triage for [change/diff and intended behavior].
Inspect existing assertions. Name the realistic regression and decide whether
to reuse coverage, extend a test, add a test, or add none.
Explain the smallest scope that can catch the failure and any other required
verification. Make a recommendation only; keep files unchanged.
```

### Choose unit, integration, or end-to-end scope

```text
Use shuna-test-triage for [failure or behavior].
The suspected risk is at [boundary, if known]. Existing harness: [if known].
Recommend the smallest faithful test scope. Explain what must be real, what may
be isolated, and whether mocks would hide the failure. Reuse the existing harness;
do not add tooling or edit tests in this assessment.
```

### Assess noisy, duplicate, or brittle tests

```text
Use shuna-test-triage to assess [specific tests] for [changed behavior].
Identify the contract each assertion protects and concrete duplication or coupling.
Recommend the smallest adjustment that preserves meaningful regression coverage.
Distinguish a defective test from a product defect. Propose changes before editing
or deleting assertions; do not treat a passing suite alone as proof of coverage.
```

**Expect:** one clear decision per behavior and a reason. Property tests are conditional on useful invariants; TDD determines implementation order rather than test scope.

## Ranga Verifier

Use Ranga to prove existing work against acceptance conditions. These prompts permit appropriate safe checks while keeping application code unchanged.

### Verify another agent's claimed completion

```text
Use ranga-verifier.
Outcome: [desired result]. Problem: [what this should solve].
Existing work: [branch/PR/files]. Acceptance conditions: [observable behaviors].
Verify the current implementation. Report each condition as passed, failed, or
pending, with code state, target, evidence, and limits. Keep application code
unchanged and recommend the smallest repair for confirmed gaps.
```

### Check behavior beyond a green build or test summary

```text
Use ranga-verifier on [feature/current revision].
Existing evidence: [commands, results, revision, target].
The behavior that matters is [user journey or contract]. Determine what the
existing checks actually establish and verify remaining gaps on [safe target].
Keep application code unchanged; report inaccessible or unrun checks as pending.
```

### Verify after a narrow follow-up change

```text
Use ranga-verifier after [new diff/revision].
Previous evidence: [revision, checks, target, results]. New behavior: [change].
Reuse evidence that still applies. Run required checks and focused verification
for invalidated or missing evidence; avoid repeating unrelated passing work.
Report results and remaining uncertainty. Keep application code unchanged.
```

**Expect:** proof tied to the current code and target, not an assurance based on another agent's summary. For verification plus repairs, use Rimuru's check-and-fix prompt.

## Kaijin Verification Builder

Use Kaijin to create or update a reusable project verification skill. These prompts authorize writing the procedure and exercising it within the stated permissions.

### Document a repeated verification journey

```text
Use kaijin-verification-builder for [project/feature].
Recurring journey: [behavior we repeatedly need to verify].
Reuse the existing harness and project skill location. Write a compact procedure
with prerequisites, confirmed commands, observable assertions, evidence, and cleanup.
Exercise one representative journey on [safe local/disposable target].
Report what was demonstrated and any exact blocker; keep credentials out of artifacts.
```

### Repair a stale verification procedure

```text
Use kaijin-verification-builder to update [existing verification skill/path].
What changed: [app/harness/environment change]. Failure evidence: [details].
Confirm the current commands and update only the affected procedure and references.
Exercise a representative safe journey and preserve its evidence before cleanup.
Report unverified sections; propose separately any missing harness work.
```

### Map verification for a complex feature

```text
Use kaijin-verification-builder for [complex feature and requirements].
Inspect existing coverage and reuse any feature-to-check map.
Create or update a small map from important behaviors to checks and known gaps,
and a reusable verification procedure. Distinguish required checks from conditional
ones. Demonstrate one representative safe journey; do not claim uncovered paths passed.
```

**Expect:** a usable procedure grounded in the actual project. Building a new harness is a separate scope decision when the existing one is insufficient.

## Short follow-ups you can use

| Situation | Follow-up |
| --- | --- |
| Options are too technical | "Explain this as a user decision. Give viable options, your recommendation, and its practical effect." |
| The agent misunderstood | "My goal is [outcome]; the problem is [problem]. Restate the corrected understanding before continuing." |
| Work is expanding | "Return to [outcome]. Explain which extra changes are required and leave optional improvements for later." |
| You approved a proposal | "Proceed with the recommended approach within the agreed scope." |
| Checks found a defect | "Fix this confirmed gap, preserve unrelated behavior, then rerun affected checks." |
| You need a handoff | "Record the current code state, completed work, evidence, unresolved decisions, and next action for a fresh agent." |
| Review is looping | "Identify the unresolved issue and new evidence. Reassess if another pass would repeat settled findings." |

Use specific outcomes rather than "make everything better." Avoid adding roles, ceremonies, or testing restrictions unless they serve this task. Keep the useful prompt short; add detail only when it changes a decision.
