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

Install all eight for Codex, Claude Code, and OpenCode in the current project:

```sh
npx skills add jccd-dev/jccdlabs-skills --skill '*' -a codex -a claude-code -a opencode
```

Add `-g` for personal installation across projects. The installer also supports Cursor, Gemini CLI, and other agents; see its [supported agents](https://github.com/vercel-labs/skills#supported-agents). No npm package for this repository is needed: `npx` runs the external `skills` installer, which reads this GitHub repository.

## Choose a skill

Start with the [practical usage guide](GUIDE.md): everyday prompts, when each skill helps, what to expect, and how to adjust it from experience. Rimuru is the usual entry point; specialist skills are optional direct choices. The [scenario prompt collection](PROMPTS.md) provides copyable prompts for all eight skills, including work started or completed by another agent.

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

Ask for a skill by its short or full name in ordinary text: "Use Kurobe to implement this change" or "Use rimuru-coordinator to choose the workflow." All eight descriptions include both names; no `$` or `/` prefix is required for model selection in a compatible harness. Use a request to apply the skill; asking what a skill does remains an explanation request.

Install the skills in a location your harness discovers. [Codex](https://learn.chatgpt.com/docs/build-skills) allows implicit invocation through `agents/openai.yaml`; [Claude Code](https://code.claude.com/docs/en/skills) allows model invocation by default; [OpenCode](https://opencode.ai/docs/skills/) lists skill names and descriptions for its agent to select through the `skill` tool. Other Agent Skills-compatible harnesses can use the same descriptions. Selection depends on the model and host settings; native skill selectors remain available when you need explicit loading.

Kurobe includes testing and reads Shuna before deciding coverage. TDD applies when requested or required; an installed `tdd` skill is optional, with a small red–green fallback included. Fixes continue through relevant checks until they pass or evidence identifies a concrete blocker. Existing coverage is reused where sufficient.

Benimaru's plans can be handed to Matt Pocock's [to-tickets](https://github.com/mattpocock/skills/blob/main/skills/engineering/to-tickets/SKILL.md) when you request ticket creation. This companion is optional; install it and follow its invocation and tracker setup requirements. Project tracker conventions and publishing permissions still apply.

Install the whole collection for sibling procedures to be available. Individually installed skills have fallbacks for missing helpers. All eight allow model selection; Shuna uses Codex's default policy. The shared skill files use standard `name` and `description` fields, with no Claude-only invocation restrictions. Loading a skill does not expand the task's editing or execution authority.

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

## Status

Initial publication: 2026-10-19. Packaging and installation checks are recorded in the GitHub release. These workflows still need representative project trials; installation compatibility does not establish engineering effectiveness.

MIT licensed. Character names are fan-inspired references; this project is unaffiliated with the series and includes no anime artwork or copied dialogue.
