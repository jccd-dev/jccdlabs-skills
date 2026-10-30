# JCCDLabs Skills Guide

## Start here

Use **Rimuru** when you want the agent to choose the workflow. You do not need to remember all eight skills or run them in sequence. Mention a specialist directly when you already know the job.

Describe the outcome, the problem, and real constraints. Let the agent recommend an implementation. If you already have an idea, say whether it is a requirement or a suggestion it may challenge.

You do not need a long prompt. Add the details that matter:

```text
Use rimuru-coordinator.
Outcome: let me find notes I recently worked on.
Problem: I lose track of useful notes between sessions.
Constraints: reuse existing search; no new dependency unless necessary.
First propose the simplest approach. Give me options for decisions I need to make.
```

That request asks for a proposal. To authorize building from the start, say "Build this feature" and state its expected behavior. Planning is optional when the work is already clear.

The examples use ordinary skill names, without `$` or `/`. You can also use the short character name, such as "Use Rimuru" or "Use Kaijin." Install the collection in your harness's supported skill location first. Codex, Claude Code, OpenCode, and other Agent Skills-compatible harnesses can select skills from their names and descriptions; host settings and model decisions still govern loading. Use a native skill selector when you need explicit loading. These skills are procedures, not a requirement to launch separate agents.

## Everyday use

| Your situation | What to say | What to expect |
| --- | --- | --- |
| You know the outcome but need an approach | "Use rimuru-coordinator. I want [outcome] because [problem]. Recommend the simplest approach and give me choices for consequential decisions." | A plain-language understanding, inspection of relevant code, and a recommendation. |
| You want a proposal before implementation | "Use benimaru-planner. Plan [outcome] first." | Your goal and problem restated, open decisions asked with recommended choices, then a recommendation and plan; code unchanged. |
| You want the agent to build a clear feature | "Use rimuru-coordinator to build [behavior]. Respect [constraints]. Ask only about decisions that affect the result." | The appropriate procedure and implementation, with meaningful checks. |
| You approved a plan | "Use kurobe-implementer. Implement [plan reference]. Reassess only concrete conflicts; reuse settled decisions." | Implementation without a fresh planning interview. |
| Work is unfinished | "Use rimuru-coordinator to resume [task]. Here is the current state, completed checks, and remaining work: [details]." | Reuse of valid findings; checks repeated only when needed. |
| The task may span several sessions | "Use benimaru-planner. Assess the actual scope. If one run would be unreliable, recommend the fewest independently verifiable parts." | A justified breakdown, dependencies, and completion conditions. |
| The agent is drifting | "Return to [requested outcome]. Explain why the additional work is necessary, and leave optional improvements for later." | A scope correction and a clear next action. |

After a proposal, "Proceed with the recommended approach" authorizes implementation within the agreed scope. You do not need to choose Kurobe yourself when Rimuru is coordinating.

## Scenario prompts

Use the [copyable scenario prompts](PROMPTS.md) for starting a feature, taking over another agent's work, checking claimed completion, fixing confirmed gaps, reviewing changes, choosing tests, and building verification procedures. Each skill has several examples with explicit editing authority and expected results.

## When to use each skill

### Rimuru Coordinator — choose and coordinate

**Use when:** the task crosses phases (plan → build → verify, or diagnose → fix), you are resuming or taking over work, or you are unsure which skill fits. Rimuru mode stays on until the task is done or you stop it.

**Skip it when:** you have one clear fix or one clear question. Ask Kurobe or the specialist directly; Rimuru would only add a skill load.

**Example:** "Use rimuru-coordinator to add saved search filters. First understand the outcome, then build the simplest version using our existing search."

**Expected result:** one agent that loads only the phases the task needs, each once, and names each transition in one line ("Plan agreed → Kurobe, slice 1"). Questions come with choices and a recommendation, like Benimaru's.

