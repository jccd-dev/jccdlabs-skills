---
name: kaijin-verification-builder
description: Create or update reusable project verification skills. Use when the user requests Kaijin or kaijin-verification-builder, or needs a repeatable project verification procedure.
---

# Kaijin — Create Verification

## Scope

Create a reusable verification skill grounded in the project's actual environment. Reuse its harness; building a missing harness is a separate scope decision.

## Workflow

1. Inspect the requested app surfaces, launch commands, readiness signals, existing checks and drivers, authentication needs, safe targets, fixtures, and cleanup. Confirm commands from the repository or tool documentation.
2. Write a compact project-specific SKILL.md in the host's supported project location. Map relevant journeys to launch, drive, observable assertions, evidence output, and cleanup. Include prerequisites, precise failure signals, and when each check applies. Distinguish required checks from conditional checks so ordinary changes do not trigger every journey. Move substantial conditional detail into referenced files.
3. Exercise one representative safe journey using the written procedure within task permissions. Confirm evidence survives cleanup. If execution is unavailable, mark the procedure unverified and record the exact blocker.

## Feature coverage

For complex projects, keep a small feature-to-check map of important behaviors, their checks, and remaining gaps. Reuse an existing map when available.

Before handoff, see each new check fail against a deliberate safe break or a known-bad state; a check never seen failing proves nothing. Record the covered paths and the commit the procedure was last synced to.

## Maintenance

When updating an existing procedure, compare covered paths since its sync commit. Classify each check as in sync, updated, product bug, or blocked. Update the procedure from the code, not from the result; report product bugs instead of weakening checks, and keep procedure updates separate from product fixes.

## Safety and cleanup

Keep credentials out of instructions and artifacts. Cleanup covers only fixtures and processes created for this task.

## Completion

Return the skill's path, demonstrated journey, retained evidence, and uncovered surfaces. Honor the requested invocation policy and existing project conventions.
