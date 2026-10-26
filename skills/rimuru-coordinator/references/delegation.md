# Delegation preferences

Use this reference when selecting or running delegated work. These are preferred routes, subject to the user's instructions, project requirements, native agent configuration, and actual host capabilities. They do not grant additional authority or change the parent model.

## Select a model

Default to the parent model's provider unless JC explicitly selects another. Identify the host separately: T3 Code running Claude is a T3 session with a Claude provider. Loading a skill alone leaves the current model in place.

Use an explicit task selection first, then a matching configured native role, then the preferences below. A pinned native role may override invocation settings; select a compatible route rather than claiming the override succeeded. Keep existing native profiles unchanged. A role pinned to high effort cannot satisfy an exact medium-effort request. If an exact requested model or effort is unavailable, keep that assignment pending until JC approves a substitute; continue independent authorized work. If explicit provider restrictions conflict with a requested model, ask which applies before dispatching that assignment. For an unavailable preference, use the current parent where suitable and disclose the fallback; resolve any material cost change before proceeding.

### Preferred lineup

| Work | Codex preference | Claude preference |
| --- | --- | --- |
| Mechanical edits, routine command checks | GPT-6 Luna, low | Haiku, low |
| Bounded investigation, test-scope decisions | GPT-6 Luna, medium | Sonnet, medium |
| Routine implementation | GPT-6.1 Sol, low | Sonnet, medium |
| Routine review, reusable verification procedures | GPT-6.1 Sol, medium | Sonnet, medium |
| Complex planning, difficult diagnosis, consequential review or implementation | GPT-6.1 Sol, high | Opus, high |

Use the model and effort from the row matching the actual work when available, unless an explicit selection or configured native role fixes different settings. Selecting a lower work level needs evidence that the task is simpler; tool availability alone is not that evidence.

Resolve the Codex preferences to `gpt-6-luna` or `gpt-6.1-sol` only when the current host lists those IDs. Resolve Claude's `haiku`, `sonnet`, and `opus` aliases through the current host. Other hosts may require provider-qualified IDs. Validate the selected model's supported effort levels; labels and availability vary by host and provider. These preferences do not establish price, subscription access, or measured quality.

### Match the skill's actual work

| Skill | Preferred route when delegation is justified |
| --- | --- |
| rimuru-coordinator | Keep coordination with the current parent. |
| benimaru-planner | Complex planning for consequential choices; routine work for a bounded plan. |
| kurobe-implementer | Mechanical, routine, or complex implementation according to the task. |
| soei-investigator | Bounded investigation first when sufficient; difficult diagnosis for unresolved ambiguity. |
| hakuro-reviewer | Use consequential review when examining concrete authorization, data-loss, concurrency, or compatibility risks; otherwise routine review. |
| shuna-test-triage | Test-scope decisions, usually inline with implementation. |
| ranga-verifier | Routine command checks; bounded investigation effort for interactive or browser checks. |
| kaijin-verification-builder | Reusable verification procedures. |

## Keep usage proportionate

- Prefer the parent for straightforward work. Use one child for a useful independent task; normally cap concurrent children at two, with separate ownership.
- Choose the appropriate capability at the start when complexity or consequences are already clear. Higher effort within an approved profile needs a concrete reason; provider changes and cost increases outside the approved choices require a user decision. Repeated failure calls for testing the shared assumption, not automatic escalation.
- Give fresh children the outcome, ownership, constraints, relevant memory and findings, checked code state, completed checks, and required deliverable. Use fresh context when supported; include the history that the task actually needs. Children report further delegation needs to the parent.
- Reuse valid findings and evidence for the current code and target. Multi-provider councils are optional and require explicit provider authorization.

## Use the current host

Consult only the relevant host route. Confirm available tools and their argument schemas before dispatch; a name in this reference is not proof that a tool exists.

| Host | Execution settings and lifecycle |
| --- | --- |
| Codex | Use exposed native agents and delegation tools. Native TOML uses `model` and `model_reasoning_effort`; pinned values take precedence over invocation settings. Keep role configuration and supported IDs as the execution source of truth. Use the host's result, wait, and close/interrupt operations. |
| Claude Code | Use native agents and supported `model` and `effort` settings. Check effective settings because host overrides can affect them. Collect results and use the exposed task completion or stop operations as needed. |
| OpenCode | Use configured agents and native task tools. Resolve `provider/model-id` and provider-specific reasoning options; use the host's result and task lifecycle. |
| T3 Code | If exposed, query `orchestrator_capabilities` before `delegate_task`. Read the actual schemas and available models; record the returned task handle and follow the exposed result, wait, and completion/cancellation contract. T3 tool names do not apply to other hosts. |
| No usable delegation route | Run suitable procedures sequentially with the parent. State any unavailable independent review or exact-model assignment; leave dependent evidence pending. |

Native configuration guidance: [Codex](https://learn.chatgpt.com/docs/agent-configuration/subagents), [Claude Code](https://code.claude.com/docs/en/sub-agents), and [OpenCode](https://opencode.ai/docs/agents/). The T3 capability names come from [tstack's sol-loop](https://github.com/t3dotgg/tstack/blob/7de017b3fc9d50c03cf3ecb98fb71e0ca65a78bd/skills/sol-loop/SKILL.md); they require confirmation in the running host.

## Dispatch and collect evidence

Briefly state the independent benefit and selected host, role, provider, model, and effort at dispatch. Distinguish requested settings from confirmed execution settings; report settings as unknown when the host does not expose them. Report a substitution once. Keep routine polling out of user-facing updates.

Give writers non-overlapping ownership and require them to preserve others' work. Record the task handle, collect required results before integration, and use returned status to avoid duplicate dispatch after an uncertain response. The parent resolves material findings, owns final verification, and releases finished workers using the host's lifecycle tools. A skill or delegation does not authorize publishing, merging, deployment, or live-data changes.
