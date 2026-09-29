# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->
# Evidence guide: where proof lives in a reproduction package

## Environment

| Where it lives | Live mode | Eval bundle |
|---|---|---|
| The environment record | The draft repro report — usually a short setup line near the top, before the steps | The repro report section of the bundle |
| What version the bug actually targets | The issue's body/thread on GitHub | The issue context section of the bundle |

What good looks like: an exact tool/library version and an exact OS, not vague words like "latest" or "a Mac." If the version reproduced is different from the version the issue names, the report says so out loud instead of staying quiet about it.

## Steps

| Where it lives | Live mode | Eval bundle |
|---|---|---|
| The reproduction steps | The draft repro report's ordered list of commands/actions | The repro report section of the bundle |
| Any steps the issue already suggests | The issue's body/thread | The issue context section of the bundle |

What good looks like: every step names its exact input — nothing is left for the reader to guess (e.g. "run the command" without saying which one is not enough). Someone with zero other context could type each line and land in the same state.

## Behavior shown


| Where it lives | Live mode | Eval bundle |
|---|---|---|
| The artifacts (output, error text, logs, screenshots) | The draft repro report | The repro report section of the bundle |
| What the bug is supposed to look like | The issue's description | The issue context section of the bundle |

What good looks like: the artifact shows the *same* behavior the issue describes, using the same input the issue used — not a different problem, and not a swapped-out input.

A "couldn't reproduce it" result can also pass. It's fine if the environment was different (OS, shell, version) — that's often *why* it didn't reproduce — as long as the report says what was different. It's not fine if the input itself was quietly changed (a different flag, a different file, different arguments) and reported as if it were the same test.

## Honesty

| Where it lives | Live mode | Eval bundle |
|---|---|---|
| The report's stated conclusion (reproduced / could not reproduce / partial) | The draft repro report's closing line(s) | The repro report section of the bundle |
| The evidence backing that conclusion | The same report's artifacts | The same section |

What good looks like: the words match what the evidence actually shows. Claiming "reproduced" off a shaky or unclear artifact is overclaiming — a fail. An honest, well-evidenced "I could not reproduce this" is a pass, not a consolation prize.

## Comms

| Where it lives | Live mode | Eval bundle |
|---|---|---|
| The repo's contribution rules | `CONTRIBUTING.md` in the repo root or `.github/` folder; issue/PR templates | The repo-facts block of the bundle |
| The actual comment text | The draft claim comment and repro comment | The claim comment / repro report sections of the bundle |

What good looks like: the comments follow every rule the repo states — including disclosing AI assistance if the repo's policy requires it. If the repo states nothing, that's not a violation; silence passes.

## Evidence traceability (preferred check)

| Where it lives | Live mode | Eval bundle |
|---|---|---|
| How the artifact is presented | The draft repro report — is there a link/attachment to the full raw output, or just a pasted snippet? | The repro report section of the bundle |

What good looks like: a maintainer can click through or open something and see the *complete* raw output, not just the lines the student chose to paste. A trimmed excerpt with nothing behind it is unclear or a fail on this check — but remember, this one is preferred, so it never blocks an otherwise-ready package from being accepted.

