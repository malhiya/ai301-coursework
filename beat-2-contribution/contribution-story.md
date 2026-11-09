# Contribution: Implement Jest Tests for Image color picker

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Malhiya Arnib
**GitHub Username:** malhiya
**Issue:** (https://github.com/Bashamega/WebDevTools/issues/392)
**Pull Request:** (https://github.com/Bashamega/WebDevTools/pull/696#issue-6247180333)

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Issue scout with my own search queries and a rubric fix after the first scan**

I built an issue scout that runs four GitHub search queries I wrote, ranks the results for free, and grades the top five with my rubric. The first scan accepted all five, but one was a real misread: Amadeus #263 passed `unclaimed` even though the reporter said they had a working patch and would send the PR on request. I changed `unclaimed` to read the issue body and fail on that kind of offer, and a re-grade showed Amadeus failing while gaia #3450 and VelaTrace #61 still passed. I also added a created-date cutoff to my queries, but I did not re-scan to check it.

**Unit 6: A voice guard that checks my posts, and a memory file for the repo**

I built a voice guard: an Upstream section in my voice guide with five rules for claims, questions and pings, and a hook that checks every comment I post through Claude Code against it. It broke on my Mac at first, because the guard's script uses a type hint that Python 3.8 can't read and my plain python3 is 3.8, so I pointed the hook at python3.12 and the wiring test then blocked as expected. My claim also had to say when I'd report back, which my "no promised timelines" rule forbade, so I changed it to allow a date for my repro report but never for a fix. I also wrote a 32-line CLAUDE.local.md for the repo, and when I asked a fresh Claude Code session how to run the tests, it gave my Node 24 command and warned against npm run format without exploring the repo.

**Unit 7:Installed the ship-gate and wrote a ship manifest for WebDevTools, and opened PR #696 after the gate passed**

On my branch the ship-gate passed on the first run: all three manifest checks (tests, coverage, format) and all six pr-precheck checks. It then let the PR through without running again. Two things tripped me up. The format check failed before I changed any code, because Prettier checks my local working files even though git ignores them. Later, Claude Code tried to add a footer to my PR description, which would have voided the pass, so I rejected that edit. I formatted my local files and kept the description as I wrote it. Since it passed the first time, I never saw it reject anything.

**Unit 8: Installed the PR monitor, wrote a playbook from five merged PRs, and ran it after my PR merged.**

I wrote my playbook from five recent merged PRs on the repo, which usually merge within a day, so I set my nudge at 4 quiet days. I only ran the monitor after Bashamega had already approved and merged the PR, because I had handled the review round by hand, so none of my nudge or walk-away rules came into play. It drafted a thank-you plus a note about a bug in page.jsx that it said CodeRabbit had found; I could not confirm that on the thread, so I left it out and posted a short thank-you in my own words. I did not change the playbook, so I can't say yet whether 4 days is the right threshold.

---

## Why I Chose This Issue

I picked #392, "Implement Jest Tests for Image color picker", from the Issue Selection site after my scout scan and a detour: I first claimed open-kgo #160 from my own search, but staff said it wasn't on the site and was poorly specified, so I released it and moved on. My scout graded #392 accept with a "straightforward" difficulty note twice: one component, no assignee or linked PR, an owner who answers claims ("Feel free to work on it" on a sibling issue), and an existing test, colorPicker.test.js, to copy. It fits my profile because it's JavaScript and React and needs no Docker, paid accounts or API keys, and I installed it and ran the existing suite on Node 24 before claiming. I hope to learn how to test a React component with Jest and Testing Library, including mocking a canvas and a file upload. My scout got better after my edits: once unclaimed read the issue body, it rejected an issue where the reporter had a patch ready, and the new difficulty note told me how hard each pick looked. It still isn't perfect, because it accepted #160 even though staff found it a poor fit. I'll check whether "straightforward" was right once I've written the tests. 

Claim comment: [link] (posted Oct 31, 2026). The owner replied under it: "Feel free to open a pr".

**Toolkit**

- Tool: issue-scout (your scout: your search strategy, your rubric),
I used it to scan GitHub with four queries I wrote, then to grade individual issues directly.

- What it produced: My scan surfaced five accepted issues. When I graded #392 directly, it was accepted twice with a "straightforward" difficulty note: one component, no assignee or linked PR, an owner who answers claims, and a similar test to copy. I also graded open-kgo #160 (accept), MaterialX #2813 (reject, open linked PR) and pyhf #1250 (reject, old release).

- Difficulties: it passed #263 although the reporter had offered a patch, passed #2813 once despite a linked PR, accepted #160 though staff found it a poor fit, and its two runs on #392 disagreed on one preferred check. All five graded issues in my scan had zero comments, so my fewest-comments rule tied.

- What changed: I made unclaimed read the issue body, replaced my title-only scope check with scope-feasible and added a difficulty note, and added a created-date cutoff to my queries (not re-scanned). I also changed repo_in_use so a recent push is enough.

---

## Understanding the Issue

**Problem Description**

The Image Color Picker page lets you upload an image, click a pixel, and see that pixel's color as hex and RGB, with buttons to copy each one. It has no Jest tests, so nothing would catch it if upload, picking, or copying broke. Issue #392 asks for tests.

**Expected Behavior**

A test file sits next to the component, the way colorPicker has one. It covers the page rendering, the image upload, picking a color, and the two copy buttons. It passes under npm test, and the component shows up in the coverage report.

**Current Behavior**

On main at 59d2d54, the component's folder holds only page.jsx. No test file mentions it, and npm test passes 8 suites and 31 tests, none of them for this page. The coverage table has no row for it. It is a testing gap, not a runtime bug.

**Affected Components**

- src/app/customizer/image-color-picker/page.jsx: the component to test. I won't change it.
- src/app/customizer/image-color-picker/imageColorPicker.test.js: the new file.
- src/app/customizer/colorPicker/colorPicker.test.js: the sibling test I'm following for the clipboard and matchMedia mocks.
- README.md: a short note on running the tests, which the issue asks for.

**Toolkit**

- Tool: CLAUDE.local.md, my repo memory file for WebDevTools
- What it produced: a 32-line file with the repo's conventions, notes on where the image color picker lives and where its sibling tests are, and the exact build and test commands.
- Difficulties: the first test command I wrote ran on my default Node 22.19.0 and failed 2 of 8 suites on @faker-js/faker. Later, format:check failed on CLAUDE.local.md itself, because Prettier checks local files that git ignores.
- What changed: I put the Node 24 wrapper (npx -y -p node@24 -c 'npm test') in the commands section, so every later run used it. I ran Prettier on the file, and I now format each local working file before running checks.

---

## Reproduction Process

**Environment Setup**

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

macOS 14.2.1 (x86_64). The repo is Bashamega/WebDevTools at commit 59d2d54 (2026-09-14), package version 2.1.1, cloned from my fork, which matches upstream main. Node v24.22.2 (run through `npx -y -p node@24`; my default is v22.19.0), npm 10.9.3, Jest 30.5.1. I installed with `npm ci`. One challenge: on Node 22.19.0 two unrelated suites (CardForm and JsonGenerator) fail because Jest can't load the ES module @faker-js/faker, and the repo's pre-commit hook runs the tests too. I fixed it by running tests and commits under Node 24 with npx instead of changing my system Node, which matches CI (it uses the latest Node). npm ci also printed peer-dependency warnings and "46 vulnerabilities"; I did not run npm audit fix, because it would rewrite package files outside this issue.

**Steps to Reproduce**

1. On main, run `git rev-parse --short HEAD`: it prints 59d2d54.
2. Run `npm ci`.
3. Run `ls src/app/customizer/image-color-picker`.
4. Run `grep -rln "image-color-picker" src __tests__ --include="*.test.*"; echo "grep exit: $?"`.
5. Run `npx -y -p node@24 -c 'npm test'`, then `npx -y -p node@24 -c 'npm run test:coverage'`.
6. Observed result: the folder holds only page.jsx, no test file mentions the component, all 8 suites (31 tests) pass and none is for it, and the coverage table has no row for it.

**Reproduction Evidence**

- **Commit showing reproduction:** none (the gap is the absence of a test file, so there is nothing to commit; the folder at that commit is https://github.com/Bashamega/WebDevTools/tree/59d2d54/src/app/customizer/image-color-picker)
- **Screenshots/logs:** `ls` prints `page.jsx` only. The grep prints no files and `grep exit: 1`. `Test Suites: 8 passed, 8 total`, `Tests: 31 passed, 31 total`. Coverage has a row for `app/customizer/colorPicker` (95.45% statements) and none for `image-color-picker`.
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing] reproduced. This is a missing-tests issue and not a runtime bug, so reproducing it meant confirming the gap, and the gap is there. The sibling Color Picker already has a test I can copy. I expect the canvas and file upload to need mocks in jsdom, but I haven't written any tests yet, so that's a guess.


**Toolkit**

* Tool: repro-check (my rubric, my evidence guide, and a real-repo scope), used on my claim and then on my claim and repro report together.
* What it produced: accept. env-recorded, behavior-matches, honest-outcome, conventions-respected and steps-complete passed; evidence-traceable (preferred) failed because my test and coverage output are excerpts and not a full log.
* Difficulties: it said the repo has no CONTRIBUTING.md (a 404) because the file is named contributing.md in lowercase. The verdict held, but that evidence line was wrong.
* What changed: nothing in the rubric yet. I'd make the evidence guide look for the contributing file under any capitalization.

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

Issue #392 asks for Jest tests for the Image Color Picker. The component is src/app/customizer/image-color-picker/page.jsx. At commit 59d2d54 its folder holds only page.jsx, no test file mentions it, and it has no row in the coverage report. The sibling colorPicker has a test file and 95.45% statement coverage.

The behavior that needs tests is all in page.jsx:
- handleImageUpload reads the chosen file with FileReader and sets the image, which makes the canvas appear.
- handleCanvasClick reads one pixel with getImageData and sets the color to rgb(r, g, b).
- rgbToHex builds the hex text shown on the page.
- handleHex and handleRGB copy to the clipboard and show a toast.

jsdom has no canvas, so the tests have to mock getContext and getBoundingClientRect. Clipboard and matchMedia get the same mocks that colorPicker.test.js uses.

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

Add one test file, src/app/customizer/image-color-picker/imageColorPicker.test.js, covering render, file upload, canvas click and the two copy buttons. Add a short "Running the tests" note to the README, because the issue asks for it.

I will not test the dark-mode toggle (isDarkMode and toggleTheme), which could count as state. I will not change page.jsx. That includes rgbToHex, which returns "# ff0000" with a space. The tests will not assert the hex string, and I will mention it in the PR as a separate finding. I will not touch other tests, the Jest config, or dependencies.


**Implementation Plan**

1. Make the branch test/392-image-color-picker.
2. Create imageColorPicker.test.js with the mocks for canvas getContext, getBoundingClientRect, clipboard and matchMedia.
3. Add the render tests: the upload prompt, the Hex and RGB labels, no canvas before an upload.
4. Add the upload tests, using waitFor because FileReader is async: the input accepts images and the canvas appears after a file is chosen.
5. Add the canvas-click test with mocked pixel data [255, 0, 0, 255]: the page shows rgb(255, 0, 0).
6. Add the copy-button tests: the RGB button calls the clipboard with the rgb string and shows its toast, and the Hex button shows its toast.
7. Check the tests can fail: temporarily change a toast message in page.jsx, confirm a test fails, then restore the file with git checkout. This is not committed.
8. Run npm test and npm run test:coverage under Node 24, and confirm an image-color-picker row appears.
9. Run npx prettier --write on the new file, and add the README note.
10. Commit with a message that says what it does.

**Deviations**

Added a dark-mode toggle test, which the plan said I would not do. The issue lists state management under its unit tests, and plan-check had noted that the toggle was not covered. I removed the "I won't test the dark-mode toggle" sentence from Proposed Solution and from plan.md. Nothing else in the plan changed.

**Nov 7**

The maintainer asked me to apply CodeRabbit's review comments, so I changed page.jsx after all. I removed the space in rgbToHex, because "# ff0000" is not a valid hex color and is what the Hex button copied. I also tightened two tests and added one. This replaces my earlier plan to leave rgbToHex alone.

**Toolkit**

- Tool: plan-check
- What it produced: an accept with 7 of 7 checks passing. It checked my plan against the live thread and the repo at 59d2d54, including that rgbToHex really returns a hex string with a space. One non-blocking note: the dark-mode toggle isn't covered by my planned tests.
- Difficulties: it accepted on the first run, so it didn't catch a flaw in my plan. I can't say how it would handle a weak plan.
- What changed: I added one sentence to the plan and to Proposed Solution saying I won't test the dark-mode toggle, so a reviewer who asks about state already has an answer.


---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

I re-ran my reproduction steps on main and on my branch, and ran the three checks from my ship manifest on both (full output in test_evidence.md, Node 24).

Before (main at 59d2d54): the folder lists only page.jsx. npm test passes 8 suites and 31 tests, none for this page. The coverage table has no row for image-color-picker.

After (branch at 7e3a1e9): the folder also has imageColorPicker.test.js. npm test passes 9 suites and 40 tests. The coverage table has a row for image-color-picker: 80.3% statements, 86.66% branches, 66.66% functions, 81.25% lines. npm run test:coverage and npm run format:check also exit 0.

One step does not change: the grep for the text "image-color-picker" in test files still exits 1, because the new test imports ./page, like colorPicker.test.js. The folder listing and coverage row are the evidence.

To show the tests can fail, I temporarily changed page.jsx and ran the new tests: the toast text and the accept attribute broke 2 tests, and disabling the dark-mode toggle broke 1. I restored the file with git checkout each time.

Not covered: the image onload callbacks, because jsdom does not load images. The tests check the hex digits but not the hex string, because the page shows "# ff0000" with a space. I left that bug for a separate issue.

**Toolkit**

- Tool: my ship manifest (ship-manifest.md)
- What it produced: the three checks to run before and after my change (unit tests, coverage, format check), each written the way it runs in a fresh terminal. I ran them on main and on my branch, with a small script to repeat the same steps on both.
- Difficulties: the format check exited 1 on my first run, before I had changed any code. Prettier checks my local files (CLAUDE.local.md and ship-manifest.md), which git ignores.
- What changed: I ran Prettier on those two files, and now do the same for each working file I make (plan.md, plan-comment.md, test_evidence.md).

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]


**Nov 4**

plan-check accepted my plan on the first run. It noted that the dark-mode toggle was not covered, so I checked the issue again.

**Nov 5**

Made the branch test/392-image-color-picker. Wrote 8 tests, and all passed on the first run. I broke page.jsx on purpose to check that the tests fail, and they did.

**Nov 5**

I had written the two copy-button tests as separate near-copies. I merged them into one test.each, the way colorPicker.test.js does it.

**Nov 5**

I pasted a script into the test file in my editor instead of running it in the terminal. I rewrote the file from the clean version and the tests passed again.

**Nov 5**

The issue lists state management, so I reversed my plan and added a dark-mode toggle test (plan.md and the plan above now say so). It fails when I disable the toggle.

**Nov 5**

Added a Running the Tests section to the README because the issue asks for docs. Prettier accepted it without changes, so I did not run --write on the README. Three commits: the tests, the toggle test, the README.

**Nov 7**

Bashamega requested changes and asked me to apply CodeRabbit's comments. First I changed the tests only, and the two hex-related tests failed against the old rgbToHex, which confirmed the space was a real bug. Then I removed the space in page.jsx and all 10 tests passed. Pushed as b27199c, updated the PR description, replied on the thread, and re-requested review.



**Toolkit**

- Tool: CLAUDE.local.md (my repo memory file)
- What it produced: the Node 24 command for every test run and commit, and the note that colorPicker.test.js is the pattern to follow, which is where I copied the clipboard and matchMedia mocks from.
- Difficulties: none during the build. All three commits passed the repo's pre-commit hook (format check and the full test suite).
- What changed: nothing was needed this week.

---

## Pull Request

**PR Link:** https://github.com/Bashamega/WebDevTools/pull/696#issue-6247180333

**PR Description:** 

Adds Jest tests for the Image Color Picker, which had none, and a short "Running the Tests" section in the README, since the issue asks for docs. The new file, imageColorPicker.test.js, follows colorPicker.test.js and has 9 tests: rendering, the image-only file input, the canvas after an upload, picking a color, the dark-mode toggle, and the RGB and Hex copy buttons. The tests mock the canvas, the clipboard and matchMedia. page.jsx is unchanged and no dependencies were added. Fixes #392. On Node 24, main had 8 suites and 31 tests with no coverage row for the page. The branch has 9 suites and 40 tests, and the page has a coverage row (80.3% statements). I broke page.jsx on purpose to check the tests fail, and they did. I did not test in a browser. The page shows the hex text as "# ff0000" with a space, which I left alone. The description also says how I used AI.

**Maintainer Feedback:**

- Nov 6: none yet. The repo's Jest and Prettier checks passed on the PR. The Vercel check was waiting for a maintainer's authorization, which is normal for a PR from a fork, and the CodeRabbit bot was still processing.

- Nov 7: Bashamega requested changes: "Apply the comments from CodeRabbit please." CodeRabbit's comments asked for the exact hex value (#ff0000, which needed a one-character fix in page.jsx), a test that the uploaded image is drawn, and a test that asserts the sampled pixel coordinates.
  
- Nov 7: I applied all three in b27199c, updated the PR description, replied on the thread, and re-requested review.
- 
- Nov 7: Bashamega approved and merged the PR, and #392 closed automatically. I thanked him on the thread.

**Status:** Merged

**Toolkit**

- Tool: ship-gate (with my ship manifest and pr-precheck)
- What it produced: PASS on its first run. My three manifest checks (tests, coverage, format) passed in 10, 7 and 3 seconds, and all six pr-precheck checks passed. When I opened the PR through Claude Code within 30 minutes, it let it through without running again.
- Difficulties: the hook test showed one stop, not two, so I ran the voice guard by hand to confirm it also works. The format check first failed on my own local files, which Prettier checks even though git ignores them. When I opened the PR, Claude Code tried to add a footer line to pr_draft.md, which would have voided the pass, so I rejected the edit.
- What changed: I formatted my local working files, and I told Claude Code not to edit the description. I did not change my rubric or manifest. Because it passed the first time, I did not see it reject anything.

---

## Learnings and Reflections

**Technical Skills Gained**

I learned to test a component that uses a canvas, FileReader and the clipboard by mocking what jsdom lacks (getContext, getBoundingClientRect, the Image class, the clipboard and matchMedia). I used test.each, waitFor and findByText, and a break-it check to prove my tests can fail. I also learned the gh and fork workflow: opening and editing a PR, posting comments and checking CI.

**Challenges Overcome**

My default Node 22.19.0 failed two unrelated suites on @faker-js/faker, so I ran everything on Node 24 and wrote that into my manifest. After Bashamega asked me to apply CodeRabbit's comments, I found a real bug (a stray space in the hex code), fixed it in page.jsx and added two tests. I recorded each plan change in my notes.

**What I'd Do Differently Next Time**

I would read the issue's whole task list before writing my plan. I added the dark-mode test late, only after plan-check noted that the issue lists state management. I would also set up the PR monitor before the review arrived, so I could use it during the review and not only after the merge.

---

## Resources Used

- [colorPicker.test.js](https://github.com/Bashamega/WebDevTools/blob/main/src/app/customizer/colorPicker/colorPicker.test.js): the sibling test I followed for the clipboard and matchMedia mocks and the test style.
- [The repo's Jest workflow](https://github.com/Bashamega/WebDevTools/blob/main/.github/workflows/jest_tests.yml): where I found the test and coverage commands for my ship manifest.
- [Jest docs, require of ESM](https://jestjs.io/docs/ecmascript-modules#require-of-esm): the link in Jest's own error message, which told me to use Node 24.9 or newer.
- [The repo's PR template](https://github.com/Bashamega/WebDevTools/blob/main/.github/PULL_REQUEST_TEMPLATE.md): what my PR description had to answer.
- [Issue #392](https://github.com/Bashamega/WebDevTools/issues/392): its task list is where I got the README note and the state-management test.
- [CodeRabbit's review on PR #696](https://github.com/Bashamega/WebDevTools/pull/696#issuecomment-6690723554): its three comments, which Bashamega asked me to apply, led to the hex fix and two stronger tests.
