# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. Read the issue and its thread first. Write down what the issue asks for. Write down anything a maintainer already said about how to fix it or what to leave alone.
2. Read the repo facts. Write down every rule the repo states: templates, contribution policy, and any AI-use disclosure requirement. If the repo states nothing, write "none stated".
3. Read the repro evidence. Write down the exact behavior it shows (the input and the output) and the exact steps that produce it. This is the anchor for the whole grade. Every later check is measured against it.
4. Read the plan. Write down its stated cause, its fix, what it says is in and out of scope, the files or areas it names, its test plan, its stated risks and unknowns, and anything written under ## Deviations
5. Read the plan comment last. Write down what it commits to, and whether it responds to what the thread already said.
6. Read the whole package before grading any check. Do not grade while reading.

Why this order: the issue and repro evidence say what the plan has to explain, so the plan is read already knowing what to look for. The comment goes last because it's judged against both the thread and the plan.

## Evidence gathering

In eval mode, use only the package text. Do not fetch anything. In live mode, use the places named under "Live".

1. **Issue and thread.**
   - Eval: the `## Issue` section and the `## Thread highlights` section.
   - Live: the issue page and every comment on it (`gh issue view <number> --comments`).
   - Record: what the issue asks for, and any direction a maintainer gave.

2. **Repo rules.**
   - Eval: the `## Repo facts` block. Read the "bug reports" line and the "contribution policy" line.
   - Live: `CONTRIBUTING.md`, the `.github/` folder (templates), and the README.
   - Record: every stated rule, including any AI-use disclosure rule. If none is stated, record "none stated".

3. **Repro evidence.**
   - Eval: the `## Repro evidence` section.
   - Live: the repro comment already posted on the issue thread. Do not use files in the working folder.
   - Record: the input, the output, and the exact steps that produce them. Also record anything the evidence rules out, such as a control run that works.

4. **The plan.**
   - Eval: the `## Candidate plan` section. Its parts are Diagnosis, Scope, Files, Approach, and Test plan.
   - Live: `plan.md`, including the ## Deviations section at the end. An empty section is fine before the build.
   - Record: the stated cause, the fix, what is in scope and out, the files named, the approach, the test plan, and any stated risks or unknowns. If the plan has no part for risks or unknowns, record "none stated".

5. **The plan comment.**
   - Eval: the `## Candidate plan comment` section.
   - Live: `comment.md`.
   - Record: what it commits to, and whether it answers what the thread said.

6. If a part is missing from the package, record "absent". Do not fill the gap from memory or guess.

## Check execution

1. Run the checks one at a time, in this order: diagnosis-matches-evidence, targets-cause-not-symptom, scope-bounded, executable, test-plan-observable, honest-unknowns, conventions-respected. The first check settles whether the stated cause fits the repro evidence, and the later ones lean on that.
2. For each check, use the facts recorded in Evidence gathering for the parts the rubric names. Go back to the package only to quote a line from those parts. Do not re-read the whole package for every check.
3. Checks that compare two parts must quote both sides: diagnosis-matches-evidence (cause and repro evidence), test-plan-observable (test plan and repro evidence), and conventions-respected (comment, thread, and repo rules). Checks that read one part (scope-bounded, executable, honest-unknowns) can be graded from that part alone.
4. Judge targets-cause-not-symptom against the cause the plan states, even if that cause failed the first check. This check asks whether the fix matches the plan's own cause, not whether the cause is right.
5. Grade each check pass, fail, or unclear, and write one line of evidence for it: a short quote or a fact from the package.
6. If a part of the plan is missing (no stated cause, no scope, no files, no test plan), grade the checks that read it as fail. A plan that leaves it out has not met the condition.
7. Grade unclear only when the thing the plan is measured against is missing: the repro evidence, the thread, or the repo rules recorded as "absent". Unclear means the evidence does not exist, not that you did not look for it.
8. Judge the substance, not the polish. A short plan that meets the pass condition passes. A long, confident plan that does not meet it fails.
9. The rubric decides. If a check passes by its stated condition but feels wrong, it still passes. Note the concern in the summary. Do not change the grade.

## Verdict assembly

1. Count the seven grades: pass, fail, and unclear.
2. Apply the rubric's verdict rule. The verdict is accept only if all seven checks are pass. If any check is fail, the verdict is reject.
3. Treat every unclear as a fail. One unclear check makes the verdict reject.
4. Do not weigh the grades against each other. Six passes and one fail is still reject.
5. Name the deciding check in the output:
   - If the verdict is reject, quote the evidence line for each check that failed or was unclear. If more than one failed, quote all of them.
   - If the verdict is accept, no single check decided it. Say that all seven passed.
6. Write the output in the format SKILL.md gives. End with the fenced JSON block, and put nothing after it. The block must have one entry per check and a verdict of accept or reject, with no third verdict.
7. In live mode, the readable summary before the JSON may also say what the author should fix first, starting with the first failed check in the order from Check execution. The JSON itself only holds the grades and the verdict.