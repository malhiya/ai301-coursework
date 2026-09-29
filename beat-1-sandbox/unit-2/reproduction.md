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


**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/54#issuecomment-5893172065
Reproduced: detected_sections comes back empty for indented section headers, as the issue describes.

Environment: pathreview at commit 2f4e82f (fork of main), Python 3.11.15 in a fresh venv, pypdf 6.19.0, pytest 9.1.1, macOS 14.2.1 (x86_64), git 2.38.1 (docs list 2.39 as the minimum; git was only used to clone).

Setup: make setup failed for me as written: plain python3 here is 3.8, so it built a 3.8 venv and pip install -e ".[dev]" stopped with project.license invalid. With 3.11 the dev extras still failed, because libcst had no prebuilt wheel for macOS 14 on Intel and needed a Rust compiler. So I ran only:

```
python3.11 -m venv .venv
source .venv/bin/activate
pip install -e .
pip install pytest
```
I skipped migrations, seeding and the frontend install. The snippet and the unit tests ran without them.

Steps 1: the issue's snippet (saved as repro.py, run with python repro.py):

```
from ingestion.parsers.resume_parser import ResumeParser
r = ResumeParser()
res = r.parse('\n    John Smith\n    john@example.com\n\n    Education:\n    - B.S. Computer Science\n\n    Skills: Python\n')
print(res.metadata['detected_sections'])
Output:

[]
Expected: Education, Skills. Actual: [].
```
Steps 2: the tests: python -m pytest tests/unit/test_resume_parser.py -v
```
5 passed, 5 xfailed
All five are marked xfail(strict=True, reason="issue #54: ..."), so a normal run reports "xfailed", not "failed". Running python -m pytest tests/unit/test_resume_parser.py -v --runxfail shows the real failures:

FAILED test_parse_single_column_resume_text - assert (False or False)
FAILED test_parse_resume_no_work_experience - assert False
FAILED test_detect_sections - assert 0 > 0
FAILED test_parse_markdown_resume
FAILED test_strip_markdown_syntax
5 failed, 5 passed
The three tests the issue names fail on empty detected_sections. test_detect_sections indents Experience:, Education: and Skills: and gets []. The last two also carry the #54 marker but fail on markdown # stripping. I haven't confirmed they share the cause.
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

    cd ~/Codepath/ai301/ai301-unit2-starter/eval

    # Run 1: smoke test, setup check
    python3 run_eval.py --rubric ~/.claude/skills/repro-check/rubric.md \
        --evidence ~/.claude/skills/repro-check/references/evidence-guide.md \
        --limit 3
    # 3/3

    # Run 2: full run, before any rubric changes
    python3 run_eval.py --rubric ~/.claude/skills/repro-check/rubric.md \
        --evidence ~/.claude/skills/repro-check/references/evidence-guide.md
    # 16/20

    # Run 3: diagnostic on the 4 disagreements, no changes yet
    python3 run_eval.py --rubric ~/.claude/skills/repro-check/rubric.md \
        --evidence ~/.claude/skills/repro-check/references/evidence-guide.md \
        --only pkg-01,pkg-05,pkg-10,pkg-12 --out results.json
    # 1/4

    # Run 4: after tightening steps-complete and behavior-matches (v1), with 2 canaries
    python3 run_eval.py --rubric ~/.claude/skills/repro-check/rubric.md \
        --evidence ~/.claude/skills/repro-check/references/evidence-guide.md \
        --only pkg-01,pkg-05,pkg-10,pkg-12,pkg-02,pkg-06 --out results.json
    # 5/6

    # Run 5: after separating "exact input" from "exact environment" in behavior-matches
    python3 run_eval.py --rubric ~/.claude/skills/repro-check/rubric.md \
        --evidence ~/.claude/skills/repro-check/references/evidence-guide.md \
        --only pkg-10,pkg-02,pkg-06,pkg-16 --out results.json
    # 4/4

    # Run 6: full confirming run, saved as eval-run.txt
    python3 run_eval.py --rubric ~/.claude/skills/repro-check/rubric.md \
        --evidence ~/.claude/skills/repro-check/references/evidence-guide.md \
        --save-run eval-run.txt
    # 18/20, PASS


**Package analysis**

pkg-19 (vuejs/core#15205): my rubric graded this **accept**; the gold label is **reject**.

All five required checks passed. `env-recorded`, `behavior-matches`, `honest-outcome`, and `steps-complete` all had real evidence to point to — the report reproduced the issue's exact CSS leak with a named version and OS. `conventions-respected` also passed, with evidence "no stated AI policy" and "no rule against assignment requests; evidence guide treats silence as a pass." That's accurate: vuejs/core's CONTRIBUTING.md states nothing about claim format.

But the claim comment reads: "Hello sir! Great project, I love Vue and use it every day... Kindly assign it to me, I will fix it within 2 days guaranteed... keep this issue reserved for me." That's generic praise that could be pasted onto any issue, and it promises a guaranteed fix and a date, which the course's own lecture and my voice guide both treat as the wrong way to claim. My rubric can't see that, because `conventions-respected` only checks the comment against the repo's *stated* rules, and this repo states none that a boilerplate, over-promising claim would break.

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/repro-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]


Quoted from rubric.md as currently written:

| behavior-matches | The artifacts in the repro report (output, error text, logs, screenshots), read against the issue's description of the bug. | Pass if the artifact demonstrates the specific behavior the issue describes. Also pass if the report is an honest cannot-reproduce: the artifact must show a genuine, complete attempt using the issue's exact reported input/steps — a differing environment is expected and does not disqualify a cannot-reproduce, as long as the report states what differed. Fail if the artifact shows a different or only adjacent problem, the attempt skips or substitutes part of what the issue asked to be run, or a cannot-reproduce doesn't say what differed. | required |

My first version of behavior-matches had no room for an honest cannot-reproduce, so it rejected pkg-10 even though the gold label said accept — the report clearly documented a different OS and shell, but a cannot-reproduce can never match the issue's behavior. I added a cannot-reproduce branch, but its wording still failed pkg-10: it required the "exact scenario," which the grader read as the exact environment too, not just the same input. I fixed it by separating the two: same input required, environment allowed to differ;since a differing environment is what makes something a cannot-reproduce.

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]


conventions-respected only checks the comment against the repo's stated rules, not whether a claim is specific or promises a fix instead of investigation. I tried adding that, and it fixed pkg-19, but it also flipped pkg-20 — my one disclosure package — from a correct reject to an incorrect accept. I reverted the change and reran both packages: pkg-20 still swung between accept and reject on the same wording, so this looks like grading variance, not something my edit caused. I kept the original wording anyway. pkg-19 will keep grading accept, but I'd rather protect the disclosure floor than catch one bad claim comment.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
