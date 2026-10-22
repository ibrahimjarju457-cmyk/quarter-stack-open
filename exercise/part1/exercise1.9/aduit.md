# Audit of ai-page.html (frozen input, committed unchanged)

Legend: **[PASTE ...]** = observation only you can make; fill it in from your own run. Source-derived proof is already written.

## Heading outline as shipped (this is proof for rows 3 and 5)

```
h1 Serrekunda Tailoring Shop
  h2 Quality You Can Trust!        <- no content under it except an <img>
  h2 About Us
    h3 Our Services                <- nested under About Us
  h2 Pricing
  h2 Opening Hours
  h2 Contact Us
```

| # | Defect | How I proved it | Kind | How I fixed it |
|---|---|---|---|---|
| 1 | No `lang` on `<html>` | Source: start tag is bare `<html>`. Validator warning text: [PASTE exact warning, expected to be about adding a lang attribute to the html start tag]. Screen reader pronunciation of the page: [PASTE which reader/voice, what it did] | 1 | `<html lang="en">`; re-run validator: [PASTE warning gone] |
| 2 | Generic `<title>` | Source: title is "Welcome to Our Tailoring Shop"; the shop name appears only in the h1. Browser tab shows: [PASTE what the tab displays] | 1 | `<title>Serrekunda Tailoring Shop – Bespoke Tailoring</title>` (confirm real shop name with owner) |
| 3 | Tagline marked as `<h2>` | Outline above: h2 "Quality You Can Trust!" is a section heading with no section under it. Headings list in screen reader / browser outline tool: [PASTE] | 1 | Changed to `<p>` |
| 4a | `alt="image"` | Source: alt text is the element's own type, says nothing about content. Screen reader read aloud: [PASTE] | 1 | Descriptive alt written once the real photo is known, or `alt=""` if decorative |
| 4b | `shop.jpg` invented | Nobody supplied a photo. DevTools Network tab / broken-image icon on load: [PASTE status for shop.jpg] | 2 | [TO ASK owner: photo, what it shows]; add `width`/`height` |
| 5 | "Our Services" is `<h3>` under About Us | Outline above: Services nested under About Us, though they are not part of it | 1 | Promoted to `<h2>` |
| 6 | Fake list (`&bull;` + `<br>`) | Source: one `<p>` with four text bullets. Screen reader should announce "list, 4 items" for a real list; for this: [PASTE what it read]. DevTools accessibility tree role: [PASTE, expect paragraph] | 1 | `<ul>` with four `<li>` |
| 7 | `<br><br>` as spacing | Source: two consecutive `<br>` between two `<p>` elements. Delete them in DevTools and observe: [PASTE what changed] | 1 | Removed; spacing handled in CSS |
| 8 | `<b>` for "Please note" | Spec distinction: `<b>` is stylistic offset, `<strong>` is strong importance. Deposit policy is important content. Caveat: many screen readers don't announce either by default, so the proof here is the accessibility tree: [PASTE] | 1 | `<strong>` |
| 9 | Founding year, "three decades", "2,000 customers", "award-winning" | Nobody supplied a founding year, a customer count, or any award. Original prompt: [PASTE prompt, show these facts are absent]. (Note: 2026 − 1985 = 41, so "over three decades" is true but vague, not false.) | 2 | Removed claims. [TO ASK owner: year founded; any real figures or awards, with proof] |
| 10 | Prices `$250.00`, `$20.00` | No prices were supplied. `$` assumes a US context; this shop is in Serrekunda. | 2 | [TO ASK owner: real prices and currency (likely GMD)] |
| 11 | "50% deposit, non-refundable" | No deposit policy was supplied; a made-up refund rule is a commitment the shop never made. | 2 | Removed pending owner's actual policy |
| 12 | Opening hours 9–5, weekends closed | No hours supplied; pattern is a generic US business week. | 2 | [TO ASK owner: real hours, including Friday and Saturday] |
| 13a | Phone `(555) 123-4567`, email `info@tailoringshop.com` | Nobody supplied contact details. 555 is a placeholder-style US number with no +220 country code. Whether the domain exists / who owns it: [PASTE lookup result; don't assume] | 2 | [TO ASK owner: real phone and email] |
| 13b | Contact details not links | Tab test: press Tab from page load. Expected: nothing on the page takes focus. Observed: [PASTE] | 1 | `<a href="tel:+220...">` and `<a href="mailto:...">` once values are real |
| 14 | No landmarks | Source: no `<header>`, `<main>`, `<footer>`, `<nav>`. Landmark list in screen reader / DevTools accessibility tree: [PASTE, expect empty] | 1 | Wrapped content in `<header>`, `<main>`, `<footer>` |

## Tally

- Kind 1 (not good enough yet): 1, 2, 3, 4a, 5, 6, 7, 8, 13b, 14
- Kind 2 (never told): 4b, 9, 10, 11, 12, 13a
- Kind 3 (barely seen this): none found. HTML is heavily covered in training data.

The Kind 1 fixes are edits. Every Kind 2 fix is a question for the owner, so the page is not finished until those answers exist.

---

# Part B: today's model vs the frozen page

## The prompt

> Make me a simple one-page website in HTML for my tailoring shop in Serrekunda, The Gambia. Include what we do, our prices, our opening hours, and how to contact us.

## The two defects nearly everyone misses (frozen page)

| Miss | Where it is in ai-page.html | Why no tool catches it |
|---|---|---|
| A fact the owner never gave, stated with confidence | "Established in 1985", "2,000 satisfied customers", "award-winning", "50% deposit... non-refundable", the shop name, the services list | The markup is valid; the validator is silent. Only someone who knows the shop can tell. |
| A detail that belongs somewhere else | `$250.00` / `$20.00` (US dollars), Mon-Fri 9-5 with weekends closed, `(555) 123-4567` (US format, no +220) | Valid HTML, readable text. Only someone who knows the place notices. |

## Q1. Defects today's model avoided (read from ai-page-today.html source)

| Defect | Evidence in the new file |
|---|---|
| 1 no lang | `<html lang="en">` |
| 2 generic title | title names the trade and place: "[Shop name] - Tailoring in Serrekunda, The Gambia" |
| 3 tagline as h2 | no tagline; the line under the h1 is a `<p>` |
| 4a, 4b image | no `<img>`, so no alt text and no invented file |
| 5 h3 under About | outline is h1 > four h2 sections, no skipped or nested levels |
| 6 fake list | services are a `<ul>` with `<li>` items |
| 7 `<br><br>` | no `<br>` anywhere |
| 8 `<b>` | no `<b>` anywhere |
| 9 invented history and claims | none present |
| 10 US dollars and made-up prices | currency stated as dalasi; amounts are `D [amount]` placeholders |
| 11 deposit policy | not present |
| 12 invented hours | all seven days listed with `[hours or closed]`; no week pattern assumed |
| 13a invented phone and email | `+220 [number]`; no email invented |
| 14 landmarks | `<header>`, `<main>`, `<footer>` present |

## Q2. Defects it repeated

None of the invented values. Three things to record honestly:

- **13b, contact not a link:** still not a link. This time there is nothing to link to, because the number is a placeholder. Tab test: [PASTE what you see].
- **Gaps announced, not filled:** the page now contains bracketed placeholders. That is a different kind of incomplete page: honest, but not publishable. Every bracket is still a question for the owner.
- **Suspected contamination:** the absence of invented facts is exactly what a model told about the audit would produce. A fresh run could invent prices or hours again. Do that run and record it here: [PASTE fresh-run result].

## Q3. Why no model improvement could prevent each repeat

Split into what a better model can and cannot do:

- **Never in the prompt, so unavailable to any model:** the shop name, services, prices, hours, phone and email. A model can only invent a plausible value (the failure) or leave a placeholder or ask (the improvement). It cannot supply the true value. This is kind 2 and will not go away.
- **Locale details (USD, 555 number, US working week):** this one is partly preventable. The prompt did say Serrekunda, The Gambia, so a better model can default to dalasi, +220 and a local week. What it still cannot know is the amounts, the digits and the hours.
- **Shop name:** the prompt gave a location, not a name. Building a name from the location ("Serrekunda Tailoring Shop") is a guess presented as a fact.

So the direction holds: structure (kind 1) improves with models, and missing facts (kind 2) need the owner. The reason I need to correct is that "wrong place" is not purely kind 2 here, because the right place was supplied.
# Part C: what the well-written prompt changed (tailoring-shop.html)
 
Evidence is read from the source of `tailoring-shop.html`. This session had already seen the audit, so a fresh run is still the stronger test.
 
| Constraint I added | Defect it removed | Kind (1/2/3) |
|---|---|---|
| "Prices should be in dalasis" | #10 US dollar prices (`$250.00`, `$20.00`); page now says "Gambian dalasi (D)" | 2 (assumed a context that is not this one) |
| "Opening hours: Monday to Saturday, 8:45 am to 4:45 pm" | #12 invented hours (Mon-Fri 9-5, weekends closed); page now carries only the supplied hours | 2 (a fact nobody gave, now given) |
| "Headings must form an outline, not be chosen for size" | #3 tagline marked as `<h2>` and #5 `<h3>` nested under About; outline is one `<h1>` and four `<h2>` | 1 |
| "Important warnings marked as important, not merely bold" | #8 `<b>` for the warning; no `<b>` in the file, and the comment points to `<strong>` | 1 |
| "State nothing about the business that it was not given" | #9 invented history, customer count and awards; #11 deposit policy; #13a made-up phone and email; shop name and services invented in the frozen page | 2 |
 
Defects that disappeared without a constraint from me (lang, title, list markup, `<br>` spacing, alt text, landmarks): avoided in this run, but in a contaminated session, so not credited to the prompt.
 
## Which defects survived a well-written prompt, and why could no wording have prevented them?
 
The shop name, the services and their price amounts, the phone number (and so the `tel:` link), and the opening hours for Sunday all survived, as bracketed placeholders or omissions. No wording could have prevented them because the prompt can forbid inventing a fact but cannot supply one, so those values exist only with the shop owner.
 