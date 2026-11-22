# JCCDLabs Skills

Twelve concise development skills for choosing a workflow, planning, implementing, investigating, reviewing, verifying, and shipping software through pull requests. Names draw from Rimuru's companions in *That Time I Got Reincarnated as a Slime*. Function labels stay explicit; the instructions focus on engineering rather than roleplay.

## Install

Requires Node.js supported by the [skills CLI](https://github.com/vercel-labs/skills). Preview the collection first:

```sh
npx skills add jccd-dev/jccdlabs-skills --list
```

Install interactively and choose your skills and agents:

```sh
npx skills add jccd-dev/jccdlabs-skills
```

Install all twelve for Codex, Claude Code, and OpenCode in the current project:

```sh
npx skills add jccd-dev/jccdlabs-skills --skill '*' -a codex -a claude-code -a opencode
```

Add `-g` for personal installation across projects. The installer also supports Cursor, Gemini CLI, and other agents; see its [supported agents](https://github.com/vercel-labs/skills#supported-agents). No npm package for this repository is needed: `npx` runs the external `skills` installer, which reads this GitHub repository.

## Choose a skill

Start with the [practical usage guide](GUIDE.md): everyday prompts, when each skill helps, what to expect, and how to adjust it from experience. Rimuru is the usual entry point; specialist skills are optional direct choices. The [scenario prompt collection](PROMPTS.md) provides copyable prompts for the original eight skills, including work started or completed by another agent.

These character-to-workflow matches are this project's interpretation of the [official character profiles](https://www.ten-sura.com/character).

| Skill | Job | Naming connection | Former name |
| --- | --- | --- | --- |
| [rimuru-coordinator](skills/rimuru-coordinator/SKILL.md) | Choose and coordinate the workflow | Rimuru brings companions together | jc-mode |
| [benimaru-planner](skills/benimaru-planner/SKILL.md) | Scope a change and prepare a plan | Benimaru's leadership and resolve | jc-plan |
| [kurobe-implementer](skills/kurobe-implementer/SKILL.md) | Build or fix the smallest complete change | Kurobe's practical smithing craft | jc-implement |
| [soei-investigator](skills/soei-investigator/SKILL.md) | Find a failure's cause from evidence | Soei's calm, covert approach | jc-investigate |
| [hakuro-reviewer](skills/hakuro-reviewer/SKILL.md) | Find actionable defects in a change | Hakuro's experienced swordsmanship | jc-review |
| [ranga-verifier](skills/ranga-verifier/SKILL.md) | Prove requested behavior | Ranga's protective role | jc-verify |
| [shuna-test-triage](skills/shuna-test-triage/SKILL.md) | Choose meaningful coverage and test scope | Shuna's careful craft and support | test-scope-triage |
| [kaijin-verification-builder](skills/kaijin-verification-builder/SKILL.md) | Write and exercise a project verification procedure | Kaijin's workshop craftsmanship | jc-create-verification |
| [shion-pr](skills/shion-pr/SKILL.md) | File, check, and review pull requests | Shion, Rimuru's secretary | new |
| [gobta-shipper](skills/gobta-shipper/SKILL.md) | Ship a change to a PR ready to merge | Gobta's eager, hands-on runs | new |
| [octagram-council](skills/octagram-council/SKILL.md) | Score work with three models from different providers | The Octagram, Tempest's council of lords | new |
| [great-sage-setup](skills/great-sage-setup/SKILL.md) | Write a repository's `.slime/config.md` | Great Sage, Rimuru's analysis skill | new |

Ask for a skill by its short or full name in ordinary text: "Use Kurobe to implement this change" or "Use rimuru-coordinator to choose the workflow." All descriptions include both names; no `$` or `/` prefix is required for skill invocation in a compatible harness. Use a request to apply the skill; asking what a skill does remains an explanation request.

Install the skills in a location your harness discovers. [Codex](https://learn.chatgpt.com/docs/build-skills) allows implicit invocation through `agents/openai.yaml`; [Claude Code](https://code.claude.com/docs/en/skills) allows model invocation by default; [OpenCode](https://opencode.ai/docs/skills/) lists skill names and descriptions for its agent to select through the `skill` tool. Other Agent Skills-compatible harnesses can use the same descriptions. Selection depends on the model and host settings; native skill selectors remain available when you need explicit loading.

Benimaru restates the goal and problem, asks the open decisions with recommended choices, and only then recommends an approach and plan. When asked, it saves one plan file with a checkbox per slice; Kurobe ticks each slice in the same commit as its code. No tracker or companion skill is required.

Kurobe sizes its own procedure: small, clear changes run checks inline without loading other skills, while larger or risky work uses Shuna, Ranga, or Hakuro for the part that needs it. TDD is used for bug fixes when a failing test is cheap, and whenever requested. Kurobe owns the red-green loop and Shuna owns test quality, so no outside TDD skill is needed.

Small work stays in one agent. Hakuro reviews a non-trivial change the same agent wrote in a subagent with a fresh context window, Octagram runs three council members by design, and Benimaru, Kurobe, Ranga, and Soei hand wide code mapping, long test runs, and long logs to a subagent on the cheapest model from the parent's provider (Haiku on Claude, Luna on Codex). The skills describe the job in prose and ship no agent definitions, so your own subagents are used when they fit. Ideas from [Matt Pocock's skills](https://github.com/mattpocock/skills) and [pstack](https://github.com/cursor/plugins/tree/main/pstack) are adapted without their subagent panels.

Install the whole collection for sibling procedures to be available. Individually installed skills have fallbacks for missing helpers. All skills allow model-initiated invocation in Claude Code; in Codex, Shuna uses the default policy, and Octagram, Gobta, and Great Sage run only when named, because they cost several model runs, push branches, or write config. The shared skill files use standard `name` and `description` fields, with no Claude-only invocation restrictions. Loading a skill does not expand the task's editing or execution authority.

Skills select procedures, not execution models. Rimuru's [delegation preferences](skills/rimuru-coordinator/references/delegation.md) favor the parent's provider and proportionate model effort when a separate agent helps. Native agent settings control execution; the collection does not install or modify them. See [model preferences and host setup](GUIDE.md#model-preferences-and-host-setup) for direct skill use and host differences.

## Per-project config

Each repository can hold a `.slime/` folder that the skills read instead of fixed defaults:

```
.slime/
├── config.md    # plans, handoffs, checks, comments, verification folder, PRs, models, Octagram
├── plans/       # Benimaru writes, Kurobe ticks
└── handoffs/    # only when handoffs are saved as files
```

Run great-sage-setup once per repository. It pre-fills answers from the repository and its PR history, asks one section at a time, and shows the draft before writing. Commit `.slime/` in a solo repository; gitignore it where others open PRs. Without a config, every skill keeps its built-in default.

## Update or remove

Manage installed copies with the [skills CLI](https://github.com/vercel-labs/skills#other-commands):

```sh
npx skills update kurobe-implementer shuna-test-triage
npx skills remove jccd-dev/jccdlabs-skills
```

Choose the matching installation scope when prompted. For a global removal, add `-g`.

To maintain the source, edit `skills/<name>/SKILL.md` in your clone, review the diff, commit, and push. Installed copies update separately. Legacy `jc-*` and `test-scope-triage` installations are separate skills; these new names do not overwrite them.

## Installation safety

This collection contains Markdown instructions and declarative metadata. It ships no executable scripts, package lifecycle hooks, agent hooks, MCP servers, credentials, or downloaded assets. Installation does not require an API key or permission to run a project's commands. Using a skill remains subject to your agent's permissions and your project's instructions.

`npx` executes a third-party installer. For a reproducible installer version, the checked command is `npx skills@1.7.2 add jccd-dev/jccdlabs-skills --list`. You can disable installer telemetry with `DISABLE_TELEMETRY=1`; see the [CLI documentation](https://skills.sh/docs/cli). Review updates before granting an agent access to sensitive projects. Instruction-only skills still influence agent behavior; this is not a sandbox or a guarantee against mistakes.

## Optional Claude Code plugin

`.claude-plugin/` packages the same skills as a Claude Code plugin. It ships no agent definitions, so it never conflicts with your own subagents.

```sh
claude plugin marketplace add jccd-dev/jccdlabs-skills
claude plugin install jccdlabs-skills@jccdlabs-skills
```

Use one installation route per host to avoid duplicate skills.

## Optional Codex plugin

The root `plugin.json` and `.agents/plugins/marketplace.json` also package the collection as a skills-only plugin, following [OpenAI's packaging format](https://developers.openai.com/plugins/build/plugins). This is an alternative installation route; use one route to avoid duplicate skills:

```sh
codex plugin marketplace add jccd-dev/jccdlabs-skills
codex plugin add jccdlabs-skills@jccdlabs-skills
```

The plugin supplies no connectors or extra permissions. Refresh its source with `codex plugin marketplace upgrade jccdlabs-skills`, then use your host's plugin update flow.

## Status

Version 0.9.0 adds a pull-request workflow and per-project config. Shion files PRs (problem first, then Evidence, Merge danger, and a model line), checks one before merge with a ready or blocked verdict, and reviews other authors' PRs by feature area with risk flags, posting drafted comments only when told. Gobta carries a change through Ranga, Hakuro, push, and Shion, then stops at the merge gate. Octagram runs a three-provider council that scores out of 10, loops until satisfied, and rejects scope creep. Great Sage writes `.slime/config.md`, which Benimaru, Kurobe, Kaijin, Ranga, and Rimuru now read for plan paths, checks, handoffs, and models. Kurobe stops writing comments that repeat the code or excuse a hack and removes ones its change makes stale; Hakuro flags them in review and can audit a folder's comments on request, following Matt Pocock's tautology, excuse, stale, and decision-record split. The comment policy is why-only by default, or none per project. PR, council, and comment conventions are adapted from Theo Browne's [tstack](https://github.com/t3dotgg/tstack) (MIT); its polling scripts were left out. The new skills have not been exercised on real tasks yet.

Version 0.8.0 makes the collection self-contained for TDD: Kurobe runs the red-green loop itself, takes test-first requests, and follows Shuna for test quality instead of loading an outside `tdd` skill. Hakuro maps each changed file's inputs, queries, auth checks, sessions, external calls, and cryptography, reports security findings only for attacker-controlled values the framework doesn't already mitigate, loads an installed `security-review` skill at trust boundaries, and lists what it read and couldn't verify. Soei compares the failing path with similar working code and logs component boundaries to find the layer that breaks. Kurobe checks a subagent's diff before repeating its success claim. Ideas adapted from [Sentry's skills](https://github.com/getsentry/skills) and [Superpowers](https://github.com/obra/superpowers). All eight skills pass [SkillEvaluator](https://github.com/NVIDIA/SkillEvaluator) 1.0.1 Tier 1 checks without a model (schema, security, PII, license, quality grade B, and loading in six harnesses); deduplication and live agent evaluation have not been run.

Version 0.7.0 connects verification and review. Ranga runs typecheck, lint, and existing tests before any hands-on check, tries one input that must be refused where a condition protects data or access, and recommends Kaijin for a hands-on check that will be needed again. Hakuro reads verification evidence first, defines three severity levels, stops after two re-review rounds on the same finding, and reviews a risky change the same agent wrote in a fresh subagent. Soei suggests a fix only when a check demonstrated the cause. Benimaru says where new code will live for a new project or module. These rules have not been exercised on real tasks yet.

Version 0.6.0 rewrites all eight skills in compact, plain, impersonal language. Ranga matches each condition to the evidence that proves it, including when a browser is needed, and counts skipped tests as not run. On risky work Rimuru verifies before review, and Hakuro focuses on what running the code can't show. Benimaru requires a runnable "done when", Kaijin fails only on new failures when old ones exist, and Kurobe keeps the TDD rule on small bug fixes.

Version 0.5.0 rebuilds Benimaru around shared understanding: restate, ask decisions with recommended choices, then plan. Spec and ticket companions are replaced by one optional plan file. Kurobe scales its procedure to the change, states whether code or test is wrong before editing a failing test, and closes plan slices in the same commit. Soei builds a reproduction loop and ranks falsifiable hypotheses; Hakuro proves findings and checks the change against the request; Shuna keeps logic out of tests, uses real dependencies for integration tests, breaks a protected line once to prove a new test can fail, and checks in the app instead of adding a test when that proves the behavior. Rimuru says when it pays off and when to skip it, loads each phase once, explains why subagents can cost more than inline work, follows explicit model requests, and ignores stale saved provider notes. Commands handed to JC must work when pasted.

Version 0.4.2 makes Hakuro's security review explicit at affected trust boundaries: authentication and authorization bypasses, injection, unsafe input handling, secret exposure, and sensitive-data leaks. Findings remain evidence-backed and tied to the supplied change. Metadata parsing and diff formatting were checked; live reviewer behavior remains untested.

Version 0.4.1 keeps Benimaru focused on conversational planning: clarify consequential unknowns before recommending, retain the goal/problem/success restatement, and leave spec and ticket procedures to their companion skills. Planning artifacts require an explicit request. Session-handoff guidance now belongs to Rimuru. Six conversational scenarios, metadata parsing, local links, and diff formatting were checked; these do not establish live cross-host behavior.

Initial publication: 2026-10-19. Packaging and installation checks are recorded in the GitHub release. These workflows still need representative project trials; installation compatibility does not establish engineering effectiveness.

MIT licensed. Character names are fan-inspired references; this project is unaffiliated with the series and includes no anime artwork or copied dialogue.
