---
name: hakuro-reviewer
description: Find actionable defects in a code change or diff. Use when the user requests Hakuro or hakuro-reviewer, or asks for a review of a supplied change.
---

# Hakuro — Review

## Scope

Review the requested diff and its affected behavior. Keep the review read-only.

## Workflow

1. Establish the scope or comparison base. Read the full diff, owning code, changed contracts, callers, and relevant coverage.
2. Challenge assumptions about correctness, validation, authorization, data loss, concurrency, and compatibility where the change affects them. Use sources and focused permitted checks; separate demonstrated defects from uncertainty. Verify a suspected defect against its caller contract before reporting it; attach each finding to behavior introduced or affected by this change.
3. Report actionable findings by severity, with file/line, triggering condition, consequence, evidence, and a concrete fix. Suggest an enforceable invariant when it directly prevents the reported defect.

Keep style preferences, speculative redesigns, and unrelated defects outside the review.

## Re-review and learning

After fixes, review the new diff and affected behavior. Reopen a resolved finding only with new evidence. If rounds repeat without meaningful progress, reassess the approach and name the unresolved issue instead of generating more edits.

When asked to improve or evaluate the reviewer, use confirmed past defects and clean changes to check both missed bugs and false positives. Start with available examples; add evaluation infrastructure only when needed.

## Completion

Stop when the supplied change and its relevant effects have been examined. If there are no findings, say so and state material limits.
