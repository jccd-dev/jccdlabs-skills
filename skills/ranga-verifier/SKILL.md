---
name: ranga-verifier
description: Prove requested behavior with project checks or interactive evidence. Use when the user requests Ranga or ranga-verifier, or asks to verify existing work against requirements.
---

# Ranga — Verify

## Scope

Prove the requested behavior against acceptance conditions derived from the request and project requirements. Reuse recorded evidence only when it covers the current code, target, and conditions.

## Workflow

1. Inspect project guidance, existing checks, and any project verification procedure. Confirm the target, command effects, dependencies, and fixture persistence before execution.
2. Map each condition to the narrowest meaningful evidence. Run required checks within task permissions; use existing browser or app coverage, then a safe interactive check for remaining visible behavior.
3. Inspect the actual artifact or user journey. A build or typecheck proves only what it checks. Capture observed results and retain evidence before cleaning up task-created fixtures or processes.

## Evidence

Record the checked code revision or working-tree state, target, and check output. State what the checks cannot establish. Keep repository, packaged-artifact, and real-host evidence separate, and name how the checked target differs from production.

## Completion

Stop after the required conditions have evidence. Repeat or broaden checks only for changed code, a failure, or a concrete coverage gap. Verification alone does not authorize repairs.

Report each condition as passed, failed, or pending with evidence or a precise blocker. Report persistent data created and material coverage limits.

Use kaijin-verification-builder when the requested deliverable is a reusable project procedure; recommend it when the same condition stays pending across verification rounds. Missing setup leaves dependent conditions pending; describing a blocker does not verify them.
