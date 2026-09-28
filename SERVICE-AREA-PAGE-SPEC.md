# Grizzly service area page — Rich Landscaping city template

Built 2026-09-11. Site `6782ba7cbc95e18c7f76bd66`, page **Service Area — Edmonds, WA**
`6aa3a79a5a7e019e2ebb9d72`, slug `/service-area-edmonds-wa`. **Staged, NOT published.**
Intended as the **template** for the remaining 29 cities.

## Reference
`https://richlandscaping.com/service-area/lynnwood-wa/` — the same Elementor site the homepage was
cloned from, so the palette and type already match: navy `#0B2735`, slate `#48586A`,
gold `#AB9114`, grey `#F5F7F8`; Plus Jakarta Sans + Inter.

## Why Edmonds and not Lynnwood
The reference URL is their Lynnwood page, but the Grizzly homepage already targets Lynnwood. Two
pages chasing "landscaping Lynnwood WA" split their own ranking signal. Sam chose Edmonds
(2026-09-11): adjacent to the Lynnwood base, dense, and it leaves the homepage its own term.

## Section order
1. Header (shared `gf-*` chrome).
2. Breadcrumb — `Home » Service Area » Edmonds, WA`, matching theirs.
3. Hero — eyebrow, H1 "Thoughtful Outdoor Upgrades for Landscaping & Hardscaping Services in
   Edmonds, WA", two lead paragraphs, gold pill CTA + phone text link.
4. Full-width photo banner.
5. Grey two-column copy — "Build Strong Foundations And Standout Features" and
   "A Cohesive Plan For Edmonds Properties" (their two H2s, rewritten for Grizzly).
6. Six service cards, one per Grizzly service line, each linking to `/projects`.
7. "Contact us for your free consultation" band — the shared 8-field form.
8. "Our Puget Sound Service Area" — their By-County layout, with all 30 cities split
   Snohomish (10) / King (20).
9. "How It Works / Get Started Today" — 3 steps, navy band.
10. Footer.

## Cloning this for another city
Nine strings carry the city name. Duplicate the page in Webflow, then swap:
1. Page title and slug (`service-area-<city>-wa`)
2. SEO title + description
3. Breadcrumb last crumb
4. H1 ("... Services in <City>, WA")
5. Hero paragraph 1 (the local geography sentence — **rewrite, do not just swap the name**)
6. H2 "A Cohesive Plan For <City> Properties" and its second paragraph
7. Service card 2's second sentence (the local drainage line)
8. "What We Do In <City>" eyebrow
9. Consultation band paragraph, the "Serving" detail row, the "Beyond <City>" eyebrow, the service
   area lead sentence, and step 01's copy
10. Form name → `Service Area <City> - Free Consultation`, domId → `sa-<city>-consultation`

The geography sentences are deliberately specific (Edmonds: bluff lots falling toward the Sound,
narrow side yards, mature trees, bluff setbacks). Copy-pasting those to an inland city would be
false. Each clone needs its own two or three true local sentences.

## NOT cloned from the reference
- **Their Google rating badge** ("4.1, based on 62 reviews") and the whole testimonial block — no
  Grizzly rating has been independently verified.
- **"Over four decades"** and similar tenure claims.
- No licensed/insured/bonded claim, no hours, no pricing, no guarantee.

**Bug in the reference worth knowing:** their Lynnwood page's H1 actually reads "…in Bellevue, WA",
and the Lawn Care block says "serving the Redmond, Washington community". Their city template
leaks the wrong city into at least two places. That is exactly the failure mode the checklist above
is meant to prevent when cloning.

## Form
Native Webflow form. Name `Service Area Edmonds - Free Consultation`, domId
`sa-edmonds-consultation`, method POST, redirect `/thank-you`. Fields: First-Name · Last-Name ·
Phone · Email · Address · ZIP-Code · How-Did-You-Hear · Project-Details. Submit reads
"Request My Free Consultation". Same structure as the Contact, FAQ and Projects forms; the distinct
form name is what makes submissions attributable to this city page.

## Build note
`data_whtml_builder` rejects **nested CSS selectors** — `.sa-step .sa-card-h` returned
"Nested selectors are not allowed… StyleParser drops descendant selectors" and the whole section
failed to insert. Rebuilt with flat `.sa-step-h` / `.sa-step-p` classes. See `lessons/`.
