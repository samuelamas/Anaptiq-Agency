# Grizzly Homepage — Augusta Lawn Care (Marysville) clone

Built 2026-09-10. Target: Webflow site `6782ba7cbc95e18c7f76bd66`, page **Home** `6a765af3b162bb3b39eec30a` (publishedPath `/`).
Page body was **empty** before this build — nothing was overwritten.

## Reference
`https://www.augustalawncareservices.com/marysville` — cloned section-for-section from screenshots supplied by Sam.

## Section map (Augusta → Grizzly)

| # | Augusta section | Grizzly equivalent |
|---|---|---|
| 1 | Yellow top bar + nav, torn bottom edge | Orange top bar + nav, torn bottom edge |
| 2 | Hero photo, eyebrow, huge headline w/ italic accent, Google badge | Same, **minus the Google badge** — replaced with two CTAs and three process chips. Do not add a rating badge back; see Open item. |
| 3 | Green estimate form, mascot left | Green estimate form, project photo left |
| 4 | Black "Why Augusta", 2 yellow cards | Black "Why Grizzly", 2 orange cards |
| 5 | Yellow comparison table, green trust strip | Orange comparison table, green trust strip |
| 6 | Black reviews carousel | Black reviews grid |
| 7 | Black about, photo left | same |
| 8 | Black services, 3 image cards | 3 cards: Irrigation / Backyard Design / Excavating |
| 9 | Yellow FAQ accordion + illustration | Orange FAQ accordion (native `<details>`) |
| 10 | Green CTA band w/ truck | Green CTA band |
| 11 | Dark footer, 3 columns + legal bar | same |
| — | (not in Augusta) | Sticky mobile call/estimate bar |

## Brand system

Taken from the site's own existing custom code, not invented.

