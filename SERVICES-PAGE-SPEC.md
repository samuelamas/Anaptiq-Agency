# Grizzly Services page — Rich Landscaping services hub clone

Built 2026-09-11. Site `6782ba7cbc95e18c7f76bd66`, page **Services** `6aa3aa74507154eaa3ddf700`,
slug `/services`. **Staged, NOT published.**

## Reference
`https://richlandscaping.com/services/` — same Elementor site as the homepage and the service-area
template, so palette and type carried over with nothing to convert: navy `#0B2735`, slate
`#48586A`, gold `#AB9114`, grey `#F5F7F8`; Plus Jakarta Sans + Inter.

## Section order
1. Header (shared `gf-*`).
2. Breadcrumb — `Home » Services`.
3. Hero — eyebrow, H1 "Expert Landscape Construction & Hardscaping for Homes Across Snohomish &
   King County, WA" (theirs lists cities; this names the two counties), two lead paragraphs, CTA.
4. **Service card grid** — the page's centrepiece and the part that mirrors their grey section:
   six cards, each a 300px photo + number + title + a substantial paragraph + a link through to
   that category on `/projects`.
5. Two-column copy — "Craftsmanship-Driven Builds for Everyday Enjoyment" and "Maintenance That
   Protects the Investment", their two H2s rewritten for Grizzly.
6. Consultation form band (`#consult`).
7. "Our Puget Sound Service Area" with the 30 cities by county.
8. "How It Works / Get Started Today".
9. Footer.

## Adaptation: no per-service detail pages
Their cards link out to `/services/landscape-construction/` and similar. Grizzly has no per-service
pages, so rather than leave six links pointing nowhere, each card links to the matching **filter on
the Projects page**: `/projects?cat=construction`, `?cat=irrigation`, `?cat=fencing`,
`?cat=maintenance`, `?cat=lighting`, `?cat=excavation`.

That required a change to the **Projects page footer script** — it now reads `?cat=` on load,
preselects the matching tab and scrolls the grid into view, falling back to a regex when
`URLSearchParams` is unavailable and to the normal "All" view when the parameter is missing or
unrecognised. So the card copy on Services and the gallery on Projects stay in sync through the
category slug, and the six links land on real filtered content.

If per-service pages are wanted later, these card links are the natural place to repoint.

## Style reuse
Only the `sv-*` service card styles are new. Header, breadcrumb, hero, copy blocks, form band,
service area and steps all reuse classes already created for the FAQ, Contact and service-area
pages, so the whole set stays visually identical and the stylesheet did not grow much.

## Form
Native Webflow form. Name `Services - Free Consultation`, domId `services-consultation`, method
POST, redirect `/thank-you`. Fields: First-Name · Last-Name · Phone · Email · Address · ZIP-Code ·
**Services-Needed** (relabelled "Which service are you interested in?" — the one field that differs
from the Contact/Projects forms, since the intent on this page is service-specific) ·
Project-Details.

## Claims deliberately NOT cloned
Their Google rating badge ("4.1, based on 62 reviews"), the whole testimonial block, and tenure
claims like "over four decades". No licensed/insured/bonded claim, no hours, no pricing, no
guarantee — same line held across every page in this set.

## Open items
1. The `348s-*` photos on three of the six cards are 348x348 originals and look soft at 300px tall.
2. Consider per-service detail pages if any service needs its own depth; the card links are the
   hook for that.
