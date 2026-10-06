
# Plan: issue #54, section headers with leading spaces are not detected

## Repro evidence

From my repro comment on this issue (commit `2f4e82f`, Python 3.11.15, pypdf 6.19.0, pytest 9.1.1, macOS 14.2.1 x86_64):

    $ python repro.py        # the snippet from the issue
    []

    $ python -m pytest tests/unit/test_resume_parser.py -v --runxfail
    FAILED test_parse_single_column_resume_text - assert (False or False)
    FAILED test_parse_resume_no_work_experience - assert False
    FAILED test_detect_sections - assert 0 > 0
    FAILED test_parse_markdown_resume
    FAILED test_strip_markdown_syntax
    5 failed, 5 passed

Without `--runxfail`, the same five tests show as "xfailed". Each one is marked `xfail(strict=True, reason="issue #54: ...")`.

## Diagnosis

`_detect_sections` in `ingestion/parsers/resume_parser.py` looks for a section name right at the start of a line. All four patterns start with `^` or `\n` followed directly by the name. A header with spaces before it never matches, so indented text gives `[]`.

This fits what I saw. The snippet's `Education:` and `Skills:` are indented and come back as `[]`. `test_detect_sections` indents all three headers and gets an empty list. The two tests the issue also names fail the same way.

I got this by reading the code. I have not run a control with no indentation yet.

## Scope

I will:
- Let the four patterns in `_detect_sections` accept spaces or tabs before the header.
- Remove the three `xfail` markers on the tests the issue names. They are strict, so they would fail once the fix works.

I will not touch `_strip_markdown`, PDF text extraction, the duplicate `\n` patterns, or the order of the results.

Two other tests carry the same #54 marker: `test_parse_markdown_resume` and `test_strip_markdown_syntax`. They fail on markdown `#` stripping, which is in `_strip_markdown`. The issue does not name them, so I am leaving them and their markers alone.

## Files

- `ingestion/parsers/resume_parser.py` (`_detect_sections` only)
- `tests/unit/test_resume_parser.py` (remove three `xfail` markers; add one test for unindented headers if there isn't one)

## Approach

1. Save the "before" output: the issue's snippet, the same snippet with no indentation, and the `--runxfail` test run.
2. In `_detect_sections`, add `[ \t]*` after `^` and after `\n` in the four patterns.
3. Remove the three `xfail` markers.
4. Run the same commands again and save the "after" output.
5. Run the rest of `tests/unit` as far as it runs on my machine.

## Test plan

I will run the same commands before and after the change:

- The issue's snippet. Before: `[]`. After: it includes `Education` and `Skills` (the order can change because the result comes from a set).
- The same snippet with no indentation. It should find sections before and after. This shows the old case still works.
- `python -m pytest tests/unit/test_resume_parser.py -v`. Before: 5 passed, 5 xfailed. Expected after: 8 passed, 2 xfailed. The two xfailed are the markdown tests I'm not changing.
- The rest of `tests/unit`. Expected: the same results as before the change.

## Risks and unknowns

- I have not run the no-indentation control yet. The code says it should work. The "before" run will confirm it.
- I have only seen the first failing line in each of the three tests. A later line could fail for another reason. If so, I will write it under Deviations.
- Indented markdown headers will still not be detected after this change. `_strip_markdown` leaves their `#` in place, so the pattern still won't match. That is the case the two excluded tests cover. I think this follows from the code, and the markdown test output shows `#` left in and no sections found.
- Those two tests keep a marker that says "issue #54", so a maintainer might not see #54 as fully closed. I will ask in the PR.
- I have not checked what else calls `_detect_sections` or `SECTION_HEADERS`. I will search before I edit.
- `libcst` would not install on my machine, so I installed only the main dependencies and pytest. Some other tests may not run here. I will say which ones ran.

## Deviations
I did not add the unindented-headers test that the Files part mentioned ("if there isn't one"). There wasn't one, but the three tests that now pass already cover the fix, and my posted comment expects 8 passed and 2 xfailed, which is what I got.

Everything else matched the plan. The four patterns in `_detect_sections` now accept spaces or tabs before the header, and the three `xfail` markers are removed. `_strip_markdown` and the two markdown tests are untouched. No other code calls `_detect_sections` or `SECTION_HEADERS`.

The wider unit run has 6 failures in `test_review_service.py`. They say "async def functions are not natively supported", because no async pytest plugin is installed on my machine. That file doesn't use the resume parser.
