# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**
malhiya

---

## Posted upstream

**Claim comment**
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/54#issuecomment-5873103099

Hi, I'll claim #54. _detect_sections() in resume_parser.py anchors its section-header patterns the start of a line, so the PDF-extracted text with leading indentation matches nothing and detected_sections comes back empty.

Next steps: I'll reproduce it two ways: the ResumeParser().parse(...) snippet from the issue, and the three failing tests it names (test_parse_single_column_resume_text, test_parse_resume_no_work_experience, test_detect_sections). I'll post a repro report with my environment and what I see.

[Link to the comment where you claimed the issue. Use the comment's own permalink, not the
issue page on its own. **Then paste the text of that comment underneath the link** — the
pasted text is what this field is graded on, so copy across what you actually posted.]

**Reproduction comment**
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/54#issuecomment-5893172065
Reproduced: detected_sections comes back empty for indented section headers, as the issue describes.

Environment: pathreview at commit 2f4e82f (fork of main), Python 3.11.15 in a fresh venv, pypdf 6.19.0, pytest 9.1.1, macOS 14.2.1 (x86_64), git 2.38.1 (docs list 2.39 as the minimum; git was only used to clone).

Setup: make setup failed for me as written: plain python3 here is 3.8, so it built a 3.8 venv and pip install -e ".[dev]" stopped with project.license invalid. With 3.11 the dev extras still failed, because libcst had no prebuilt wheel for macOS 14 on Intel and needed a Rust compiler. So I ran only:

python3.11 -m venv .venv
source .venv/bin/activate
pip install -e .
pip install pytest
I skipped migrations, seeding and the frontend install. The snippet and the unit tests ran without them.

Steps 1: the issue's snippet (saved as repro.py, run with python repro.py):

from ingestion.parsers.resume_parser import ResumeParser
r = ResumeParser()
res = r.parse('\n    John Smith\n    john@example.com\n\n    Education:\n    - B.S. Computer Science\n\n    Skills: Python\n')
print(res.metadata['detected_sections'])
Output:

[]
Expected: Education, Skills. Actual: [].

Steps 2: the tests: python -m pytest tests/unit/test_resume_parser.py -v

5 passed, 5 xfailed
All five are marked xfail(strict=True, reason="issue #54: ..."), so a normal run reports "xfailed", not "failed". Running python -m pytest tests/unit/test_resume_parser.py -v --runxfail shows the real failures:

FAILED test_parse_single_column_resume_text - assert (False or False)
FAILED test_parse_resume_no_work_experience - assert False
FAILED test_detect_sections - assert 0 > 0
FAILED test_parse_markdown_resume
FAILED test_strip_markdown_syntax
5 failed, 5 passed
The three tests the issue names fail on empty detected_sections. test_detect_sections indents Experience:, Education: and Skills: and gets []. The last two also carry the #54 marker but fail on markdown # stripping. I haven't confirmed they share the cause.

[Link to the comment where you posted your reproduction. It must record the environment
(OS, relevant versions, code state), steps a stranger could follow, and what you observed.
**Then paste the text of that comment underneath the link** — the pasted text is what this
field is graded on, so copy across what you actually posted.]

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

[Quote one check from the `rubric.md` you uploaded to `tools/repro-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
