# Grizzly Homepage — Rich Landscaping clone

Built 2026-09-10. Site `6782ba7cbc95e18c7f76bd66`, **new page** "Home — Rich Style"
`6aa321fd39185ecd2ccdaab8`, slug `/home-rich-style`. **Staged, NOT published.**
Nothing on the existing Home page `6a765af3b162bb3b39eec30a` was touched.

## Reference
`https://richlandscaping.com/` — WordPress + Elementor. Design system read out of the live
Elementor kit variables and computed styles, not eyeballed.

## Brand system (taken verbatim from Rich Landscaping)

| Token | Value | Source |
|---|---|---|
| Navy | `#0B2735` | `--e-global-color-secondary`; all headings, dark bands, footer |
| Slate | `#48586A` | `--e-global-color-primary`; body copy |
| Gold | `#AB9114` | every `.elementor-button` background + `h6` eyebrow color |
| Light grey | `#F5F7F8` | alternating section background |
| Heading face | **Plus Jakarta Sans** 700 | `--e-global-typography-primary/secondary-font-family` |
| Body face | **Inter** 400 | `--e-global-typography-text-font-family` |
| h1 | 48px / -1.5px letter-spacing / 1.3em | computed |
| h2 | 39px / -0.5px | computed |
| h6 eyebrow | 14px / 700 / 1px / uppercase / gold | computed |
| Button | gold, 30px radius, 12–13px × 24px, 14px/500 | computed |

Fonts are loaded from Google Fonts in the **page head code**, together with the
`font-family` rules — WHTML `css` silently drops `font-family` (`missing_font`).

## Section map (Rich → Grizzly)

| # | Rich Landscaping | Grizzly equivalent |
|---|---|---|
| 1 | Navy top bar (email, city, socials) + white nav | Same, socials dropped (no verified Grizzly profiles) |
| 2 | Hero photo, dark scrim, h1, gold CTA | Same + phone CTA and four service chips |
| 3 | Photo + gold "Give us a Call" card + multi-step form | Same, single-step native Webflow form |
| 4 | "Professional Landscaping … in Redmond, WA" split | Same, Kirkland |
| 5 | "Innovating Landscaping" long copy | "Practical Landscaping, Built for How the Eastside Actually Lives" |
| 6 | "Details that Protect, Enhance and Maintain" + checklist | Same |
| 7 | Service cards with gold "Learn more" | Six cards = Grizzly's six real service lines |
| 8 | "Above the Competition / Why Choose" 4 tiles | Same, claims rewritten (see below) |
| 9 | Puget Sound service-area section | Kirkland/Bothell/Kenmore + Eastside tags |
| 10 | FAQ accordion | Same, native `<details>`, no JS |
| 11 | "How it works" 3 steps | Same |
| — | Testimonials carousel ("Great 4.1, 62 reviews") | **Omitted entirely** |
| 12 | Dark footer, 4 columns + legal bar | Same |
| — | Gold CTA band | Green→navy CTA band over the truck photo |

## Verified facts used
- Phone **(425) 648-9443** everywhere (as instructed; this is the L&I / GBP / Yelp number,
  not the (425) 599-6702 GHL tracking line the other homepage uses).
- Email `admin@grizzlylandscapeconstruction.com` (from the live `/services` page).
- Six services, named as the live site names them: Fencing · Landscaping Construction ·
  Landscaping Maintenance · Irrigation and Drainage · Lighting and Hardscaping · Excavation.
- Legal name: Grizzly Landscape & Construction LLC.

## Claims deliberately NOT copied from Rich Landscaping
Rich leans on things Grizzly cannot currently say:
- **No "Since 1981" / "over 40 years"** — no verified founding date for Grizzly.
- **No review rating or count.** Rich prints "Great 4.1 · 62 reviews" and 20 named testimonials.
  No Grizzly rating has ever been independently verified, so the whole testimonial section was cut
  rather than filled with placeholders.
- **No "30 Day Warranty"** tile — no confirmed Grizzly guarantee.
- **No licensed/insured/bonded claim.** WA reg. `GRIZZLC755LL` is SUSPENDED since 2026-06-13
  (general liability lapsed). Making the claim is a gross misdemeanour risk under RCW 18.27.020.
- **No business hours** (four conflicting values across platforms).
- No pricing, no project counts, no response-time promises.

