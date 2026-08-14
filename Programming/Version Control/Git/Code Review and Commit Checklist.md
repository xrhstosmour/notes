#git #github #code-review #pull-requests

## Before opening a pull request

- Each commit message is one line, 50-80 chars, describes what the commit does, and the commit's actual diff doesn't do more than the message says.
- No out-of-context changes bundled into a commit, split by concern.
- Squash fixup commits before or during review, don't leave a trail of "fix typo" commits in the final history.
- Test coverage matches the change, and the feature has been manually exercised against the scenarios it's meant to cover.
- Read through your own diff commit by commit before asking for review, it catches most of what a reviewer would flag anyway.

## Requesting review

- Give reviewers real turnaround time, don't send a PR and immediately expect it reviewed.
- Respond to every comment, even a disagreement, silence on a comment reads as ignoring it.
- After addressing feedback, ask explicitly for a final look rather than assuming silence means approval.

## Before merging

- Rebase onto the current default branch, don't merge on top of a stale base.
- Confirm CI is green, never merge around a red check.

## After merging

- Whoever merged (or their team) is responsible for confirming the feature actually works in production.
- Watch application error rates and performance metrics for regressions tied to the change, not just whether it deployed.