**Why it can cost more:** every subagent starts cold and re-reads the skill, project instructions, and code. On small work that start-up cost is larger than the task, so a Haiku subagent can cost more than the parent doing it inline. Rimuru delegates only when you ask in the conversation, when a standing host rule says so (T3 Code's `delegate_task`), or for a large independent job that returns a short result, and it says why first.

**Adjust when:** it loads every workflow, repeats planning, asks which skill to use next, or delegates without explaining the benefit. Request the specific correction; record repeated failures before changing the skill.

### Benimaru Planner — understand and decide

**Use when:** the desired result or approach needs discussion, choices have meaningful tradeoffs, or you want a proposal before code changes.

**Example:** "Use benimaru-planner. I want recurring reminders but have not chosen how they should work. Restate the goal and problem, investigate, and clarify choices that could change the approach before recommending a plan."

**Expected result:** four steps in order. (1) Your outcome, problem, and "done when" check, restated. (2) The open decisions that could change the approach, asked before any recommendation: up to four per round, each with 2–4 choices, the recommended one first with its reason. It uses the host's question tool when available, numbered choices otherwise, and checks facts itself instead of asking. (3) A verdict-first recommendation and the main rejected alternative. (4) A plan sized to the work, split into slices only when one session would be unreliable.

The plan stays in the conversation unless you ask to save it; then it writes one Markdown file with a checkbox per slice, which Kurobe ticks as slices land.

When work needs another session, Rimuru and Kurobe give a [short handoff](skills/rimuru-coordinator/SKILL.md#finish). They update an existing plan file or handoff, or give the handoff in the response when writing a file is not authorized. Ordinary completed tasks need no separate handoff document.

**Adjust when:** it recommends before asking, asks without choices or a recommendation, offers choices that do not answer the same question, asks you facts it could look up, or repeats settled questions. Name the step it skipped.

### Kurobe Implementer — build or fix

**Use when:** the change is clear or its plan is approved. Kurobe already includes test selection and verification; a separate verifier is not required for every change.

**Example:** "Use kurobe-implementer to implement the approved saved-filter plan. Preserve existing search behavior and verify the changed path."

**Expected result:** a complete change at the owning boundary, reuse of existing architecture, a meaningful test decision, and observed checks. Small, clear fixes stay fast: checks run inline without loading other skills. Failures caused by the change are fixed until checks pass or a concrete blocker remains. Before editing a failing test, Kurobe says whether the code or the test is wrong and why. A finished plan slice is ticked in the same commit as its code.

TDD is used for bug fixes when a failing test is cheap, and whenever you say "Use TDD": one behavioral test red for the right reason, then minimal green. Commands you must run yourself come with real values, the user to run them as, and the expected output.

**Adjust when:** it adds speculative abstractions, skips relevant checks, weakens assertions, or repeatedly retries without new evidence. Identify the actual mismatch with the request.

### Soei Investigator — explain a failure

**Use when:** something is broken, slow, or intermittent and you need the cause understood before deciding on a fix.

**Example:** "Use soei-investigator. Saving sometimes creates duplicate notes after a connection retry. Find the cause and smallest fix; keep this investigation read-only."

**Expected result:** observed symptoms, a safe reproduction or existing evidence, a supported cause with uncertainty stated, and the next useful check or fix.

**Adjust when:** it edits during a diagnosis-only request, guesses without evidence, or repeats checks that cannot distinguish causes. If you also want a fix, say so explicitly.

### Hakuro Reviewer — find defects in a change

**Use when:** you have a diff, branch, or commit range to review. Give it a comparison base when available.

**Example:** "Use hakuro-reviewer to review this branch against main for defects introduced by the saved-filter change. Keep the review read-only."

**Expected result:** actionable findings with severity, location, trigger, consequence, and evidence, or a clear statement that no defects were found. Later review focuses on fixes and affected behavior; resolved findings need new evidence to reopen.

**Adjust when:** it reports preferences as bugs, flags unrelated old defects, or keeps producing review rounds without meaningful progress. Ask it to substantiate the finding against the caller contract.

### Shuna Test Triage — choose useful coverage

**Use when:** you are unsure whether a change needs new tests or which test scope can catch its realistic failure. Kurobe normally reads this procedure itself.

**Example:** "Use shuna-test-triage. Does this filter change have a coverage gap? Inspect existing assertions and recommend reuse, extension, a new test, or no new test."

**Expected result:** one explained test decision, the failure it catches, and the smallest faithful scope. New tests are justified by a gap; skipping a new test still requires appropriate verification. When an existing end-to-end flow or using the app proves the behavior, it checks that way instead of writing a test. New tests use literal expected values, run integration cases against the real engine, and are broken once on purpose to show they can fail.

**Adjust when:** it adds tests for every edit, writes a test that using the app would already prove, puts logic in tests, mirrors implementation details, or chooses mocks that hide the failure. Test scope is about what must be exercised; TDD is about implementation order.

### Ranga Verifier — prove existing work

**Use when:** work already exists and you want evidence that it meets the request, without authorizing repairs.

**Example:** "Use ranga-verifier to verify that filters survive reload and remain private to their owner. Use the safe local target and report gaps; do not modify application code."

**Expected result:** passed, failed, or pending conditions tied to the checked code state, target, and actual output. A build alone does not establish that the user journey works.

**Adjust when:** it declares success from insufficient evidence, repeats passing checks without a reason, or changes code during verification-only work. Explicitly authorize repairs if you want them.

### Kaijin Verification Builder — create a reusable procedure

**Use when:** the project repeatedly needs the same verification workflow and lacks a clear, reusable procedure. A one-off check can use Ranga.

**Example:** "Use kaijin-verification-builder to document how to verify saved filters using our existing harness, disposable data, and local app. Exercise one representative journey."

**Expected result:** a project verification skill with real commands, prerequisites, observable checks, evidence, and cleanup. Complex projects may need a small feature-to-check map. Unsupported execution is reported as unverified.

**Adjust when:** it creates a new testing framework without need, documents commands it has not confirmed, or treats a written procedure as proof it works.

## Keep time and cost proportionate

Give an existing plan, relevant failure output, and completed checks when available. State constraints early. An instruction such as "no browser tests this session" leaves dependent proof pending; it does not make an unrun check pass.

Ask for the first useful milestone before a large build. Split for reliable delivery or handoffs, not because of an arbitrary file or ticket count. Separate agents add coordination work; use them for a named independent benefit. Required project checks and safety boundaries still apply.

If a task is expensive, inspect where work went: genuine scope, new decisions, environment failures, repeated investigation, or unnecessary coordination. Skill length and elapsed time alone do not establish the cause.

## Model preferences and host setup

Loading a skill leaves the current model in place. Direct specialist use works without Rimuru: "Use Kurobe" applies its procedure to the current agent. Rimuru checks applicable standing delegation instructions before choosing inline or delegated work. Its [delegation preferences](skills/rimuru-coordinator/references/delegation.md) classify delegated work by complexity and distinguish Codex, Claude Code, OpenCode, and T3 Code. The reference is loaded only for delegated work.

The default is to stay with the parent's provider. A Claude parent prefers the Claude lineup; a Codex parent prefers the Codex lineup. In T3 Code or OpenCode, identify the actual model provider separately from the host. Explicit task choices take priority, subject to available routes and pinned native settings. If an exact request cannot be satisfied, the agent reports it; a missing independent review remains a gap.

For reliable execution settings, use your host's native agent configuration and keep it authoritative. The reference links official configuration documentation. Supported model IDs, effort levels, overrides, and task tools must be confirmed in the current environment. `agents/openai.yaml` controls skill UI and invocation policy; it is not where this collection sets execution models. Installing these skills changes no native agent profiles and enables no additional provider access.

Keep small work in the parent and use one child when its separate contribution is useful. Select stronger reasoning for an identified difficult decision or consequential risk. Existing approved profiles can be used without repeated confirmation; changes outside approved provider or cost choices need a decision. These are usage preferences, not measured subscription savings or a requirement to delegate every phase.

## Make adjustments from experience

| Kind of adjustment | Where it belongs |
| --- | --- |
| A preference for this task, such as proposal-only or TDD | Your request |
| A stable project rule, such as required checks or protected data | The project's existing instructions |
| A repeated workflow mistake across projects | The relevant `SKILL.md` |
| Display text or supported Codex invocation settings | That skill's `agents/openai.yaml` |
| Shared delegation behavior and preferred work levels | Rimuru's `references/delegation.md` |
| Exact execution models, effort, and role overrides | Your host's native agent configuration |

For a skill change, record the task, expected behavior, actual behavior, and consequence. Change the narrowest relevant instruction. Compare similar tasks with the same model and starting state, including a case where extra process should be unnecessary. Keep a change only when outcomes support it; word matching and attractive formatting do not establish effectiveness.

Edit the maintained files in `skills/<name>/SKILL.md`, review, commit, and push. Update installed copies separately. Avoid editing a managed installed copy as the only source because an update may replace it.

For the workflow and plain-name invocation changes in v0.2.0:

```sh
npx skills update rimuru-coordinator benimaru-planner kurobe-implementer soei-investigator hakuro-reviewer ranga-verifier shuna-test-triage kaijin-verification-builder
```

Select the matching installation scope when prompted; add `-g` to target global installs. For Codex plugin installations, use the plugin update flow instead. See [installation and update instructions](README.md#update-or-remove).
