This fall, I had an open-source contribution merged: automated tests for the Image Color Picker in WebDevTools, a collection of web developer tools. The page lets you upload a picture, click a pixel, and copy its color code, and until now nothing tested that it worked.

The most useful part wasn't my first draft. While writing the tests, I noticed the page copied color codes with a stray space ("# ff0000"), which isn't a valid color. I decided to leave that for another day and wrote tests that avoided it. They all passed.

Then the review came back. An automated reviewer flagged exactly that stray space, and the maintainer asked me to act on its comments. My tests hadn't caught the bug because I had written them not to look at it. I fixed the one-character bug, rewrote the tests to check the exact value, and the pull request was merged.

What stays with me: a passing test only means something if it could have failed. So now I break my own code on purpose to see whether the tests notice.

Pull request: https://github.com/Bashamega/WebDevTools/pull/696
