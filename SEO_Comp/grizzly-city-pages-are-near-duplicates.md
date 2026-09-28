---
name: grizzly-city-pages-are-near-duplicates
description: Grizzly's 16 live service-area city pages are 98.4% token-identical (Edmonds included), 15 of 16 have placeholder title tags, and the Lynnwood H1 renders "in L, WA"
---

**Summary:** measured on the live site 2026-09-17 and re-verified independently: **13 differing
tokens out of 833 — 98.4% identical** — for Lynnwood, Bothell, Renton, Auburn and Seattle against
`/service-area-kirkland-wa`; 26 for Hunts Point; **33 of 832 for Edmonds**, the page that was built
by hand from the spec and is therefore still 96% identical to a page about a different city. Fifteen of sixteen carry the title tag
"Service Area — <City>, WA" with no service words and no brand. `/service-area-lynnwood-wa` renders
its H1 as "…Services in **L**, WA" and repeats the truncation twice in the body.

**Why it matters:** the 2026-09-14 research set criticised a competitor for 48 pages that were
99.83% identical. Grizzly is now running the same play, and the broken page is the one targeting
its own home city — the highest-value term on the site.

**How to apply:** fix the Lynnwood H1 first, then the fifteen title tags, then give each retained
city page its own two or three true local sentences per the nine-string checklist in
SERVICE-AREA-PAGE-SPEC.md. Consider deleting Auburn, Renton and Hunts Point — they are outside any
plausible service radius from Lynnwood and dilute the set.


**Measurement trap worth remembering:** `diff <(tr ' ' '\n' < a) <(tr ' ' '\n' < b) | grep -c '^[<>]'`
**doubles** the real difference, because each substitution produces both a `<` and a `>` line. And
`sed 's/<[^>]*>/ /g' | wc -w` over raw HTML inflates word counts by roughly 10%, because it counts
script and style content. My first pass made both mistakes and every figure flattered the site.
Verify content-similarity numbers with a second, independent measurement before reporting them.
