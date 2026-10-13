# Procedure: how this tool grades a PR package

## Read order

1. Read the issue and its thread first. Write down what the issue asks for and anything a maintainer said about how to fix it.
2. Read the repo's stated rules: the PR template, the contribution guide, and any AI-use rule. Write down every section the template asks for, every check it lists, and every disclosure it requires. If the repo states nothing, write "none stated".
3. Read the plan, including anything under `## Deviations`. Write down its scope (what is in and out), the files it names, its approach, and its test plan. This is what the PR is measured against.
4. Read the diff. Write down every file changed and what each hunk does.
5. Read the PR title and description. Write down each change the Summary and Changes sections claim, which boxes are ticked, and what the disclosure says.
6. Read the test evidence last. Write down which commands were run, what output is shown, and which of the repo's listed checks have a result.
7. Read the whole package before grading any check. Do not grade while reading.

Why this order: the plan says what the PR promised, so the diff is read knowing what to look for. The description and the evidence come last because both are judged against the diff.

## Evidence gathering

In eval mode, use only the package text. Do not fetch anything. In live mode, use the places named under "Live".

1. **Issue and thread.**
   - Eval: the `## Issue` section and the `## Thread highlights` section.
   - Live: the issue page and every comment on it.
   - Record: what the issue asks for, and any maintainer direction.

2. **Repo rules.**
   - Eval: the `## Repo facts` section.
   - Live: `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`.
   - Record: each template section, each listed check, and any AI-use rule. If none is stated, record "none stated".

3. **The plan.**
   - Eval: the `## Plan context` section, including any deviation notes in it.
   - Live: `plan.md`, including `## Deviations`.
   - Record: scope, files, approach, test plan, and every deviation.

4. **The diff.**
   - Eval: `### Diff` under `## Candidate PR`.
   - Live: the output of `git diff main...HEAD`. Do not use uncommitted changes.
   - Record: the list of changed files, and one line per hunk saying what it does. Mark any hunk that is a debug line, commented-out code, or an edit the change doesn't need.

5. **The PR title and description.**
   - Eval: `### Title` and `### Description` under `## Candidate PR`. Also read `### Commits`.
   - Live: `pr_draft.md`. The first line is the title.
   - Record: the changes it claims, the boxes ticked, and the AI-use disclosure.

6. **The test evidence.**
   - Eval: `### Test evidence` under `## Candidate PR`.
   - Live: `test_evidence.md`.
   - Record: the before and after of the repro steps with their commands and output, and a result (or a stated reason) for each check the template lists.

7. If a part is missing from the package, record "absent". Do not fill the gap from memory or guess.

## Check execution

1. Run the checks one at a time, in this order: diff-matches-plan, description-matches-diff, tests-show-the-fix, repo-checks-run, diff-is-clean, standards-followed. The first one settles what the diff really does, and the later ones lean on it.
2. For each check, use the facts recorded in Evidence gathering for the parts the rubric names. Go back to the package only to quote a line. Do not re-read the whole package for every check.
3. Checks that compare two parts must quote both sides:
   - diff-matches-plan: a changed file or hunk, and the plan line or deviation that covers it (or the lack of one).
   - description-matches-diff: a change the description claims, and the hunk that does it (or the lack of one).
   - tests-show-the-fix: the plan's test plan or repro steps, and the before and after output.
   - repo-checks-run: a check the template lists, and its result in the evidence.
   - standards-followed: a template section or AI-use rule, and where the description meets it.

   diff-is-clean reads the diff alone.
4. Grade each check pass, fail, or unclear, and write one line of evidence: a short quote or a fact from the package.
5. If something the PR itself should contain is missing (no after output, an empty template section, no disclosure, a check with no result and no reason), grade the check fail.
6. Grade unclear only when the thing the PR is measured against is missing: the plan, the template, or the repo rules recorded as "absent". Unclear means that evidence does not exist, not that you did not look.
7. A shortfall the PR discloses is not a failure. If the diff leaves out something the plan promised, or a check couldn't run, and the description or Deviations says so with a reason, grade the check pass and quote the disclosure. A shortfall that is hidden is a fail.
8. Judge the substance, not the polish. A short PR that meets the pass condition passes. A long, confident one that does not meet it fails.
9. The rubric decides. If a check passes by its stated condition but feels wrong, it still passes. Note the concern in the summary and do not change the grade.

## Verdict assembly

1. Count the six grades: pass, fail, and unclear.
2. Apply the rubric's verdict rule. The verdict is accept only if all six checks are pass. If any check is fail, the verdict is reject.
3. Treat every unclear as a fail. One unclear check makes the verdict reject.
4. Do not weigh the grades against each other. Five passes and one fail is still reject.
5. Pick the deciding check. It is the first check that failed or was unclear, in this order: diff-matches-plan, description-matches-diff, tests-show-the-fix, repo-checks-run, diff-is-clean, standards-followed. Quote its evidence line in the summary as the check the verdict turned on. If the verdict is accept, there is no deciding check. Say that all six passed.
6. Still list every check with its own grade and evidence line in the JSON. The deciding check only decides what the summary leads with.
7. Write the output in the format SKILL.md gives. End with the fenced JSON block, with one entry per check and a verdict of accept or reject, and put nothing after it.
8. In live mode, the summary before the JSON may also say what to fix first. That is the deciding check, then the other failed checks in the same order. The JSON itself only holds the grades and the verdict.