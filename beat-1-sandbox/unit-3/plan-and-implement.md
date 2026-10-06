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

Same commands as my repro comment on issue #54. "Before" is commit `2f4e82f` with no changes. "After" is branch `fix/54-indented-section-headers`.

`repro.py` holds the issue's snippet:

```
from ingestion.parsers.resume_parser import ResumeParser
r = ResumeParser()
res = r.parse('\n    John Smith\n    john@example.com\n\n    Education:\n    - B.S. Computer Science\n\n    Skills: Python\n')
print(res.metadata['detected_sections'])
```

Before:

```
$ git rev-parse --short HEAD
2f4e82f
$ python --version
Python 3.11.15
$ python repro.py
[]
$ python -c "from ingestion.parsers.resume_parser import ResumeParser; print(ResumeParser().parse('John Smith\njohn@example.com\n\nEducation:\n- B.S. Computer Science\n\nSkills: Python\n').metadata['detected_sections'])"
['Education', 'Skills']
$ python -m pytest tests/unit/test_resume_parser.py -v
tests/unit/test_resume_parser.py::TestResumeParser::test_parse_single_column_resume_text XFAIL [ 10%]
tests/unit/test_resume_parser.py::TestResumeParser::test_parse_resume_no_work_experience XFAIL [ 20%]
tests/unit/test_resume_parser.py::TestResumeParser::test_detect_sections XFAIL [ 70%]
========================= 5 passed, 5 xfailed in 0.23s =========================
$ python -m pytest tests/unit/test_resume_parser.py -v --runxfail
FAILED tests/unit/test_resume_parser.py::TestResumeParser::test_parse_single_column_resume_text
FAILED tests/unit/test_resume_parser.py::TestResumeParser::test_parse_resume_no_work_experience
FAILED tests/unit/test_resume_parser.py::TestResumeParser::test_parse_markdown_resume
FAILED tests/unit/test_resume_parser.py::TestResumeParser::test_detect_sections
FAILED tests/unit/test_resume_parser.py::TestResumeParser::test_strip_markdown_syntax
========================= 5 failed, 5 passed in 0.19s =========================
```

The change:

```
$ git diff --stat
 ingestion/parsers/resume_parser.py | 8 ++++----
 tests/unit/test_resume_parser.py   | 9 ---------
 2 files changed, 4 insertions(+), 13 deletions(-)
```

After:

```
$ python repro.py
['Education', 'Skills']
$ python -c "from ingestion.parsers.resume_parser import ResumeParser; print(ResumeParser().parse('John Smith\njohn@example.com\n\nEducation:\n- B.S. Computer Science\n\nSkills: Python\n').metadata['detected_sections'])"
['Skills', 'Education']
$ python -m pytest tests/unit/test_resume_parser.py -v
tests/unit/test_resume_parser.py::TestResumeParser::test_parse_single_column_resume_text PASSED [ 10%]
tests/unit/test_resume_parser.py::TestResumeParser::test_parse_resume_no_work_experience PASSED [ 20%]
tests/unit/test_resume_parser.py::TestResumeParser::test_detect_sections PASSED [ 70%]
========================= 8 passed, 2 xfailed in 0.24s =========================
$ python -m pytest tests/unit -q
6 failed, 372 passed, 50 xfailed, 21 warnings in 19.86s
```

The indented snippet went from `[]` to `['Education', 'Skills']`. The unindented control still finds the same two sections. The order changed because the result comes from a set. The three tests the issue names now pass. The two markdown tests still show as xfailed, because I did not change `_strip_markdown`.

The 6 failures in the full run are all in `test_review_service.py`. Each says "async def functions are not natively supported", because no async pytest plugin is installed on my machine. I did not run the full suite before my change.


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
