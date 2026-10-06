# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

malhiya

**Plan comment**
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/54#issuecomment-5996949466

Plan for #54, based on my repro above (commit 2f4e82f).

Cause. In ingestion/parsers/resume_parser.py, _detect_sections() only matches a section name right after ^ or \n. A header with spaces before it never matches. That fits what I saw: the issue's snippet returns [], and test_detect_sections gets an empty list.

Change. Let the four patterns in _detect_sections() accept spaces or tabs before the header, then remove the three xfail markers on the tests the issue names. They are strict, so they would fail once the fix works. I'm only touching that function and the test file.

test_parse_markdown_resume and test_strip_markdown_syntax carry the same #54 marker, but they fail on markdown # stripping in _strip_markdown(). The issue doesn't name them, so I'm leaving them alone. Let me know if you want them in this change.

Test. I'll run the same steps as my repro before and after: the issue's snippet, the same snippet without indentation, and tests/unit/test_resume_parser.py. I expect 8 passed and 2 xfailed after. I'll post both outputs.

Not confirmed yet. I haven't run the no-indentation control. I haven't checked what else calls this function. I'll do both before I change any code.

---

## Your branch

**Branch**

fix/54-indented-section-headers 

**Evidence**

[Your Unit 2 reproduction steps re-run against the built change: the before, then the
after. Paste both, including the commands you ran and their output.]

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/plan-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
