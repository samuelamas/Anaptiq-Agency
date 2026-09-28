# Grizzly FAQ page — Cedar Rustic clone

Built 2026-09-10. Site `6782ba7cbc95e18c7f76bd66`, page **FAQ** `6aa346d9fc9f7e7a37c7b86c`,
slug `/faq`. **Staged, NOT published.**

## Reference
`https://cedarrustic.com/faq` — itself a Webflow site. Layout cloned section for section;
palette deliberately NOT cloned (see below).

## What was cloned vs. changed

| | Cedar Rustic | Grizzly |
|---|---|---|
| Hero | photo background, centred, 33px uppercase line over a 72px accent line | same, over `frog-garden-square.jpg` with an 86% white scrim |
| Accent | orange `#F26300` | gold `#AB9114` |
| Open accordion / band | cream `#EDE8DF` | light grey `#F5F7F8` |
| Heading colour | `#2D393B` | navy `#0B2735` |
| Body colour | `#1D2324` | slate `#48586A` |
| Heading face | Prompt | **Plus Jakarta Sans** |
| Body face | Open Sans | **Inter** |
| Button | square, 3px accent border, 14px/700 uppercase, 0.84px tracking | same geometry, solid gold fill |
| Accordion | JS-driven, chevron SVG | native `<details>`/`<summary>`, no JS, CSS chevron rotation |
| Sections | hero → breadcrumbs → FAQ → contact band | same, plus header and footer chrome |

Sam chose to keep Grizzly's navy/gold rather than Cedar Rustic's orange/cream so the FAQ page
sits beside the new homepage as one site.

## Content
16 questions written for Grizzly's six service lines: service area (with the 30-city tag list
Sam supplied), permits, timelines, winter work, property lines, post checking, staining cedar,
gates heaving, standing water, French drains, paver settling, irrigation repair, winterisation,
excavation, retrofit lighting, and getting started.

## Claims deliberately NOT cloned
Cedar Rustic's FAQ leans on things Grizzly cannot currently say:
- Their **"What type of warranties do you offer?"** item ("three-year warranty on workmanship")
  was dropped — no confirmed Grizzly guarantee.
- Their **"we are licensed and bonded"** line was dropped — WA reg. `GRIZZLC755LL` is SUSPENDED
  since 2026-06-13.
- No pricing, no hours, no review or rating claim, no years in business.

The permit answer is deliberately hedged ("depends on the city… confirm with your local building
department") rather than stating thresholds, because the specific Lynnwood / Edmonds / Bothell /
county numbers were not verified this session.

## Location change — needs follow-through
Sam confirmed 2026-09-10: **base is Lynnwood, WA**, service area is the 30-city list.
This page says Lynnwood throughout. **The homepage `/home-rich-style` and the live site still say
Kirkland**, and the live `/services` page still shows the old area. Those need the same change.

## Form
Native Webflow form. Name `FAQ - Still Have Questions`, domId `faq-still-have-questions`,
method POST, redirect `/thank-you`. Fields: First-Name · Last-Name · Phone · Email · Address ·
ZIP-Code · How-Did-You-Hear · Project-Details (textarea). All required except the last two.
Submit reads "Send My Question". Visible labels, not placeholders (placeholders are unwritable
via the Data API — see `lessons/webflow-input-placeholder-is-not-writable.md`).
SMS consent is static text, matching Cedar Rustic — there is no consent checkbox.

## Build note
Every WHTML fragment was wrapped in a throwaway outer `<div>` so the real section was a *child*,
because the builder strips classes from the root element. All six section roots kept their class
first time — no repair pass needed. See `lessons/webflow-whtml-strips-the-root-class.md`.

## Open items
1. Confirm the permit thresholds if you want specific heights in that answer.
2. The hero photo is a finished-garden shot; a fencing or hardscape photo may suit the FAQ better.
3. Nav links point at `/` for Home — repoint if `/home-rich-style` becomes the homepage.
