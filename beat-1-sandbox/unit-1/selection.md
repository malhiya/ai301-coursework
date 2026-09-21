# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/54 

**Verdict output**
```
  #54 — Resume section detection fails on text with leading whitespace
  - scope_bounded: pass — one specific bug in one function.
  - spec_included: pass — names file/function, runnable repro snippet with
    observed vs. expected output, and the exact failing tests.
  - Verdict: accept
{
      "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/54",
      "checks": [
        {"name": "maintainer_merging", "grade": "pass", "evidence": "Last 5 
  default-branch commits (through 2026-09-16) all authored by human Aburke225"},
        {"name": "maintainer_replying", "grade": "pass", "evidence":
  "Collaborator Aburke225 commented 2026-09-16 closing resolved issues in the 
  response sample"},
        {"name": "repo_in_use", "grade": "pass", "evidence": "Not archived; no 
  releases but pushed_at 2026-09-16, within 90 days"},
        {"name": "scope_bounded", "grade": "pass", "evidence": "Title: 'Resume 
        {"name": "scope_bounded", "grade": "pass", "evidence": "Title: 'Resume section
  detection fails on text with leading whitespace' — one specific bug"},
        {"name": "unclaimed", "grade": "pass", "evidence": "state=open, assignees=[], no
  cross-referenced PRs, comments=0"},
        {"name": "ai_policy", "grade": "pass", "evidence": "No
  CONTRIBUTING.md/AI_POLICY.md/AGENTS.md found (all 404); PR template has no AI-disclosure
  cross-referenced PRs, comments=0"},
        {"name": "ai_policy", "grade": "pass", "evidence": "No
  CONTRIBUTING.md/AI_POLICY.md/AGENTS.md found (all 404); PR template has no AI-disclosure
  clause"},
        {"name": "spec_included", "grade": "pass", "evidence": "Body names
  `_detect_sections()` in `resume_parser.py`, gives runnable repro code with observed vs
  expected output, and lists 3 related failing tests"}
      ],
      "verdict": "accept"
    }
```

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
   Summary

  Repo-level facts (apply to all three issues): not archived; last push
  2026‑09‑16 (4 days old, no releases but within 90‑day window) → repo_in_use
  pass. Last 5 commits all from a human (Aburke225) dated 2026‑09‑16 →
  maintainer_merging pass. A collaborator (Aburke225) commented on issues as
  recently as 2026‑09‑16, closing resolved issues → maintainer_replying pass. No
  CONTRIBUTING.md/AI policy file found anywhere in the repo, and the PR
  template has no AI-disclosure requirement → ai_policy pass (silence).

  All three issues: open, no assignee, no linked/cross-referenced PRs, zero
  comments → unclaimed pass.

  #61 — Health check DB probe passes a raw SQL string
  - scope_bounded: pass — title names one specific fix (SQLAlchemy 2.x text()
    wrapping).
  - spec_included: pass — names file (api/routes/health.py), exact error, repro
    steps.
  - Verdict: accept
  
  #54 — Resume section detection fails on text with leading whitespace
  - scope_bounded: pass — one specific bug in one function.
  - spec_included: pass — names file/function, runnable repro snippet with
    observed vs. expected output, and the exact failing tests.
  - Verdict: accept

  #45 — No property-based tests for the PII scrubber
  - scope_bounded: pass — one bounded deliverable (hypothesis-based tests for
    one module), not a question or umbrella.
  - spec_included: pass — names the test file and gives an effort estimate
    (4–6h).
  - Verdict: accept
  
  Ranking: the rubric's preferred checks tie all three (all pass
  maintainer_replying and spec_included), so the fit profile
  (Python/JS/TS/React/Java, wants tier‑1/2, avoid Docker/paid-API setup) breaks
  the tie: #54 ranks first — it's a pure-Python parsing bug with a
  self-contained repro, no DB/Docker/service needed to verify. #61 is second —
  also tier‑1 and a one-line fix, but touches the DB health-check path. #45 is
  third — tier‑2, a bigger 4–6h effort requiring learning hypothesis rather than
  a quick bug fix.

  [
    {
      "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/54",
      "checks": [
        {"name": "maintainer_merging", "grade": "pass", "evidence": "Last 5 
  default-branch commits (through 2026-09-16) all authored by human Aburke225"},
        {"name": "maintainer_replying", "grade": "pass", "evidence":
  "Collaborator Aburke225 commented 2026-09-16 closing resolved issues in the 
  response sample"},
        {"name": "repo_in_use", "grade": "pass", "evidence": "Not archived; no 
  releases but pushed_at 2026-09-16, within 90 days"},
        {"name": "scope_bounded", "grade": "pass", "evidence": "Title: 'Resume 
        {"name": "scope_bounded", "grade": "pass", "evidence": "Title: 'Resume section
  detection fails on text with leading whitespace' — one specific bug"},
        {"name": "unclaimed", "grade": "pass", "evidence": "state=open, assignees=[], no
  cross-referenced PRs, comments=0"},
        {"name": "ai_policy", "grade": "pass", "evidence": "No
  CONTRIBUTING.md/AI_POLICY.md/AGENTS.md found (all 404); PR template has no AI-disclosure
  cross-referenced PRs, comments=0"},
        {"name": "ai_policy", "grade": "pass", "evidence": "No
  CONTRIBUTING.md/AI_POLICY.md/AGENTS.md found (all 404); PR template has no AI-disclosure
  clause"},
        {"name": "spec_included", "grade": "pass", "evidence": "Body names
  `_detect_sections()` in `resume_parser.py`, gives runnable repro code with observed vs
  expected output, and lists 3 related failing tests"}
      ],
      "verdict": "accept"
    },
    {
        {"name": "spec_included", "grade": "pass", "evidence": "Body names
  `_detect_sections()` in `resume_parser.py`, gives runnable repro code with observed vs
  expected output, and lists 3 related failing tests"}
      ],
      "verdict": "accept"
    },
    {
      "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/61",
      "checks": [
        {"name": "maintainer_merging", "grade": "pass", "evidence": "Last 5
  default-branch commits (through 2026-09-16) all authored by human Aburke225"},
        {"name": "maintainer_replying", "grade": "pass", "evidence": "Collaborator
  Aburke225 commented 2026-09-16 closing resolved issues in the response sample"},
        {"name": "repo_in_use", "grade": "pass", "evidence": "Not archived; no releases
  but pushed_at 2026-09-16, within 90 days"},
        {"name": "scope_bounded", "grade": "pass", "evidence": "Title: 'Health check DB
  probe passes a raw SQL string, which fails under SQLAlchemy 2.x' — one specific fix"},
        {"name": "unclaimed", "grade": "pass", "evidence": "state=open, assignees=[], no
  cross-referenced PRs, comments=0"},
        {"name": "ai_policy", "grade": "pass", "evidence": "No
  CONTRIBUTING.md/AI_POLICY.md/AGENTS.md found (all 404); PR template has no
  AI-disclosure clause"},
        {"name": "spec_included", "grade": "pass", "evidence": "Body names
  `api/routes/health.py`, the exact SQLAlchemy ArgumentError text, and repro steps via
  GET /health"}
      ],
      "verdict": "accept"
    },
    {
      "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/45",
      "checks": [
        {"name": "maintainer_merging", "grade": "pass", "evidence": "Last 5
  default-branch commits (through 2026-09-16) all authored by human Aburke225"},
        {"name": "maintainer_replying", "grade": "pass", "evidence": "Collaborator
  Aburke225 commented 2026-09-16 closing resolved issues in the response sample"},
        {"name": "repo_in_use", "grade": "pass", "evidence": "Not archived; no releases 
  but pushed_at 2026-09-16, within 90 days"},
        {"name": "scope_bounded", "grade": "pass", "evidence": "Title: 'No property-based
  tests for the PII scrubber' — one bounded deliverable, not a question or umbrella"},
        {"name": "unclaimed", "grade": "pass", "evidence": "state=open, assignees=[], no 
  cross-referenced PRs, comments=0"},
        {"name": "ai_policy", "grade": "pass", "evidence": "No 
  CONTRIBUTING.md/AI_POLICY.md/AGENTS.md found (all 404); PR template has no 
  AI-disclosure clause"},
        {"name": "spec_included", "grade": "pass", "evidence": "Body names 
  `tests/unit/test_pii_scrubber.py` and gives an estimated effort of 4-6 hours"}
      ],
      "verdict": "accept"
    }
  ]
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

```
cd ~/Codepath/ai301/ai301-unit1-starter/eval

# Run 1: smoke run, 2/3
python3.12 run_eval.py --rubric ~/.claude/skills/issue-select/rubric.md --limit 3 --out smoke.json

# Run 2: after "Touching several files is fine", 0/1
python3.12 run_eval.py --rubric ~/.claude/skills/issue-select/rubric.md --only issue-01

# Run 3: same wording, re-run to save the evidence, 0/1
python3.12 run_eval.py --rubric ~/.claude/skills/issue-select/rubric.md --only issue-01 --out one.json

# Run 4: after the "one goal, one PR" wording, 0/1
python3.12 run_eval.py --rubric ~/.claude/skills/issue-select/rubric.md --only issue-01 --out one.json

# Run 5: after the title-only scope_bounded, 1/1
python3.12 run_eval.py --rubric ~/.claude/skills/issue-select/rubric.md --only issue-01

# Run 6: full run, 18/20, saved as eval-run.txt
python3.12 run_eval.py --rubric ~/.claude/skills/issue-select/rubric.md --out results.json --save-run eval-run.txt
```

**Issue analysis**

issue-01:
```
{
  "rubric": "/Users/malihya/.claude/skills/issue-select/rubric.md",
  "model": "sonnet",
  "agreement": [
    1,
    1
  ],
  "results": [
    {
      "id": "issue-01",
      "verdict": "accept",
      "failed_checks": [
        "maintainer_replying"
      ],
      "checks": [
        {
          "name": "maintainer_merging",
          "grade": "pass",
          "evidence": "Last 5 default-branch commits all dated 2026-08-04 (1 day before capture), authored by named humans codewithdaniel1 and danyeaw"
        },
        {
          "name": "maintainer_replying",
          "grade": "fail",
          "evidence": "Only #16275 of 5 sampled issues got a maintainer reply, and it took 32.9 days; #16493, #16231, #16023, #16026 got none"
        },
        {
          "name": "repo_in_use",
          "grade": "pass",
          "evidence": "Not archived; latest release 26.7.0 on 2026-07-31; last push 2026-08-04"
        },
        {
          "name": "scope_bounded",
          "grade": "pass",
          "evidence": "Title: 'Add permanent docs for installing PyPI packages with conda install' \u2014 single add-request, not a question"
        },
        {
          "name": "unclaimed",
          "grade": "pass",
          "evidence": "Issue state open, assignees: none, linked PRs: none, 0 comments"
        },
        {
          "name": "ai_policy",
          "grade": "pass",
          "evidence": "CONTRIBUTING.md: 'generative AI tools welcome; you are responsible for all contributions and must review and understand AI-generated content'"
        },
        {
          "name": "spec_included",
          "grade": "pass",
          "evidence": "Body lists exact files to add/update (new task page, manage-pkgs.rst, pip-interoperability.rst, new-features.md, troubleshooting.rst) with detailed content requirements for each"
        }
      ],
      "error": null
    }
  ]
}
```

**Check rationale**
Quoted from `rubric.md` as currently written:

`| maintainer_merging | Last 5 default-branch commits and their authors (Repo facts) | At least one of the last 5 commits is from the last 60 days and was made by a person. A bot commit only counts if it merged a person's PR. | required |`

I wrote it this way because a repo with recent code changes but no real person behind them can leave a pull request unreviewed. Recent commits show that someone is still merging work, and I only count bots when they merged a person's PR, because a bot on its own doesn't show a maintainer is around.

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
3. The anticipated difficulty in claiming it.]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
