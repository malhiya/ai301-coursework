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

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

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

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

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
