# Delegation preferences

Apply task and explicit standing delegation instructions before these model preferences. Preferences alone neither require delegation nor grant authority. Project requirements, native configuration, and host capabilities still apply; the parent model stays unchanged.

## Select a model

Default to the parent's provider unless JC selects another. Distinguish host from provider: T3 Code running Claude is a T3 host with a Claude provider.

Use explicit model and effort instructions first, then a compatible configured role, then the table. Keep native profiles unchanged; pinned settings may override invocation arguments. If exact requested settings are unavailable or conflict with provider restrictions, leave that assignment pending for JC's decision and continue independent authorized work. For an unavailable preference, use the parent where suitable and disclose the fallback. Resolve material cost changes before dispatch.

### Preferred lineup

| Work | Codex preference | Claude preference |
| --- | --- | --- |
| Mechanical edits, routine command checks | GPT-6 Luna, low | Haiku, low |
| Bounded investigation, test-scope decisions | GPT-6 Luna, medium | Sonnet, medium |
| Routine implementation | GPT-6.1 Sol, low | Sonnet, medium |
| Routine review, reusable verification procedures | GPT-6.1 Sol, medium | Sonnet, medium |
| Complex planning, difficult diagnosis, consequential review or implementation | GPT-6.1 Sol, high | Opus, high |

Classify actual work, not the skill name. Command-only verification is routine; interactive verification needs bounded investigation. Review concrete authorization, data-loss, concurrency, or compatibility risks as consequential work. A lower work level needs evidence of simpler work, not merely tool availability.

Resolve `gpt-6-luna`, `gpt-6.1-sol`, or Claude's `haiku`, `sonnet`, and `opus` aliases against models and effort levels exposed by the host. Other hosts may require provider-qualified IDs. This table does not establish price, access, or measured quality.

## Keep usage proportionate

- Keep coordination with the parent. Use one child unless independent tasks justify two; normally cap concurrency at two.
- Choose sufficient capability at the start. Raising effort needs a concrete reason; provider or cost changes outside approved choices need JC's decision. Repeated failure calls for testing shared assumptions, not automatic escalation. Multi-provider councils require explicit provider authorization.
- Give fresh children the outcome, separate ownership, constraints, relevant memory and findings, checked code state, completed checks, and deliverable. Writers preserve others' changes. Children report further delegation needs to the parent.

## Use the current host

Consult only the current host's route. Confirm exposed tools and schemas before dispatch; listed names do not prove availability.

| Host | Execution settings and lifecycle |
| --- | --- |
| Codex | Use native agents. TOML uses `model` and `model_reasoning_effort`; pinned role settings control execution. |
| Claude Code | Use native agents with supported `model` and `effort`; check effective settings for overrides. |
| OpenCode | Use configured agents and native task tools with `provider/model-id` and supported reasoning options. |
| T3 Code | Use exposed native agent tools. For an exposed `delegate_task` route, query `orchestrator_capabilities` first when available. Confirm its models and lifecycle from the actual schemas. |
| No usable delegation route | Run suitable procedures sequentially with the parent. Report unavailable independent review or exact-model assignments; leave dependent evidence pending. |

Native configuration guidance: [Codex](https://learn.chatgpt.com/docs/agent-configuration/subagents), [Claude Code](https://code.claude.com/docs/en/sub-agents), and [OpenCode](https://opencode.ai/docs/agents/). The T3 capability names come from [tstack's sol-loop](https://github.com/t3dotgg/tstack/blob/7de017b3fc9d50c03cf3ecb98fb71e0ca65a78bd/skills/sol-loop/SKILL.md); they require confirmation in the running host.

## Dispatch and collect evidence

At dispatch, briefly state the independent benefit, host, role, provider, model, and effort. Distinguish requested from confirmed settings; mark unexposed settings unknown. Report substitutions once; keep routine polling out of updates.

Record task handles; inspect status after uncertain responses before redispatching. Collect required results before integration. The parent resolves material findings, owns final verification, and releases finished workers through host completion, close, or stop tools. Delegation does not authorize publishing, merging, deployment, or live-data changes.
