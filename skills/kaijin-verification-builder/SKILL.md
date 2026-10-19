---
name: kaijin-verification-builder
description: Use when explicitly asked to create or update a reusable verification skill for a specific project.
---

# Kaijin — Create Verification

Create a reusable verification skill grounded in the project's actual environment. Reuse its harness; building a missing harness is a separate scope decision.

1. Inspect the requested app surfaces, launch commands, readiness signals, existing checks and drivers, authentication needs, safe targets, fixtures, and cleanup. Confirm commands from the repository or tool documentation.
2. Write a compact project-specific SKILL.md in the host's supported project location. Map relevant journeys to launch, drive, observable assertions, evidence output, and cleanup. Include prerequisites, precise failure signals, and when each check applies. Distinguish required checks from conditional checks so ordinary changes do not trigger every journey. Move substantial conditional detail into referenced files.
3. Exercise one representative safe journey using the written procedure within task permissions. Confirm evidence survives cleanup. If execution is unavailable, mark the procedure unverified and record the exact blocker.

Keep credentials out of instructions and artifacts. Cleanup covers only fixtures and processes created for this task.

Return the skill's path, demonstrated journey, retained evidence, and uncovered surfaces. Honor the requested invocation policy and existing project conventions.
