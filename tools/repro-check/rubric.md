# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

# Rubric: is this reproduction package ready to post?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| env-recorded | The repro report's environment record (tool/library version, OS, relevant config). | Pass if the report states both the exact tool/library version and the OS it ran on. Fail if either is missing or given only vaguely (e.g. "latest", "a Mac"). | required |
| behavior-matches | The artifacts in the repro report (output, error text, logs, screenshots), read against the issue's description of the bug. | Pass if the artifact demonstrates the specific behavior the issue describes. Also pass if the report is an honest cannot-reproduce: the artifact must show a genuine, complete attempt using the issue's exact reported input/steps — a differing environment is expected and does not disqualify a cannot-reproduce, as long as the report states what differed. Fail if the artifact shows a different or only adjacent problem, the attempt skips or substitutes part of what the issue asked to be run, or a cannot-reproduce doesn't say what differed. | required |
| honest-outcome | The repro report's stated conclusion (reproduced / could not reproduce / partial), compared against what the artifacts actually show. | Pass if the stated outcome matches the evidence — including an honest "could not reproduce" backed by a real attempt. Fail if the report claims more certainty or success than the evidence supports. | required |
| conventions-respected | The claim comment and repro comment text, checked against the repo's stated contribution rules (issue template, CONTRIBUTING file, disclosure policy). | Pass if the comments follow every rule the repo states for contributors, including disclosing AI assistance if the repo's policy requires it. Fail if any stated repo rule is violated, including a missing required disclosure. | required |
| evidence-traceable | How the artifacts are presented in the repro report — a pasted excerpt vs. a link/attachment to the complete raw output. | Pass if the report links to or attaches the full raw output/log, so a maintainer could verify nothing relevant was cut. Fail or unclear if only a trimmed excerpt or paraphrase is given with no way to see the rest. | preferred |
| steps-complete | The repro report's listed reproduction steps. | Pass if a stranger could reach the same triggering state — every value that actually matters for triggering the behavior is given exactly, either written out or by precise reference to a value already stated elsewhere (like the issue's own exact input). Incidental setup details that don't affect the bug can be described rather than transcribed. Fail if any value that matters for triggering the behavior is left vague, generic, or unstated (e.g. "run the command" without saying which one). | required |

## Verdict rule

Accept only if every required check passes. A required check graded `unclear` counts as `fail`. Preferred checks are informational only: a `fail` or `unclear` grade on a preferred check never changes the verdict — a package can still be `accept` even if `evidence-traceable` fails.