## Assets (all real Grizzly work)
| Slot | Asset | ID |
|---|---|---|
| Nav + footer logo | grizzly-logo.jpg | `6aa2d9988a7a71f1b349f27e` |
| Hero background | grizzly-hero-trench.jpg | `6aa2db6b8fce9271ae23969d` |
| Consultation band | drip-field-square.jpg | `6a2cc427d8c767bf9a8f0a30` |
| Intro split | drip-install-square.jpg | `6a2b964eacceb3126a5effdb` |
| Details split | landscape-plan-square.jpg | `6a2b964e0914b4c1fc3e9ac6` |
| Card — Landscape Construction | 348s-2.jpg (paver drive + block wall) | `67956db74a42c429001d5f76` |
| Card — Irrigation & Drainage | sprinkler-adjust-square.jpg | `6a2b97ff807242bd162f1541` |
| Card — Fencing | 348s-8.jpg (cedar fence + stairs) | `67956db7406d3f1f2ebdc9b1` |
| Card — Maintenance | 348s-7.jpg (crew pruning hedge) | `67956db78a347375dc8f8282` |
| Card — Lighting & Hardscaping | frog-garden-square.jpg | `6a2b964eb10d0d51771434f9` |
| Card — Excavation | 348s-3.jpg (trench + drain pipe) | `67956db73d3f3dc62dec2788` |
| Service area split | 348s-6.jpg (mulch bed) | `67956db73d3f3dc62dec2785` |
| CTA band | 348s-5.jpg (Grizzly truck) | `67956db7fe820499696403d4` |

Every `348s-*` file is only 348×348 and visibly soft. Each was previewed before use to confirm
its subject matches the card it sits on. AI-generated assets (`before.png`, `after.png`,
`Drought.avif`, `Loving_life.avif`) and template stock (`project_1`–`project_6.webp`) were avoided.

## Form
Native Webflow form. Name `Home Rich Style - Free Consultation`, domId
`home-rich-style-consultation`, method POST, redirect `/thank-you`.
Fields: Name · Phone · Email · Project-Address · Services-Needed · Project-Details (textarea).
All required except Project-Details. Submit reads "Request My Free Consultation".
Fields carry **visible labels, not placeholders** — see `lessons/`.

The site-wide footer script that stamps a hidden `ad-source` field onto every form still applies.


## Repair pass, 2026-09-10

Every section root came back from WHTML **with no class at all** — the builder strips classes from
the single root element and never creates their styles. The visible symptom was the nav bar
appearing underneath the hero: with `.rl-hero` gone the hero had no `position:relative`, so its
absolutely-positioned dark scrim sized itself to the viewport and painted over the header.

Fixed by creating the 13 section styles through `data_style_tool` and applying them with
`set_style` (one class per element — two names is read as a combo class and fails). Section
backgrounds, padding, the hero/CTA background images and all breakpoint overrides are verified
present. The `rl-page` wrapper class was abandoned; the page head CSS now scopes the fonts to
`body` and the tag/class list directly. See `lessons/webflow-whtml-strips-the-root-class.md`.


## Restore pass, 2026-09-11

The page was found altered after the FAQ build: the whole nav row inside `.rl-nav` was gone (its
logo link had been moved into a template `NavbarWrapper` styled `FN Navbar Box Second`), and the
`.rl-cta` and `.rl-footer` sections had been replaced by a Webflow **component instance named
"Footer"** whose props carried this build's own copy and logo asset. That is Designer editing, not
an API change — nothing in this session's tool calls can delete elements or create components.

Restored to the verified 13-section state: nav row, CTA band and footer re-inserted with their
existing classes, the template navbar and the Footer component instance removed from this page,
and all 21 anchor links re-bound with `set_link`. The **"Footer" component definition still exists
in the site's component library** — only the instance on this page was removed, so it can be
dropped back in at any time.


## Location update, 2026-09-11

Repointed from Kirkland to **Lynnwood, WA** per Sam. Twenty-three text nodes rewritten plus the
SEO title and description; "Eastside" now appears nowhere on the page (replaced by "Snohomish and
King County", "Puget Sound" or "Northwest" depending on context). The service-area section's tag
grid was replaced with the full **30-city list**, and the footer's Service Areas column now reads
Lynnwood / Edmonds / Mountlake Terrace / Bothell / Everett / Seattle.

Kirkland now appears exactly twice, both correct: as one city tag among the thirty, and inside the
FAQ service-area answer. Section headings changed: "Professional Landscaping & Landscape Design in
Lynnwood, WA", "Practical Landscaping, Built for How the Northwest Actually Lives", "Based in
Lynnwood, Serving Snohomish & King County", "Built for Northwest Conditions".

The 30 cities are Sam's own list (two typos in it corrected: Woodinville, East Renton Highlands).
The live site and its `/services`, `/about` and `/contact` pages still say Kirkland and still carry
the old (425) 599-6702 number — not touched this session.

## Open items before publish
1. Decide whether this page replaces `/` or stays a separate variant.
2. Rich's design leans on a social row in the top bar — add Grizzly's Facebook/Instagram if they exist.
3. `348s-*` originals at full resolution would visibly improve four of the six service cards.
4. A transparent light-background logo lockup (only a brown-on-black raster exists).
