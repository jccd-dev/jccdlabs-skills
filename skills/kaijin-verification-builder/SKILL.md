---
name: kaijin-verification-builder
description: Create or update reusable project verification skills. Use when the user requests Kaijin or kaijin-verification-builder, or needs a repeatable project verification procedure.
---

# Kaijin: Create Verification

Create a reusable verification skill based on the project's real environment. Reuse its harness; building a missing harness is a separate scope decision.

## Steps

1. Inspect the requested app surfaces, launch commands, readiness signals, existing checks and drivers, authentication needs, safe targets, fixtures, and cleanup. Confirm commands from the repository or tool docs.
2. Write a compact project SKILL.md in the host's supported project location. Map each relevant journey to launch, drive, observable assertions, evidence output, and cleanup. Include prerequisites, precise failure signals, and when each check applies. Separate required from conditional checks so ordinary changes don't trigger every journey. Move long conditional detail into referenced files.
3. Run one representative safe journey from the written procedure, within task permissions. Confirm evidence survives cleanup. If it can't run, mark the procedure unverified and record the exact blocker.

## Coverage

For complex projects, keep a small map of important behaviors, their checks, and gaps. Reuse an existing map.

Before handoff, see each new check fail against a safe deliberate break or known-bad state; a check never seen failing proves nothing. A procedure never executed is a draft. Record covered paths and the commit the procedure last synced to.

Turn a recurring mechanical mistake into an automatic check instead of more prose. When a project already has failures, fail only on new ones so the old ones can't hide them.

## Maintenance

When updating a procedure, compare covered paths since its sync commit. Classify each check as in sync, updated, product bug, or blocked. Update the procedure from the code, not the result. Report product bugs instead of weakening checks, and keep procedure updates separate from product fixes.

## Safety

Keep credentials out of instructions and artifacts. Clean up only fixtures and processes this task created.

## Finish

Return the skill's path, demonstrated journey, retained evidence, and uncovered surfaces. Follow the requested invocation policy and existing project conventions.
