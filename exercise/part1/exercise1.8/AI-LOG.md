# AI Log: Broken Page Debugging Exercise

This log records how I observed, located ,traced, fixed and verifed the code with the help of claude (AI)

## Exercise summary

- **Assignment:** Fix a deliberately broken HTML page. Find all errors (at least 12), fix each using the loop *observe, locate, trace, fix ONE thing, verify*, comment each fix, keep a one-line-per-bug log in `errors-found.txt`, and finish with a page that validates with zero errors.
- **Files in this folder:**
  - `fixed-page.html`:the fixed code 
  - `errors-found.txt`: the bug log, one line per bug
  - `AI-LOG.md`: this file

## Interaction log

### 1. Prompt

- **Prompt (summarised):** the user pasted the broken page together with the assignment requirements. The paste was cut off mid-sentence at "the symptom you observed and the…".
- **Interpretation by the AI:** it treated the "Requirements…" lines as instructions, not page content, and assumed the cut-off sentence meant "the symptom you observed and the cause and fix".

### 2. Observe

- The AI saved the original as `broken.html` and ran two validators on it.
- `html-validate` could not parse the page past the unclosed `<title>`, and its output was not useful.
- The AI then installed the W3C Nu validator (`vnu-jar` from npm, run with the Java already in the sandbox). It reported 2 errors: "Unclosed element title" and "End of file seen when expecting text or an end tag".

### 3. Locate, trace and fix

- The AI wrote a short Python script holding an ordered list of 15 fixes. For each one, the script:
  1. checked that the text to replace occurred exactly once,
  2. applied that single change and added a `<!-- FIX n -->` comment,
  3. re-ran the W3C validator and printed the remaining errors.
- The order was chosen by the AI, starting with the unclosed `<title>` because it hid the other errors.
- Fixing `<title>` raised the count from 2 to 18 as hidden errors surfaced. The count then fell fix by fix, reaching 0 after fix 14.

### 4. Verify and format

- The AI ran Prettier 3 on `fixed.html`, then ran the W3C validator on the result. Outcome: 0 errors, 0 warnings, and 1 info note about the trailing `/>` Prettier adds to `<meta>`.
- Prettier moved two comments: FIX 2 now sits before `<html>`, and FIX 15 after `</body>`.

### 5. Log and write-up

- The AI wrote `errors-found.txt` from the validator output captured during step 3, and this log from the conversation history.

## Results

- **15 bugs fixed:**
  - 7 unclosed tags: `title`, `h2`, `h3`, and four `li`/`p` elements
  - 3 mismatched end tags: `<h1>` used as a closer, `</em>` closing `strong`, and `</h3>` closing `h2`
  - 2 incorrect nesting: an `ol` inside an `ol`, and `strong`/`p` overlap
  - 1 case and missing-attribute fix: `<HTML>` and no `lang`
  - 1 missing `</html>`
  - Some of these count differently depending on how you group them. The log lists them individually.
- **6 of the 15 produce no validator message** because their end tags are optional in HTML (four `li`/`p` tags, the missing `</html>`, and the uppercase `<HTML>`). They were found by reading the source and fixed because the assignment counts them.

## What was and wasn't verified

**Checked by tooling:**

- The W3C Nu validator was run on the original, after every fix, and on the final formatted file.
- Prettier was applied to the final file.

**Not checked:**

- The pages were not opened in a browser, so the rendered result was not compared against the original by eye.
- The one-fix-at-a-time loop was automated with a script. A person doing the exercise by hand would observe each browser symptom themselves; the "symptoms" in the log are mostly validator messages, plus "found by reading the source" for the six that have none.
- The AI chose how to group errors into 15 lines. Your instructor may count them differently, for example treating the two unclosed-`strong`/`p` messages as one bug or several.

## Open points

- The log columns are an assumption, because the assignment text was cut off.
- The earlier `documented-page.html` project was checked only with `html-validate`. The W3C validator is now available in the sandbox, so that page could be re-checked the same way if wanted.

## Your review

*Fill this in yourself. An AI log is more useful when it records your own judgement.*

- **What I changed or rejected:**
- **What I verified myself (for example in a browser):**
- **What I learned:**