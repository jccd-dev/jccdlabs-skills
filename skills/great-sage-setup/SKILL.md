---
name: great-sage-setup
description: Set up a repository for the JCCDLabs skills by writing .slime/config.md with its plan, handoff, check, PR, model, and council settings. Use when the user requests Great Sage or great-sage-setup, or asks to set up or reconfigure the skills for a project.
---

# Great Sage: Setup

Write one per-repository config that the other skills read, so plan paths, checks, PR rules, and models aren't fixed inside the skills. Run once per repository and again to change it.

```
.slime/
├── config.md    # every setting, one section per topic
├── plans/       # benimaru-planner writes, kurobe-implementer ticks
└── handoffs/    # only when handoffs are saved as files
```

Start from [the config template](references/config-template.md). Split a section into its own file only once it grows long.

## 1. Explore

Pre-fill answers from evidence before asking anything. Read an existing `.slime/config.md` first and keep its values as defaults.

- Checks: scripts in `package.json`, `Makefile`, `composer.json`, `pyproject.toml`, or CI workflows. Run nothing.
- PRs: the default branch, and the last ~10 merged PRs (`gh pr list --state merged --limit 10 --json baseRefName,mergedBy,author`) for base, merge method, and who merges. Several authors means a shared repository.
- Models: in T3 Code, `orchestrator_capabilities`; elsewhere, the models the host exposes. Unknown is fine.
- Instructions: whether `CLAUDE.md`, `AGENTS.md`, or `CLAUDE.local.md` exist.
- Existing plans or verification skills, such as `docs/plans/`, `.agents/skills/`, or `.claude/skills/`.

## 2. Ask one section at a time

Use the host's question tool, otherwise numbered questions with lettered choices. Put the recommended answer first with its evidence ("main: the last 10 PRs merged into main"). Skip a section the evidence settles; say what was assumed. Sections: Plans, Handoffs, Checks, Code comments, Verification procedures, PRs, Models, Octagram.

Then ask once whether to commit `.slime/`:
- **Commit** (recommended for a solo repository): settings and plans are versioned.
- **Gitignore** (recommended when other people open PRs): add `.slime/` to `.gitignore` so personal settings and plans stay out of the shared repository.

## 3. Draft, then write

Show the full `config.md` draft and wait for approval. Then write `.slime/config.md`, create `.slime/plans/`, and create `.slime/handoffs/` only when handoffs are files. Apply the commit or gitignore choice. If plans exist elsewhere, offer to move them; don't move them unasked.

Add this pointer to the instructions file:

```markdown
## Agent skills
JCCDLabs skills config, plans, and handoffs live in `.slime/`. See `.slime/config.md`.
```

Edit `CLAUDE.md` or `AGENTS.md`, whichever exists; ask when neither exists. When `.slime/` is gitignored, put the pointer in `CLAUDE.local.md` instead, since a committed pointer would name a folder others don't have.

## Finish

List the files written, assumptions made, and values left as defaults. Commit only when the user asks.
