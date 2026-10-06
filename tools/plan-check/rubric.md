# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis-matches-evidence | The plan's stated cause, read against what the repro evidence actually shows. | Pass if the stated cause explains the exact behavior the repro evidence shows. Fail if the cause contradicts the evidence, or isn't tied to it at all. | required |
| targets-cause-not-symptom | The plan's described fix, read against its own stated cause. | Pass if the fix addresses the cause itself. Fail if the fix only patches the symptom (for example, catching an error instead of fixing what produces it) while the cause goes unaddressed. | required |
| scope-bounded | The plan's scope statement — what's in, what's out, which files or areas are named. | Pass if the plan is one bounded change with a clear edge: it says what it will touch and what it won't. Fail if the scope is vague, unbounded, or includes unrelated changes beyond what the issue needs. | required |
| executable | The plan's described approach — files or areas to touch, order of work. | Pass if a stranger could start working from the plan without asking the author anything — specific files, specific steps. Fail if it's vague, like "update the code" with no file or approach named. | required |
| test-plan-observable | The plan's test plan, read against the repro evidence. | Pass if the test plan reuses or clearly maps to the repro steps, and states exactly what should be seen before and after the fix. Fail if it's vague, or doesn't tie back to the actual repro evidence. | required |
| honest-unknowns | The plan's stated risks and unknowns. | Pass if real uncertainty is named as uncertain. Fail if the plan states something as settled fact that the evidence doesn't actually support. | required |
| conventions-respected | The plan comment, read against the issue thread and the repo's stated rules (templates, contribution policy, AI-use disclosure). | Pass if the comment follows every rule the repo states, and responds to anything a maintainer already said in the thread rather than ignoring it. Fail if it breaks a stated rule or ignores a maintainer's existing direction. | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept only if every required check passes. A required check graded `unclear` counts as `fail`. There are no preferred checks this week — all seven cover failure modes that actually get bad plans posted, so none of them can be optional.



