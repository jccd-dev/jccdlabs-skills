# JCCDLabs skills config

Read by the JCCDLabs skills. Edit by hand or rerun great-sage-setup. A missing section means the skill's built-in default.

## Plans
- Folder: .slime/plans/
- Save: on request
- When every slice is done: delete

## Handoffs
- Where: chat only
<!-- chat only | .slime/handoffs/ | memory tool (name it) -->

## Checks
- Typecheck: pnpm typecheck
- Lint: pnpm lint
- Tests: pnpm test
- E2E: none
- Known failures: none

## Code comments
- Policy: why-only
<!-- why-only: a comment only for a non-obvious why | none: no comments; decisions go in commits, PRs, or ADRs -->

## Verification procedures (Kaijin)
- Folder: .agents/skills/

## PRs
- Base: main
- Who merges: user
<!-- user | teammate | agent when told -->
- Merge method: squash
- Body: problem first, Evidence, Merge danger

## Models
| Work | Model | Effort |
| --- | --- | --- |
| Mechanical edits, routine checks | Haiku | low |
| Bounded investigation, routine implementation and review | Sonnet | medium |
| Complex planning, hard diagnosis, risky review | Opus | high |

## Octagram
- Members: Claude Opus high, GPT Sol high, Gemini Pro high
- Allowed on: T3 Code
- Use for: frontend design, plans, risky reviews, large PRs
- Max rounds: 3
