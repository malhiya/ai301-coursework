# Writing Jest Tests for an Open-Source Color Picker (and the Hex Bug Code Review Caught)

## Overview
WebDevTools is an open-source web app of developer utilities, and its Image Color Picker page lets you upload an image, click a pixel, and copy that pixel's color as hex or RGB. The page had no tests, so nothing would have flagged it if upload, picking, or copying broke. For issue #392 I wrote 10 Jest and React Testing Library tests and a "Running the Tests" section for the README. During review I found that the page copied hex codes with a stray space (`# ff0000`, which is not a valid color), so I fixed that line and tightened my tests. The pull request was merged and closed the issue: https://github.com/Bashamega/WebDevTools/pull/696. 

## What happened

### The gap
I claimed #392 on October 31, and the owner replied "Feel free to open a pr". The color picker component folder held only page.jsx. `npm test` passes 8 suites and 31 tests, none of them covered this page, and the coverage table had no row for it. This was a missing tests issue, not a not a runtime bug, so reproducing it meant confirming that gap.



## Limitations and what's next
