# JCCDLabs skills config

Read by the JCCDLabs skills. Edit by hand or rerun great-sage-setup. A missing section means the skill's built-in default.

## Models
| Work | Provider | Model | Effort |
| --- | --- | --- | --- |
| Mechanical edits, code mapping, test runs, log reading | Claude | Haiku | low |
| Mechanical edits, code mapping, test runs, log reading | Codex | GPT-6 Luna | low |
| Bounded investigation, test-scope decisions | Claude | Sonnet | medium |
| Bounded investigation, test-scope decisions | Codex | GPT-6 Luna | medium |
| Routine implementation and review, verification procedures | Claude | Sonnet | medium |
| Routine implementation and review, verification procedures | Codex | GPT-6.1 Sol | medium |
| Complex planning, hard diagnosis, risky review or implementation | Claude | Opus | high |
| Complex planning, hard diagnosis, risky review or implementation | Codex | GPT-6.1 Sol | high |

## Octagram
| Member | Effort |
| --- | --- |
| Claude Opus | high |
| GPT Sol | high |
| Gemini Pro | high |

- Max rounds: 3
- Pass score: none
<!-- none: pass when every member is satisfied | 1-10: pass when the round average meets it -->

## Plans
- Folder: .slime/plans/
- When every slice is done: delete
<!-- delete | keep | move to <folder> -->

## Handoffs
- Where: chat only
<!-- chat only | .slime/handoffs/ | memory tool (name it) -->