- Display: **Anton** (added this build) — the heavy condensed face standing in for Augusta's grunge display
- Body: **Archivo** (already on the page)
- Eyebrow/label: **Barlow Semi Condensed** (already on the page)
- Accent orange `#F2600C` (already in the page's focus-ring CSS)
- Deep green `#1C3F2B`, near-black `#0E0F10`, cream `#FFF7F0`

## Verified facts used

- Phone on site: **(425) 599-6702** (GHL tracking line — the number the site and its SEO description already use)
- Service area copy order: **Kirkland, Bothell & Kenmore, WA**
- Email: grizzlylandscapeconstruction@gmail.com (Danny's, confirmed 2026-09-04)
- Legal name: Grizzly Landscape & Construction LLC

## Claims deliberately NOT made

L&I registration `GRIZZLC755LL` is **SUSPENDED since 2026-06-13** and there is **no current insurance account** on file.

- No "Licensed & Insured" badge anywhere — Augusta has one in its trust strip and its footer; both were replaced.
- No licence number. The live legacy site's `#123456` is fake and is a gross misdemeanour risk under RCW 18.27.020.
- Augusta's comparison row "Insurance — uninsured work leaves you exposed / licensed and insured" was replaced with an "After the job" row.
- No business hours (four conflicting values across platforms; none verified).
- No years-in-business, no project counts, no pricing, no guarantees, no response-time promises.
- No `aggregateRating` JSON-LD (self-serving; makes the page ineligible under Google policy).

## Open item

The three review cards in section 6 carry bracketed placeholder text, each under a visible "Placeholder" label. **They must be replaced with real review text before this page is published.**

No star rating or review count appears anywhere on the page, and that is deliberate. A 2026-09-10 verification pass could not independently confirm any Google rating: every "5.0 · 7 reviews" figure the search engines return traces back to Grizzly's own website HTML, and the one Google Maps CID that surfaced belongs to a different company in Colorado Springs. Yelp's own page title says 13 reviews while the live site claims 16. Until Danny confirms the real figures from inside the Google Business Profile, the page makes no numeric review claim at all.

## Webflow mechanics observed on this site

- WHTML `css` silently drops `font-family` (`missing_font`) — all `font-family` rules live in the page head `<style>` block, targeting classes that the WHTML inserts create as real Webflow styles.
- Author copy in `<p>`, never `<div>` — `set_text` rejects `Block` elements.
- The page head/footer arrived carrying a leftover multi-step form driver keyed to `.gzl-*` classes from a previous build. This build uses a single-step form and no element on the page carries a `gzl-` class, so the script and its CSS were dead; both were removed. (~31 orphan `gzl-*` styles still exist site-wide and should be cleaned up separately.)
- `<details>` / `<summary>` survive the WHTML import as DOM elements, which is what makes the FAQ accordion and the mobile menu work with no JavaScript at all.
- Every WHTML insert on this site returns three `dropped_style` warnings for `._w-input parent`, `._w-input-1 parent` and `._w-input-1-2 parent`. These are pre-existing site-level style collisions, fire regardless of the markup being inserted, and do not affect the inserted content.

## Assets used (all verified real Grizzly work unless noted)

| Slot | Asset | ID | Note |
|---|---|---|---|
| Header + footer logo | grizzly-logo.jpg | `6aa2d9988a7a71f1b349f27e` | Uploaded this build from `Grizzly_Website_ &_Images/Grizzly.jpg`. Bear/wordmark on solid black, so the nav bar was set to `#000000` and the logo's own field disappears into it. |
| Hero | grizzly-hero-trench.jpg | `6aa2db6b8fce9271ae23969d` | Created this build: `tempImageZ6IXJx.jpg` (4032×3024, the only full-res real photo) rotated for EXIF orientation 6 and cropped to a 2200×1236 band. Golden-hour irrigation trench along a laurel hedge. |
| Estimate band | drip-field-square.jpg | `6a2cc427d8c767bf9a8f0a30` | Waterfront planting bed mid-install, 1050². |
| About | drip-install-square.jpg | `6a2b964eacceb3126a5effdb` | Crew member in the red Grizzly shirt connecting drip line, 1050². |
| Services — Irrigation | sprinkler-adjust-square.jpg | `6a2b97ff807242bd162f1541` | Crew member adjusting a running rotor, branded shirt. 644² — the best branded-crew image on the site. |
| Services — Backyard Design | frog-garden-square.jpg | `6a2b964eb10d0d51771434f9` | Finished Japanese-influenced garden, 1050². |
| Services — Excavating | 348s-3.jpg | `67956db73d3f3dc62dec2788` | Real excavated trench with perforated drain pipe. **Only 348² — visibly soft. Weakest asset on the page.** |
| FAQ | landscape-plan-square.jpg | `6a2b964e0914b4c1fc3e9ac6` | Printed planting plan on a workbench, 1050². |
| CTA band | 348s-5.jpg | `67956db7fe820499696403d4` | The only Grizzly truck photo on the site. **348² — upscaled, soft.** |

### Assets deliberately avoided

- `before.png`, `after.png`, `before and after pic.avif`, `Drought.avif`, `Loving_life.avif` — **AI-generated** (their `originalFileName` is still `ChatGPT Image …`). Publishing them as Grizzly's own before/after would misrepresent the company's work. No before/after section was built.
- `project_1`–`project_6.webp` — named like projects, actually template stock (a birthday cake, a deer, a harbor, a wedding couple…).
- `excavating.jpg`, `wc0014.jpg` — stock heavy equipment, not Grizzly's machines. `wc0014` is visibly Florida, not the PNW.
- `gbc_logo.avif` (a competitor, GBC Landscaping) and the `UltraRenivation` / `UR - <name>` files (a different company) are sitting in this site's asset library and should be cleaned out separately.

## What still needs Danny before publish

1. **Three real review quotes** for the reviews section (currently bracketed placeholders).
2. **A white or light logo lockup.** Only a brown-on-black raster exists; the header works because the nav is pure black, but a transparent light version would be better everywhere else.
3. **Full-resolution originals** of the `348s-*` crew, truck and excavation photos — they exist only as 348×348 gallery thumbnails, which is why the excavating card and the CTA band are the softest images on the page.
4. **Real matched before/after pairs**, if a before/after section is wanted.
5. **A decision on the phone number.** The site uses (425) 599-6702; L&I, Yelp and BuildZoom all list (425) 648-9443, and this site's own `/contact`, `/about` and `/services` pages still show 648-9443. The homepage is internally consistent; the site is not.

## Form wiring

Native Webflow form, `name` = "Home - Free Estimate", `domId` = `home-free-estimate`, redirect on submit = `/thank-you`.
Fields in order: Name (text, required) · Email (email, required) · Address (text, required) · Phone (tel, required) ·
Services-Needed (text, required) · Project-Details (textarea) · SMS-Consent (checkbox). Submit reads
"SEND MY FREE ESTIMATE REQUEST".

The site-wide footer script that stamps a hidden `ad-source` field onto every form still applies, so submissions
carry the landing path. Site head still carries the Meta Pixel and the Google Ads gtag — untouched.

## Audit pass, 2026-09-10

A fresh-context agent audited the built page against this spec. Eight structural checks passed
(section order, phone consistency, all 40 links resolve, form field order and settings, mobile breakpoints on every
section, no `min-width` that would scroll at 375px, every head-CSS font class exists as a real Webflow style,
and the compliance sweep found no licence/insurance/rating/hours/pricing/guarantee claim anywhere).

Six findings were raised and all six fixed:

1. **The three review cards rendered literal gold `★★★★★` next to admittedly fake review text.** The stars were the
   one thing in the card that was *not* bracketed, so a five-star rating rendered as fact. Replaced with
   `[STAR RATING — MATCH THE REAL REVIEW]` and restyled grey so a rating can never render without a real review.
2. **The comparison table lost its column headers below 767px**, leaving three unlabelled stacked cells per row —
   the persuasive point of the section inverted on mobile. Each answer cell now names its own column via a
   `::before` label in head CSS, and the lowest-bid cell got its own background.
3. **Form was still named "Email Form"** with no redirect. Renamed, and pointed at `/thank-you`.
4. **Dead code shipped in the page head and footer** — six `.gzl-*` rules and the full multi-step form driver from a
   previous build, with zero matching elements on the page. Both removed, along with a misleading
   `body{padding-bottom:0}` rule (sticky-bar clearance actually comes from `.gzh-foot` `padding-bottom:76px`).
5. **This spec had drifted** from what was built (it still promised a hero Google badge). Corrected.
6. **The three city pages got no links from the homepage.** Added a "Service areas" block to the footer linking
   `/landscaping-kirkland-wa`, `/landscaping-bothell-wa`, `/landscaping-kenmore-wa`.

## Not done

**The page has not been published.** It exists in the Designer on the Home page only. Nothing has been pushed to
`www.grizzlylandscapeconstruction.com` or to the `grizzly-b44224.webflow.io` staging subdomain, so the rendered
result has not been visually verified at any screen width — only the element tree, styles and breakpoints were
checked, by query.
