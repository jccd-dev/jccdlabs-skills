---
name: ranga-verifier
description: Prove requested behavior with project checks or interactive evidence. Use when the user requests Ranga or ranga-verifier, or asks to verify existing work against requirements.
---

# Ranga: Verify

Prove the requested behavior against conditions from the request and project requirements. Reuse old evidence only if it still covers the current code, target, and conditions.

## Steps

1. Read project guidance, existing checks, and any verification procedure. Before running anything, confirm its target, effects, dependencies, and whether its test data stays.
2. Give each condition the smallest check that proves it, within task permissions, using the table below. Prefer existing browser or app coverage, then a safe hands-on check for remaining visible behavior.
3. Inspect the real result or user journey. A build or typecheck proves only what it checks; reading code isn't running it. Skipped tests count as not run. Save evidence before cleaning up anything the task created.

| Condition | Evidence |
| --- | --- |
| Pure logic, parsers, calculations | Tests; a browser adds nothing |
| API or service | A real request, checking the response and saved data |
| UI behavior or user journey | Browser: do the journey, then check page state, console errors, and network calls |
| Layout or responsive design | Browser: inspect screenshots at phone and desktop widths |
| Auth and permissions | Browser or real requests as each role, including a denied role |
| Migrations and data | A run on a throwaway copy of the real engine, then a query |
| CLI or background jobs | A real run, checking output, exit code, and side effects |

Use the host's browser tool or the project's browser tests, with one journey per condition. Screenshots prove appearance only; prove behavior from page state, network calls, or saved data.

When the user must run a check, such as on a server, give paste-ready commands: real values, which user, whether `sudo` is needed, and expected output. For an unknown value, give the command that finds it first.

## Evidence

Record the code revision or working-tree state, target, and output. State what the checks can't show. Keep repo, packaged-build, and real-host evidence separate, and name how the target differs from production.

## Finish

Stop when every required condition has evidence. Repeat or widen a check only after a code change, a failure, or a real coverage gap. Verification alone doesn't authorize fixes.

Report each condition as passed, failed, or pending, with evidence or the exact blocker, plus data left behind and important coverage gaps. Missing setup leaves dependent conditions pending, even when the blocker is explained.

Use kaijin-verification-builder when the deliverable is a reusable procedure; recommend it when a condition stays pending across rounds.
