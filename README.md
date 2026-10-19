# JCCDLabs Skills

Eight concise development skills for choosing a workflow, planning, implementing, investigating, reviewing, and verifying software. Names draw from Rimuru's companions in *That Time I Got Reincarnated as a Slime*. Function labels stay explicit; the instructions focus on engineering rather than roleplay.

## Install

Requires Node.js supported by the [skills CLI](https://github.com/vercel-labs/skills). Preview the collection first:

```sh
npx skills add jccd-dev/jccdlabs-skills --list
```

Install interactively and choose your skills and agents:

```sh
npx skills add jccd-dev/jccdlabs-skills
```

Install all eight for Codex and Claude Code in the current project:

```sh
npx skills add jccd-dev/jccdlabs-skills --skill '*' -a codex -a claude-code
```

Add `-g` for personal installation across projects. The installer also supports Cursor, Gemini CLI, and other agents; see its [supported agents](https://github.com/vercel-labs/skills#supported-agents). No npm package for this repository is needed: `npx` runs the external `skills` installer, which reads this GitHub repository.

## Choose a skill

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

In Codex, mention `$kurobe-implementer` to implement a change or `$rimuru-coordinator` to select a workflow. Other agents use their own skill selector or invocation syntax.

Kurobe includes testing and reads Shuna before deciding coverage. TDD applies when requested or required; an installed `tdd` skill is optional, with a small red–green fallback included. Fixes continue through relevant checks until they pass or evidence identifies a concrete blocker. Existing coverage is reused where sufficient.

Install the whole collection for sibling procedures to be available. Individually installed skills have fallbacks for missing helpers. Codex metadata preserves explicit invocation for the seven task workflows and normal discovery for Shuna. Invocation controls vary by host; other agents may automatically select skills by description.

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

## Optional Codex plugin

The root `plugin.json` and `.agents/plugins/marketplace.json` also package the collection as a skills-only plugin, following [OpenAI's packaging format](https://developers.openai.com/plugins/build/plugins). This is an alternative installation route; use one route to avoid duplicate skills:

```sh
codex plugin marketplace add jccd-dev/jccdlabs-skills
codex plugin add jccdlabs-skills@jccdlabs-skills
```

The plugin supplies no connectors or extra permissions. Refresh its source with `codex plugin marketplace upgrade jccdlabs-skills`, then use your host's plugin update flow.

## Status and credits

Initial publication: 2026-10-19. Packaging and installation checks are recorded in the GitHub release. These workflows still need representative project trials; installation compatibility does not establish engineering effectiveness.

Originally authored and refined in JC's Chibako collection. This Git repository is the maintained distribution source. Concepts were adapted in original wording from [Poteto's trust hierarchy](https://x.com/poteto/status/2111133080526495985) and [Cursor pstack](https://github.com/cursor/plugins/tree/main/pstack): architectural invariants, executable checks, concise instructions, and focused review. Test triage grew from JC's supplied skill. Matt Pocock's TDD skill is not bundled.

MIT licensed. Character names are fan-inspired references; this project is unaffiliated with the series and includes no anime artwork or copied dialogue.
