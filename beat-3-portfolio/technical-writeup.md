# Writing Jest Tests for an Open-Source Color Picker (and the Hex Bug Code Review Caught)

## Overview
WebDevTools is an open-source web app of developer utilities, and its Image Color Picker page lets you upload an image, click a pixel, and copy that pixel's color as hex or RGB. The page had no tests, so nothing would have flagged it if upload, picking, or copying broke. For issue #392 I wrote 10 Jest and React Testing Library tests and a "Running the Tests" section for the README. During review I found that the page copied hex codes with a stray space (`# ff0000`, which is not a valid color), so I fixed that line and tightened my tests. The pull request was merged and closed the issue: https://github.com/Bashamega/WebDevTools/pull/696. 

## What happened

### The gap
I claimed #392 on October 31, and the owner replied "Feel free to open a pr". The color picker component folder held only page.jsx. `npm test` passes 8 suites and 31 tests, none of them covered this page, and the coverage table had no row for it. This was a missing tests issue, not a not a runtime bug, so reproducing it meant confirming that gap.

## What I did

jsdom has no canvas and never loads images, so I mocked what the page uses: `getContext` (with `getImageData` and `drawImage`), `getBoundingClientRect`, the `Image` class, the clipboard, and `matchMedia`. I followed the sibling `colorPicker.test.js` for the style. My default Node 22 failed two unrelated suites on an ES-module import, so I ran everything on Node 24, which also matches CI.
 
To check the tests could fail, I temporarily broke `page.jsx` and restored it with `git checkout` each time:
 
> Changed the toast text `RGB Code Copied!!` to `RGB Code Copied` and removed `accept="image/*"` from the file input. Result: 2 failed, 6 passed (8 tests at that point).
>
> Changed `setIsDarkMode(!isDarkMode)` to `setIsDarkMode(isDarkMode)`. Result: 1 failed, 8 passed (9 tests at that point).
 
The second check came from a plan change. My plan said I would not test the dark-mode toggle, but the issue lists state management among its tests, and my plan check had noted the toggle was uncovered. On Nov 5 I reversed the plan and added a test that clicks the theme button twice and checks the page background each time:
 
```js
test("should toggle dark mode when the theme button is clicked", () => {
  const { container } = render(<ColorPicker />);
  const main = container.querySelector("main");
  const toggle = screen.getByLabelText("Toggle dark mode");
 
  expect(main).toHaveClass("bg-white");
  fireEvent.click(toggle);
  expect(main).toHaveClass("bg-gray-900");
  expect(main).not.toHaveClass("bg-white");
  fireEvent.click(toggle);
  expect(main).toHaveClass("bg-white");
});
```
 
The break-it check above shows this test doing its job: when I disabled the toggle in `page.jsx`, it was the one test that failed. That version had 9 suites and 40 tests, with 80.3% statement coverage on the page.
 
### Where my first version fell short
 
The page showed the hex value as `# ff0000`, with a space. I noticed it early, but I planned to leave it for a separate issue and wrote tests that avoided asserting the exact string:
 
```js
expect(screen.getByText(/ff0000/)).toBeInTheDocument();
// ...
copied: expect.stringContaining("ff0000"),
```
 
Those tests passed straight over the bug. After I opened the PR, CodeRabbit's inline review said:
 
> The Hex test accepts `# ff0000`, which is not a valid CSS hex color. Assert `"#ff0000"` and remove the space after `#` in `rgbToHex` so the test checks the correct clipboard value.
 
The maintainer, Bashamega, then requested changes: "Apply the comments from CodeRabbit please". I changed my plan, since the PR now touched `page.jsx`. The fix was one character, and the tests now assert the exact value:
 
```diff
-    return `# ${red}${green}${blue}`;
+    return `#${red}${green}${blue}`;
```
 
```diff
-    expect(screen.getByText(/ff0000/)).toBeInTheDocument();
+    expect(screen.getByText("#ff0000")).toBeInTheDocument();
```
 
CodeRabbit's other two comments made the tests stricter as well. One asked me to simulate the image loading and check that it gets drawn.

### Proof the new tests catch it
 
On Nov 7 I changed the tests first, and the hex tests failed against the old `rgbToHex`, which confirmed the space was a real bug. I then re-ran that on Nov 14 to capture the output, putting the old `page.jsx` back under the final tests:
 
```
✕ should sample the clicked pixel and show the picked color
✕ should correctly copy with Hex Code and display toast message
Expected: "#ff0000"
Received: "# ff0000"
Tests:       2 failed, 8 passed, 10 total
```

## Limitations and what's next

**What the tests can't check**
- **Real image loading.** The test environment has no real canvas or images, so my tests use fake ones. Code that only runs when a real browser loads a picture (lines 60–66 and 171 of `page.jsx`) is never tested, and I never tried the page in an actual browser.
- **Colors the page can't read.** One line in `rgbToHex` (line 76) handles a color it can't understand, and my tests only ever give it valid colors.
**Review suggestions I didn't apply.** CodeRabbit's second review, right after my fix, left three more ideas:
- If someone picks one image and then quickly another, the first can finish loading last and show up instead. This bug was already in the page.
- Clicking the Hex button before picking any pixel copies nothing useful (`undefined`) but still shows a "copied" message.
- My fake pixel reader returns red even before anything has been drawn.
**What's next.** I would add a test for each of those three, a test for a color the page can't read, and a real-browser test for loading an image. What I'd do differently: check exact values from the first version, and report the stray space as a bug instead of writing tests that avoided it.

