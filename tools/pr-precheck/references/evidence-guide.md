# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

Where it lives:
- Package: the plan is in `## Plan context`. Its scope, its "Not in scope" line, its "Files" line, and any deviation note are all there. The diff is `### Diff` under `## Candidate PR`. The description's claims are in `### Description` and `### Commits`.
- Live: `plan.md` (scope, files, and `## Deviations`), the output of `git diff main...HEAD`, and the Summary and Changes in `pr_draft.md`.

What good looks like:
- Every changed file and hunk falls inside the plan's files and scope, or inside a deviation note.
- Everything the plan promised is in the diff, or its absence is written down in a deviation note or the description.
- The description says what the diff does. It claims nothing the diff doesn't do, and it leaves out nothing the diff does.

Silent drift goes both ways: the diff does more than the plan with no note, or less than the plan with no note. A description that claims more or less than the diff delivers is also drift. An honest deviation fixes the mismatch.

## Test evidence (harness category: not-tested)

Where it lives:
- Package: `### Test evidence` under `## Candidate PR`. Read it against the test plan and the repro evidence in `## Plan context`. The checks the repo asks for are in the "pull requests" line of `## Repo facts`.
- Live: `test_evidence.md`, read against the test plan in `plan.md` and the checks the PR template lists.

What good looks like:
- The repro steps are shown as the commands that were run, with their output before and after. The after output shows the fix working.
- Every check the repo lists has its result shown. A check that failed or couldn't run says so, with the reason.
- If the repo lists no checks, nothing is missing.


"Tests pass" with no check named is not evidence. A result written next to the command it came from counts. Controls and test counts that are only mentioned don't need their own output if the main repro is shown before and after.


## Diff quality (harness category: unreviewable)

Where it lives:
- Package: `### Diff` under `## Candidate PR`, and the list in `### Commits`.
- Live: `git diff main...HEAD`, and `git diff main...HEAD --stat` for the file list.

What good looks like:
- The fix is easy to see, and nothing unrelated rides along.
- Every added or removed line belongs to the change the plan describes.

Signs of debris are debug lines, commented-out code, formatting changes, and drive-by edits to files or lines the change doesn't need. Unchanged context lines are not debris. Only added or removed lines count.

## Standards and comms (harness category: standards-wall)

Where it lives:
- Package: `## Repo facts` holds the "pull requests" line (the template sections or the asks) and the contribution policy, including any AI-use rule. `## Thread highlights` holds any explicit maintainer direction. The PR text is `### Title`, `### Description`, and `### Commits` under `## Candidate PR`.
- Live: `.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md`, and the issue thread, read against `pr_draft.md`.

What good looks like:
- Every section the repo's template asks for is filled with real content, and the issue is named.
- Every ask the repo states is followed. For example, "keep PRs small and reference the issue" means the PR is small and names the issue.
- If the repo asks for an AI-use disclosure, it is there.
- Boxes are ticked only where the test evidence backs them.
- Any explicit maintainer direction in the thread is followed or answered.

If the repo states nothing, record "none stated". That is not a violation. Boilerplate or an ignored ask is a fail. In your own PR, the course asks for an AI-use disclosure in Notes for Reviewers even where the repo doesn't.

Whether the description matches the diff belongs under Plan fidelity, not here.