# Grizzly Contact Us page — Cedar Rustic clone

Built 2026-09-11. Site `6782ba7cbc95e18c7f76bd66`, page **Contact Us** `6aa34e46316bb32aa145320d`,
slug `/contact`. **Staged, NOT published.**

## Reference
`https://cedarrustic.com/contact` (Webflow). Layout cloned section for section; palette swapped to
Grizzly's, same as the FAQ page.

## Sections
1. **Hero** — photo background under an 86% white scrim, single centred uppercase H1 "Contact Us"
   (38px / 700 / 2.88px tracking, matching Cedar Rustic's exactly).
2. **Breadcrumbs** — "Grizzly Landscape & Construction / Contact Us".
3. **Get in touch band** (`#form`, `#F5F7F8`) — two columns. Left: H2 with the accent-coloured
   "free estimate" run-in (gold, 2.88px tracking, exactly how Cedar Rustic colours theirs), two
   paragraphs, the phone at 32px, then an Email / Based in / Service area detail block. Right: the
   8-field form.
4. **Locations split** — full-bleed two-panel: live Google Map on one side, navy panel on the other
   with "We Proudly Serve", a gold pin-marker list (Snohomish County, King County), and the
   "Not sure if we serve your city?" + underline button, pointing at `/faq` where the 30 cities are.
5. **Footer** — same as the FAQ page.

## Palette / type
Same as the homepage and FAQ page: navy `#0B2735`, slate `#48586A`, gold `#AB9114`,
light grey `#F5F7F8`. Plus Jakarta Sans headings, Inter body. Cedar Rustic's orange `#F26300`
became gold and their cream `#EDE8DF` became `#F5F7F8`.

Header, hero shell, breadcrumbs and footer **reuse the FAQ page's `gf-*` classes** — WHTML attaches
existing styles cleanly when no `css` is passed, so no duplicate styles were created.

## Map
Cedar Rustic runs a keyed Google Maps JS build with project markers. This page uses a keyless
`https://www.google.com/maps?q=Lynnwood,+WA&output=embed` iframe inside a Webflow **HtmlEmbed**
element — WHTML silently drops raw `<iframe>` tags (see `lessons/`). Framing is set by `ll=47.63,-122.25&z=9` with **no `q` parameter**, so the map shows the whole
service region with **no marker** — Everett and Langley across the top, down through Lynnwood,
Seattle, Bellevue and Renton to Tacoma, Puyallup and South Hill. Sam asked for that extent
specifically (screenshot, 2026-09-11).

Zoom 9 was derived rather than guessed: Google Maps shows `height_px x 360 x cos(lat) / (256 x 2^z)`
degrees of latitude, so a 560px panel at z=9 spans ~1.04 deg — 47.11 to 48.15 around a 47.63 centre,
which is the requested extent. Panel min-height is therefore pinned at 560px desktop / 520px tablet /
440px mobile; dropping it lower crops Tacoma and Everett off the edges.

No marker is dropped and no street address is shown, because no verified Grizzly street address
exists.

## Form
Native Webflow form. Name `Contact - Get In Touch`, domId `contact-get-in-touch`, method POST,
redirect `/thank-you`. Fields mirror Cedar Rustic's: First-Name · Last-Name · Phone · Email ·
Address · ZIP-Code · How-Did-You-Hear · Project-Details. All required except the last two.
Submit reads "Send My Request". Visible labels, not placeholders. SMS consent is static text.

## Claims deliberately NOT made
No licensed/insured/bonded claim, no warranty or guarantee, no business hours, no pricing, no
review or rating claim, no years in business — same compliance line as the homepage and FAQ.
No street address is shown, because none has been verified.

## Open items
1. A verified Lynnwood street address would let the map drop a real pin instead of a city centre.
2. Business hours could go in the detail block once Danny confirms the real ones.
3. Nav links point at `/` for Home — repoint if `/home-rich-style` becomes the homepage.
