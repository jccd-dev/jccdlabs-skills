---
name: great-sage-setup
description: Set up a repository for the JCCDLabs skills by writing .slime/config.md with its models, council, plans, and handoff settings. Use when the user requests Great Sage or great-sage-setup, or asks to set up or reconfigure the skills for a project.
---

# Great Sage: Setup

Write one per-repository config that the other skills read for the settings they can't derive from the repository. Run once per repository and again to change it.

```
.slime/
├── config.md    # settings only, one section per topic
├── plans/       # benimaru-planner writes, kurobe-implementer ticks
└── handoffs/    # only when handoffs are saved as files
```

Start from [the config template](references/config-template.md). The config holds only its four sections: Models, Octagram, Plans, Handoffs. Don't add checks, PR rules, commit rules, or other instructions; the skills find those in the repository.

## 1. Explore

Pre-fill answers from evidence before asking anything. Read an existing `.slime/config.md` first and keep its values as defaults.

- Models: in T3 Code, `orchestrator_capabilities`; elsewhere, the models the host exposes. Unknown is fine; keep the template rows.
- Existing plans, such as `docs/plans/`.
- Whether other people open PRs (`gh pr list --state merged --limit 10 --json author`).

## 2. Ask one section at a time

Use the host's question tool, otherwise numbered questions with lettered choices. Put the recommended answer first with its evidence. Skip a section the evidence settles; say what was assumed. Sections: Models, Octagram, Plans, Handoffs.

Then ask once whether to commit `.slime/`:
- **Commit** (recommended for a solo repository): settings and plans are versioned.
- **Gitignore** (recommended when other people open PRs): add `.slime/` to `.gitignore`.

## 3. Draft, then write

Show the full `config.md` draft and wait for approval. Then write `.slime/config.md`, create the plans folder, and create the handoffs folder only when handoffs are files. Apply the commit or gitignore choice. If plans exist elsewhere, offer to move them; don't move them unasked.

Write nothing outside `.slime/` and `.gitignore`. The skills read `.slime/config.md` directly, so `AGENTS.md`, `CLAUDE.md`, and `CLAUDE.local.md` need no pointer.

## Finish

List the files written, assumptions made, and values left as defaults. Commit only when the user asks.
