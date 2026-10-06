# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

Where it lives:
- Eval: the `### Diagnosis` part of `## Candidate plan`, and the `## Repro evidence` section.
- Live: the Diagnosis part of `plan.md`, and the repro comment posted on the issue thread.

What good looks like: the stated cause explains the exact behavior the repro evidence shows. It also fits what the evidence rules out, such as a control run that works or a run on another version. If the repro evidence shows the error happens before the code the plan blames is even reached, the plan contradicts it.



## Scope

Where it lives:
- Eval: the `### Scope` and `### Files` parts of `## Candidate plan`, read against what the issue asks for in `## Issue`.
- Live: the same parts of `plan.md`, read against the issue page.

What good looks like: one change with a clear edge. The plan says what is in scope and what is not, and the files it names match that scope. Nothing in it goes beyond what the issue needs.


## Executability

Where it lives:
- Eval: the `### Files` and `### Approach` parts of `## Candidate plan`.
- Live: the same parts of `plan.md`.

What good looks like: specific files and numbered steps in a working order. A stranger could start from it without asking the author anything. "Update the code" with no file named does not count.


## Test plan


Where it lives:
- Eval: the `### Test plan` part of `## Candidate plan`, read against the steps in `## Repro evidence`.
- Live: the Test plan part of `plan.md`, read against the repro comment on the thread.

What good looks like: it re-runs the repro steps (same command, same environment) and says what will be seen before and after the fix, such as the output or the exit code. "Run the tests" only counts if it names which test and what result to expect.

## Honesty

Where it lives:
- Eval: any risks or unknowns the plan states, whether in their own part or as lines inside Diagnosis, Approach, or Test plan. If there are none, record "none stated". Also read how certain the claims in the plan are.
- Live: the same places in `plan.md`, plus the `## Deviations` section at the end.

What good looks like: real uncertainty is named as uncertain ("I think", "not yet confirmed", "I need to check"). Nothing is stated as settled fact that the repro evidence does not support. A change made mid-build is written under Deviations, with what changed and why.

## Comms

Where it lives:
- Eval: `## Candidate plan comment`, read against `## Thread highlights` and the `## Repo facts` block (its "bug reports" and "contribution policy" lines).
- Live: `comment.md`, read against the issue thread and the repo's `CONTRIBUTING.md`, `.github/` templates, and README.

What good looks like: the comment follows every rule the repo states, including any AI-use disclosure rule. If the repo states nothing, that is not a violation. It also answers what maintainers already said in the thread. A comment that would fit any issue does not count as answering them.
