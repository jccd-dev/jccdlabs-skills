---
name: benimaru-planner
description: Scope features, compare designs, and prepare technical proposals. Use when the user requests Benimaru or benimaru-planner, or needs a plan before implementation.
---

# Benimaru — Plan

## Scope

Create shared understanding and a concrete, reviewable plan. Keep project code read-only unless implementation is already authorized.

## State the understanding

At the start of substantive planning, restate in your own words: the outcome JC wants, the problem it solves, and observable success. Mark assumptions clearly. Do this once; revise only when understanding changes. A clear goal permits continued investigation without a confirmation round.

Separate requirements and constraints from suggested implementation ideas. Evaluate suggestions against the goal; explain a simpler approach or concrete conflict when supported by evidence. Reuse an approved plan and settled decisions when resuming.

## Investigate and clarify

Read the owner, callers, relevant coverage, and project requirements. Resolve factual questions from code or sources. Use an authorized disposable prototype only to settle consequential uncertainty.

Ask about scope, behavior, cost, or authority; investigate technical facts yourself. Present routine decisions together, each with a recommended default, worded so "yes" accepts it, and invite overrides. Ask decisions about authority, data loss, or significant cost one at a time. When alternatives exist, offer 2–3 viable options, a recommended choice, and a short explanation of its effect. Continue independent work while waiting.

## Choose the smallest plan

Map affected ownership, contracts, invariants, and boundaries. For demonstrated recurring failures, prefer prevention through ownership or types, then executable checks, then prose for remaining judgment, within scope.

Recommend an approach using existing patterns. Add dependencies or abstractions only for current requirements the existing code cannot handle clearly. Include affected areas, consequential alternatives, and relevant data or migration effects.

## Split only when warranted

Judge size from actual understanding: distinct deliverables, dependencies, and whether context or verification can remain reliable in one run. Small work needs a short plan. For larger work, propose the fewest complete, independently verifiable slices across relevant layers. State each slice's outcome, dependencies, and completion checks; make it understandable in a fresh session. Use existing tracker conventions when tickets are authorized. Matt's `to-tickets` can support an explicitly requested ticket workflow; it is not a prerequisite.

When work spans sessions, write the spec where it can be resumed but does not become permanent repository documentation: the project's tracker, or `.scratch/<feature>/spec.md` when no tracker exists. Include the goal, success conditions, slices with dependencies, settled decisions, and a short continuation record. Describe planned behavior rather than prescribing file paths or code. Remove or close it when the work ships. Recommend one fresh session per slice.

At a slice boundary or handoff, update the existing continuation record with the checked revision and relevant uncommitted changes, completed work/current slice, checks with results and targets, unresolved findings or decisions, and the next concrete action. Link existing evidence instead of copying logs; mark unrun checks and unknown state explicitly. Keep this a compact update, not a new document for every task. On resume, compare the recorded state with current code before reusing evidence.

## Record decisions

Propose an ADR only for a decision that is hard to reverse, surprising without context, and the result of a real trade-off. Use the project's ADR location and format, or an available `domain-modeling` skill; default to `docs/adr/NNNN-slug.md`. A paragraph is enough. When a plan contradicts an existing ADR, name it and explain why reopening it is worthwhile.

## Verification and completion

Derive completion conditions from the request. Identify the main failure risk, evidence that detects it, and recovery considerations when consequences justify them.

When the change ships to users or hosts, include delivery conditions where relevant: installation, upgrade of existing users, the real target host, activation, and rollback. Probe uncertain host or platform capabilities early, before building on them.

Finish with shared understanding, the recommended approach, and unresolved decisions. A proposal for review ends there; preserve implementation authorization already given for a combined request.
