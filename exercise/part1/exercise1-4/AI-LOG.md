# AI Log: Wall Sheet Exercise (`instructions.html`)

**Tool:** Claude (Anthropic), chat interface
**Date:** 20 October 2026

## 1. The task I gave the AI

Create `instructions.html`: a single sheet that gets printed and stuck on a wall, followed by someone busy, tired or in a hurry, where getting it wrong costs something real. The brief required:

- Zero validator errors
- Choosing `<ul>` or `<ol>` deliberately, with a one-sentence HTML comment above each list explaining why
- An `<h1>` title, then a short paragraph on who it is for and when they need it
- `<h2>` sections: "What you need" (unordered list), "Steps" (ordered list), "If something goes wrong" (paragraph)
- At least one correct use each of `<strong>`, `<em>` and `<abbr title="...">`

## 2. What the AI produced

- **Topic:** safe use of a portable generator during a power cut. Wrong use can cause carbon monoxide poisoning, fire or electrocution.
- **`instructions.html`:** the full page, using only the structure the brief asked for.
- **`styles.css`:** added after I asked to separate HTML and CSS. It holds large black-on-white text and a print stylesheet.

## 3. How each requirement was met

| Requirement | How it was met |
|---|---|
| `<ul>` vs `<ol>` | "What you need" is a `<ul>`: items can be gathered in any order. "Steps" is an `<ol>`: starting with a load attached, or refuelling a hot engine, causes harm, so order matters. |
| Comment above each list | One sentence above each list explaining the choice. |
| `<strong>` | Three harm-causing warnings: running it indoors, plugging it into a wall socket, refuelling a hot engine. |
| `<em>` | On "after" in the refuelling step; the stress changes the meaning of the sentence. |
| `<abbr title="...">` | On every occurrence of CO, m, min and kW. |
| Page structure | `<h1>`, intro paragraph, then the three `<h2>` sections in the order required. |
| Zero validator errors | **Not yet confirmed.** See section 4. |

## 4. Verification (to complete)

- **W3C validator:** the AI did not run it. I need to check `instructions.html` at https://validator.w3.org/ and record the result: _[result]_
- **Safety content:** written from general knowledge. I need to compare the steps with my generator's manual or another trusted source: _[notes]_
- **Print check:** _[print preview or printed copy checked?]_

## 5. My own changes and reflection

_[What I edited or rejected, and what I learned about ordered vs unordered lists.]_