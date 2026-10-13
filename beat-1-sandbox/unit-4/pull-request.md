# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s3/pull/170

**Branch**

fix/54-indented-section-headers

## Eval iterations

**Run history**

```
cd ~/Codepath/ai301/ai301-unit4-starter/eval

# Run 1: smoke run, 3/3
python3.12 run_eval.py --skill ~/.claude/skills/pr-precheck --limit 3

# Run 2: first full run, 16/20
python3.12 run_eval.py --skill ~/.claude/skills/pr-precheck --save-run eval-run.txt

# Run 3: re-grade of the four misses, 1/4
python3.12 run_eval.py --skill ~/.claude/skills/pr-precheck --only pkg-05,pkg-08,pkg-11,pkg-19 --out results.json

# Run 4: after editing tests-show-the-fix and repo-checks-run, with canaries, 9/9
python3.12 run_eval.py --skill ~/.claude/skills/pr-precheck --only pkg-05,pkg-11,pkg-19,pkg-04,pkg-07,pkg-10,pkg-14,pkg-01,pkg-20 --out results.json

# Run 5: confirming full run, saved as eval-run.txt, 19/20
python3.12 run_eval.py --skill ~/.claude/skills/pr-precheck --save-run eval-run.txt
```

Scores in order: 3/3, 16/20, 1/4, 9/9, 19/20

The last line of `eval-run.txt` reads: `agreement: 19/20 scored items  (bar: 18/20: PASS)`.

**Package analysis**

pkg-08 (jesseduffield/lazygit#5883, category `clear-accept`). My rubric decided reject, and the gold label is accept. The row in `eval-run.txt` reads: `pkg-08  clear-accept    accept  reject   NO     failed: repo-checks-run, standards-followed`.

The PR description says: "Requirements: cheatsheets regenerated (no binding changes, no diff); code formatted; integration test added; new error text internationalised; no UserConfig changes." The test evidence says: "Integration test `stash_untracked_only_errors` passes; `go test ./...` passes; `go generate ./...` produces no cheatsheet diff." It never shows a formatting command.

The grader's evidence for `standards-followed` was: "The 'code formatted' checklist box is ticked in the description with no backing result in the test evidence, violating 'every ticked box is backed by the test evidence.'" My rubric reads it this way because the `standards-followed` pass condition says "every ticked box is backed by the test evidence." The repo's template lists "code formatted", and the evidence has no result for it.

The gold label disagrees, so my rubric is stricter than the answer key here. I kept it, because the same rule is what catches a PR that ticks a box it didn't earn.

**Check rationale**

From `rubric.md`, as it reads now:

| tests-show-the-fix | The test evidence, read against the plan's test plan and the repro steps. | Pass if the issue's own repro is shown before and after the change, each with its command and its result, and the after result shows the fix working. A result written next to its command counts (for example, a command that prints nothing on success, with the outcome beside it). Extra checks the evidence only mentions, such as a control run or a test count, don't need their own output. Fail if the before or the after of the repro is missing, or the after result doesn't show the fix working. | required |

My first version failed any result that was "described but not shown". After my first full run (16/20), pkg-05, pkg-11 and pkg-19 failed this check even though they showed the issue's repro before and after. For pkg-11 the grader wrote: "Before output shows the real error text, but after results are only described." For pkg-05 it wrote: "'Same-key redefine prints the one-time warning' and 'keybindings list confirms' are asserted but never shown running."

I rewrote the rule so a result written next to its command counts, and a control or test count that is only mentioned doesn't need its own output. I kept the requirement for a before and an after of the issue's own repro. After the edit, pkg-05, pkg-11 and pkg-19 all agreed.

**Trade-offs**

Loosening `tests-show-the-fix` could let a bad package through, so I re-ran canaries with `--only`: the three packages I was fixing, all four `not-tested` packages (pkg-04, pkg-07, pkg-10, pkg-14), and both `standards-wall` packages (pkg-01, pkg-20). The result was `agreement: 9/9 scored items`, with every canary still rejecting.

The cost is that a PR can now pass with an "after" result that is only a line written next to its command, with no full output. I accept that, because the full run still ended at `19/20 scored items  (bar: 18/20: PASS)`.

I also accept one miss: pkg-08 was rejected in both full runs, and I chose not to loosen `standards-followed` to flip it.
