# Rubric: is this a good first issue?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer_merging | Last 5 default-branch commits and their authors (Repo facts) | At least one of the last 5 commits is from the last 60 days and was made by a person. A bot commit only counts if it merged a person's PR. | required |
| maintainer_replying | Maintainer first-response sample (Repo facts) and the author_association on comments | An Owner, Member, or Collaborator commented in the last 30 days, and maintainers answer issues in the response sample. | preferred |
| repo_in_use | Archived flag, latest release, and last push to any branch (Repo facts) | The repo is not archived. It has a release from the last 12 months, or if it has no releases, a push from the last 90 days. | required |
| scope_bounded | Issue title | The title asks for one specific change, such as add, fix, update, or remove something, and is not a question. | required |
| unclaimed | Issue state, assignees, linked PRs, and comments | The issue is open, has no assignee, and has no open linked PR. Nobody has claimed it in the last 30 days without a maintainer answering. If the sidebar and the thread disagree, believe the thread. | required |
| ai_policy | Contribution policy line (Repo facts) | The repo does not ban AI-generated contributions. Conditions like disclosure or testing are fine. No stated policy is a pass. | required |
| spec_included | Issue body | The issue says what needs fixing and where to look, such as a file, an error message, or steps to reproduce. | preferred |

## Verdict rule
Accept the issue if every required check passes. Reject it if any required check fails. If a required check is `unclear`, count it as a fail. Preferred checks never change the verdict. Among accepted issues, list the ones that pass more preferred checks first, then the ones with the most recent maintainer comment.

