---
name: shion-pr
description: File a pull request, check whether one is ready to merge, or review someone else's. Use when the user requests Shion or shion-pr, or asks to file, open, check, or review a PR.
---

# Shion: Pull Requests

Three jobs: file the user's PR, check a PR before merge, and review another author's PR. Use the repository's default branch and its recent merged PRs as the convention for base branch and merge method, and project guidance and scripts for check commands.

Never merge, approve, post a comment, or push unless the user asked for that action in this conversation.

## File a PR

1. Check whether a PR for this branch already exists; update it instead of opening a second one.
2. Review the diff against the base. Confirm it matches the goal and contains no stray files.
3. Title: follow the repository's title convention from recent merged PRs and history. Say why the change matters, not how. "Cut websocket frame size by 70%" beats "negotiate permessage-deflate on the websocket".
4. Body, in this order:

```markdown
<The problem, in one or two plain sentences from the user's original request. Then the fix in one or two more.>

## Evidence
<What proves it: checks run and results, before/after screenshots or output, the journey tried. Say what was not checked.>

## Merge danger
<One-way or two-way door. What breaks, for whom, if this is wrong. How to roll back.>

## Council review
<Only when octagram-council ran: its score table.>

Created with <model> in <harness>.
```

Don't open with a list of changed functions. Use the model name the host reports and include subagent models that wrote part of the change; if the model is unknown, name only the harness.

5. Check the title, body, and attachments for secrets and private details.
6. Open a real PR, not a draft. If `gh pr create` fails on the GraphQL rate limit, use REST: `gh api repos/<owner>/<repo>/pulls -f title=... -f head=... -f base=... -F body=@<file>`.
7. Return the PR URL.

## Check before merge

Report each item as pass, fail, or unknown with its evidence:

- Checks on the latest commit are green, or the repository has no CI (say so). A check that never ran is unknown, not green.
- The branch is up to date with the base and has no conflicts.
- The diff still matches what the title and body claim.
- Required reviews are present when the repository requires them.

Verdict: **ready**, or **blocked** with the failing items. Stop there. Merge only when the user says to, with the repository's merge method.

## Review another author's PR

1. Read the PR description, the full diff, and the code it touches. Note the base branch and size.
2. Summarize by feature area, not file by file: what each area now does differently.
3. Flag risk areas: authentication and authorization, payments and money, migrations and data changes, deletions, and public API changes.
4. Review with hakuro-reviewer. Use octagram-council instead only when the user asks; say which in one line.
5. Give a verdict: approve, approve with comments, or request changes, with the findings behind it.
6. Draft the comments. Show them to the user and post only after the user says to post.

## Comments

Every comment posted on the user's behalf starts with this callout:

```markdown
> [!NOTE]
> 🤖 **<model> responding on behalf of <user>**

The comment starts here.
```

Use the model name the host reports and the user's GitHub login. Don't add a signature, heading, or second attribution. Skip the callout for text the user asked to post verbatim, PR descriptions, and commit messages.

Lead with the conclusion, cite the code line, check, or reproduction, and separate verified fact from judgment. Check for secrets before posting. After posting, confirm GitHub returned the comment or review URL. Resolve a thread only after its reply posted.

## Finish

Return the PR URL, the verdict, or the drafted comments, plus anything unverified.
