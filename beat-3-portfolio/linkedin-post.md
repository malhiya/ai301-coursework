This fall, I wrote automated tests for an open-source web tool, and my work was merged into the project. The tests check that the Image Color Picker page in WebDevTools can load a picture, read the color of a clicked pixel, and copy the color code.

The page had no tests, so nothing would have warned its maintainers if it broke. I wrote 10 tests, and they now exercise about 86% of the page's code.

The most useful moment came in review. The maintainer asked me to act on an automated reviewer's comments, and one pointed out that the page copied color codes with a stray space ("# ff0000"), which isn't a valid color. My first tests had worked around that instead of catching it. I fixed the bug and rewrote the tests to check exact results, and the pull request was merged.

What I took from it: a test that accepts "close enough" can pass right over a real bug, so I now check the exact value.

Pull request: https://github.com/Bashamega/WebDevTools/pull/696
