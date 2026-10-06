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
```
cd ~/Codepath/ai301/ai301-unit3-starter/eval

# Run 1: first full run, not saved, 18/20
python3 run_eval.py --rubric ~/.claude/skills/plan-check/rubric.md --evidence ~/.claude/skills/plan-check/references/evidence-guide.md

# Run 2: same files, confirming full run, saved as eval-run.txt, 18/20 (PASS)
python3 run_eval.py --rubric ~/.claude/skills/plan-check/rubric.md --evidence ~/.claude/skills/plan-check/references/evidence-guide.md --save-run eval-run.txt
```
Scores in order: 18/20, 18/20

I did not change any file between the two runs. Both missed pkg-14 and pkg-20. pkg-14 failed `executable` in run 1 and `executable, honest-unknowns` in run 2, so the grader gave different notes on identical files.


**Package analysis**

pkg-01 (httpie/cli#1838, category wrong-cause). My rubric decided reject, and the gold label is reject. The eval-run.txt row reads pkg-01 wrong-cause reject reject yes.

The plan blames the wrong code, and its own repro evidence shows it. The plan says: "The REQUEST_ITEM tokenizer in httpie/cli/requestitems.py is the problem." The repro evidence says: "the request items are never handed to HTTPie's item parser." So the tokenizer never runs. The plan also calls the Python version difference "a red herring", but repro step 3 says the same command on 3.13.5 "prints the full request, exit 0." So the version difference is real, not a red herring.

My diagnosis-matches-evidence check says: "Fail if the cause contradicts the evidence, or isn't tied to it at all." This plan contradicts its own evidence, so it fails.

eval-run.txt doesn't list which checks failed on rows that agree, so this is my own reading of the package against my rubric.


**Check rationale**
From rubric.md, as it reads now:

| diagnosis-matches-evidence | The plan's stated cause, read against what the repro evidence actually shows. | Pass if the stated cause explains the exact behavior the repro evidence shows. Fail if the cause contradicts the evidence, or isn't tied to it at all. | required |

I wrote it as a rule about the outcome, so two people reading the same plan and repro evidence get the same answer. I haven't changed it since my first draft, because that draft already cleared the bar. I considered folding it into targets-cause-not-symptom and rejected that. A plan can name the right cause and still only patch the symptom, which is a different mistake, so each gets its own check.

**Trade-offs**

All seven checks are `required`, and my verdict rule says: "Accept only if every required check passes. A required check graded `unclear` counts as `fail`." The cost is that one strict grade holds a package. In run 1, pkg-14 was rejected on `executable` alone: `pkg-14  clear-accept       accept  reject   NO     failed: executable`. The gold label is accept. In run 2 it failed `executable, honest-unknowns`.

The other miss is `pkg-20  thread-convention  reject  accept   NO     graded accept`. I did not open pkg-14 or pkg-20 to find out why, because the run still cleared the bar: `agreement: 18/20 scored items  (bar: 18/20: PASS)`. The categories line shows `thread-convention 1/2`, so the category floor held only through pkg-04. I accept that cost, because requiring all seven is what lets the rubric hold a plan that is weak in one place.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
