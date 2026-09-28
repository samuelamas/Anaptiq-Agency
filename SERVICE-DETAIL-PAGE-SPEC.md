# Service detail pages (Rich Landscaping service template)

Two built so far; the pattern below is the template for the rest.

| Page | ID | Slug | Sub-services |
|---|---|---|---|
| Landscape Maintenance | `6aa3ae370be312c35684203e` | `/landscape-maintenance` | 6 |
| Landscape Construction | `6aa49df69c5e3632faf308ca` | `/landscape-construction` | 8 |
| Irrigation & Drainage | `6aa49fe436ed2ed5a91df40b` | `/irrigation-drainage` | 8 |

---

## Landscape Maintenance

Built 2026-09-11. Site `6782ba7cbc95e18c7f76bd66`, page **Landscape Maintenance**
`6aa3ae370be312c35684203e`, slug `/landscape-maintenance`. **Staged, NOT published.**

## Reference
`https://richlandscaping.com/services/maintenance/` — same Elementor site as the homepage, services
hub and service-area template, so palette and type carried across unchanged.

## Section order
1. **Header component** (shared).
2. Breadcrumb — `Home » Services » Landscape Maintenance`, with Services linked. Matches theirs.
3. Hero — eyebrow, H1, two lead paragraphs, CTA.
4. Photo banner — the hedge-pruning shot, the one genuinely-maintenance photo in the library.
5. **Sub-service cards** — the part that makes this a service *detail* page. Theirs lists seven
   (Plant Healthcare, Irrigation Maintenance, Bed Maintenance, Tree & Shrub Care, Garden Care,
   Annual Flowers, Mowing); this lists Grizzly's six.
6. Two-column copy — scheduling approach, and maintaining landscapes Grizzly did not build.
7. Consultation form band (`#consult`).
8. "Our Puget Sound Service Area" with the 30 cities by county.
9. "How It Works" — step 3 retitled **"We Keep It Right"**, since maintenance is ongoing rather
   than a project that finishes.
10. **Footer component** (shared).

## The six sub-services
Taken from how the live Grizzly site already describes this service line — "lawn care, pruning,
mulching, weed control, and seasonal cleanups" — plus irrigation maintenance, which Grizzly does and
which Rich Landscaping also files under maintenance:

Mowing & Lawn Care · Pruning & Hedge Shaping · Mulching & Bed Maintenance · Weed Control ·
Seasonal Cleanups · Irrigation Maintenance

Nothing here was invented; every item traces to a service Grizzly already advertises.

## Cards are text, not photos — deliberately
Their sub-service cards are icon boxes. Ours are numbered text cards because the asset library has
only three genuinely maintenance-related photos (hedge pruning, mulch bed, sprinkler rotor). Putting
a paver-patio or garden-design photo on a "Weed Control" card would misrepresent the work, so the
three real ones are used in the banner and elsewhere and the cards carry no imagery.

## Cross-links now wired
- The **Services page** "Landscape Maintenance" card now links to **this page** (was
  `/projects?cat=maintenance`) and its link reads "Learn more".
- The Irrigation Maintenance card links to `/projects?cat=irrigation`.

## Using this as the template for the other five
Clone the page, then swap: page title/slug, SEO, breadcrumb last crumb, hero eyebrow + H1 + both
lead paragraphs, the banner photo, all six sub-service cards, both copy-block H2s and their bodies,
the consultation paragraph, the form's "What needs maintaining?" label, the service-area lead, and
step 03. Rename the form to `<Service> - Free Consultation` and its domId to `<service>-consultation`
so submissions stay attributable. Then repoint that service's card on `/services`.

Remaining five: Landscape Construction · Irrigation & Drainage · Fencing · Lighting & Hardscaping ·
Excavation.

## Form
Native Webflow form. Name `Landscape Maintenance - Free Consultation`, domId
`maintenance-consultation`, method POST, redirect `/thank-you`. Fields as elsewhere, with the
service field relabelled "What needs maintaining?".

## Claims deliberately NOT cloned
Their "over four decades" and "over 40 years of experience" lines appear twice in the reference's
sub-service copy. Dropped, along with the rating badge and testimonials. No licensed/insured claim,
no hours, no pricing, no guarantee.

---

## Landscape Construction

Built 2026-09-12 from `https://richlandscaping.com/services/landscape-construction/`. Same section
order as the maintenance page; the reference page is structurally identical to theirs.

**Eight sub-services**, against their ten. Each traces to Grizzly's own description of the line
("hardscaping, retaining walls, patios, walkways, and outdoor living spaces") or to what the project
photos show:

Paver Patios & Walkways · Retaining Walls · Stairs & Pathways · Rockeries & Stone Features ·
Outdoor Living Spaces · Grading & Drainage · Land & Soil Preparation · Planting & Garden Design

**Dropped from their list**: Pools & Spas and Putting Greens — Grizzly advertises neither, and
there is no evidence they do that work. Decks/Fences/Arbors and Lighting are Grizzly services but
belong to their own service lines, so they are not repeated here.

Six of the eight cards deep-link into the matching `/projects` filter. Outdoor Living Spaces and
Land & Soil Preparation have no card link, because no photo in the library specifically shows them.

Copy blocks: "The Base Is Most of the Job" (with a four-point checklist) and "Planned Against
Everything Else". Step 03 stays "We Build It". Banner is the paver-driveway-and-retaining-wall shot.

Form: `Landscape Construction - Free Consultation`, domId `construction-consultation`, service field
relabelled "What do you want built?".

The Services page construction card now links here instead of `/projects?cat=construction`.

---

## Irrigation & Drainage

Built 2026-09-12. Reference: `https://richlandscaping.com/services/drainage-services/`.

**Their drainage page breaks the pattern** — it uses H3 topic blocks rather than sub-service cards,
and it splits irrigation across their maintenance and construction pages. Grizzly sells the two as
one line, so this page keeps the established card template and covers both halves.

**Eight sub-services:**

Irrigation Design & Installation · Irrigation Repairs · Winterisation & Blow-Outs · Drip Irrigation ·
French Drains · Catch Basins & Surface Drainage · Downspout & Foundation Drainage ·
Re-Grading for Runoff

All eight trace to Grizzly's own "system design, installation, repairs, and water management", and
the technical claims match what the FAQ page already says about drainage diagnosis and winterisation.

**Not cloned from their page**: their *Line Jetting* service (Grizzly does not advertise it) and
their *Commercial Drainage Installations* block — Sam's residential-only instruction from the
Projects page applies site-wide.

Copy blocks: "Diagnose First, Dig Second" (four-point checklist) and "Cut Before the Finish Work".
Step 03 is **"We Fix It"**. Banner is the perforated-drain-pipe trench.

Form: `Irrigation & Drainage - Free Consultation`, domId `irrigation-consultation`, service field
relabelled "Irrigation, drainage, or both?".

The Services page irrigation card now links here.

### Mobile carousel on the "Water In, Water Out" cards (2026-09-17)

At ≤767px the eight cards used to stack into one column — a very long scroll. They are now a
horizontal scroll-snap carousel. Desktop (3-col) and tablet (2-col) are untouched.

Scoped with **combo classes** so the shared `.sa-cards` / `.sa-card` used by the other service
pages keep their behaviour:

| Style | Breakpoint | What it does |
|---|---|---|
| `.sa-cards.is-carousel` | `small` | flex row, `overflow-x:auto`, 16px gap, `scroll-snap-type:x mandatory`, `margin:0 -24px` + `padding:0 24px` to bleed past the `.gf-shell` gutter |
| `.sa-card.is-carousel-item` | `small` | `width:82%`, `flex-shrink:0`, `scroll-snap-align:start` |
| `.sa-swipe-hint` | base `display:none`, `small` `display:block` | new paragraph "Swipe to see all eight →" above the track, gold, mobile only |

The snap properties are **native Webflow styles**, so the carousel renders in the Designer canvas
and Preview. Only the scrollbar-hiding rule lives in page head CSS, because `::-webkit-scrollbar`
is a pseudo-element. Verified at 375 / 768 / 1280px: card 268px with the next peeking ~90px, all
eight reachable, and `scrollWidth === clientWidth` so the page never scrolls sideways.

New element: swipe hint `85354822-233a-449a-d37d-403bdcc4a75e`. Track is
`61650c7e-0693-dc7b-34c2-dedb08952cc3`. Details in
`lessons/webflow-style-api-accepts-scroll-snap.md`.

**To repeat it on another service page:** the three styles already exist site-wide, so it is only
`set_style` → `["sa-cards","is-carousel"]` on that page's track, `["sa-card","is-carousel-item"]`
on each card, plus the hint paragraph and the head-CSS block.

**Outstanding on this page:** seven of the eight cards link to `/projects?cat=excavation` — a
leftover from the clone. Only "Drip Irrigation" points at `?cat=irrigation`. Being fixed separately.

**Build trap hit here:** the first build of the expander labels shipped Webflow's placeholder
"This is some text inside of a div block." to all four, because `set_text` is silently dropped on
`TextBlock` and inside nested `children[]` while still returning success. See
`lessons/webflow-set-text-silently-ignored-on-blocks.md` — always read text back after a build.

### County city lists are now expandable (2026-09-17)

"Our Puget Sound Service Area" listed all 30 cities at once. Each county now shows **three rows**,
fades out over a partial fourth, and carries a gold **"SEE MORE CITIES ▾"** control. The two
counties toggle independently and collapse back via "SHOW FEWER".

Because `.sa-counties` is `1fr 2fr` on desktop, Snohomish (1 column) shows 3 cities and King
(2 columns) shows 3 rows = 6 cities — the same collapsed **height**, which is what keeps the two
columns aligned. Below 767px King drops to one column and also shows 3 cities.

**No JavaScript.** It is a hidden `<input type="checkbox">` plus `:checked ~` sibling CSS, so it
cannot break if a script fails, and it is keyboard operable. `<details>` was rejected: a closed
`<details>` hides *all* non-summary children, so the three-city peek is impossible.

Structure added inside each county block, wrapping the existing `.sa-city-list`:

```
.sa-more
  input.sa-more-toggle      (type=checkbox, domId sno-more / kc-more; 1px, opacity 0)
  .sa-more-clip             (overflow hidden, max-height 122px)
     .sa-city-list          (MOVED here, untouched)
     .sa-more-fade          (absolute, 30px, gradient to #F5F7F8)
  label.sa-more-btn         (for= the toggle)
     span.sa-more-label "See more cities"
     span.sa-more-less  "Show fewer"   (display:none until checked)
     span.sa-more-arrow                (CSS border triangle, rotates 180° when open)
```

All three children of the label are **spans**, not divs — `<label>` takes phrasing content only.

`max-height:122px` = three 33px rows on a 35px pitch, plus half the fourth. The fade is **30px**,
starting at 92px so it clears the third row's glyphs entirely — at 58px and again at 40px it dimmed
the third city, which is wrong. Open state is `max-height:1400px` against a real worst case of
698px (King, one column, 20 cities).

Verified by clicking the real markup at 1240px and 375px: collapsed = exactly 3 full rows + a
partial 4th; expanded = clip height equals list height on both counties (348px desktop, 698px King
on mobile), last cities Snohomish/Woodinville reached, fade to opacity 0, arrow rotated, label
swapped; collapse-back returns to 122px with everything restored; counties toggle independently;
no horizontal page overflow.

New element ids — Snohomish wrapper `380b1c99-31fc-0f0e-ddb7-90e4c0a251c4`, clip
`54b8d1a1-ff7c-0cfa-2627-5ebd6fecd7bd`; King wrapper `b6b81553-28c3-5b23-4ba1-07c82df7bcfd`, clip
`1d4b9362-baa5-2304-ad62-70883c81b71c`. Mechanics in
`lessons/webflow-jsless-expander-via-custom-tag-checkbox.md`.

**Designer caveat:** the collapsed look (clip, fade, arrow) renders in the Designer, but the toggle
itself only works on the published site — Webflow does not run page custom code in the canvas or
Preview. Test the expand on a published/staging URL, not in Preview.

**To repeat on another page:** all nine styles exist site-wide now. Rebuild the wrapper, move that
page's `.sa-city-list` into the clip, and give the two checkboxes **page-unique domIds** — ids must
not collide if two service pages are ever on one page.

### Contact section compressed (2026-09-17)

The "LET'S CHAT / Contact Us" band is the shared **Contact form** component
`dc6a1dbd-61f7-16a0-df98-5b8cfc257037`, used on exactly **two** pages: `/irrigation-drainage` and
`/services`. Changes below are to that component's classes, so they apply to both.

Measured on the live site before changing anything:

| | desktop 1280px | mobile 375px |
|---|---|---|
| section height | 1087px | 1825px |
| text column | 578px | 740px |
| form column | **927px** | 875px |
| info block (3 cards) | 375px | **526px** |

**On desktop the form column sets the height** — the text column had 349px of slack, so compressing
the info cards there saves nothing. The cards were the real problem on mobile, where the columns
stack and the cards go icon-above-text at ~155px each.

Changes: `.rt-contact-one-information-box` back to a **row** (icon beside text) at medium/small/tiny
with 14–16px padding; `.rt-info-block` to one column with a 12px row gap at small/tiny;
`.rt-component-section-8` padding 80→56px (40px at small); `.rt-contact-para` margin-bottom
50→28px; `.rt-info-details.rt-align` and `.rt-contact-type` left-aligned on mobile instead of
centred.

**Result: mobile 1825 → 1518px (−307px). Desktop 1087 → 1039px (−48px).**

Two latent bugs fixed on the way:
- `.rt-info-details` had default `min-width:auto` so it would not shrink, squeezing the 30px icon to
  **width 0** — the mail/phone/pin icons were missing on mobile on the live site. Fixed with
  `min-width:0` + `flex-shrink:0` on `.rt-info-icon`.
- `.rt-category-cards-text-2.rt-text-lowarcase` carried a hardcoded `width:385.78125px` at medium,
  so the email overflowed its card and was clipped. Fixed with `width:auto` + `max-width:100%`.

**To shorten desktop further** the form column is the only lever: its fields are 84px tall
(`.rt-contact-form-text-field`, padding 25/29 + 20px margin). Trimming to ~16/16 padding and a 14px
margin would take roughly 110px off both breakpoints. Not done — out of scope.

**NOT changed, needs Sam's decision (both live right now):**
- The email label reads **"Emain"** (prop Text 4) — typo for "Email".
- The phone **link** is `tel:888 456 7890` (prop Link 2) while the displayed text is
  (425) 648-9443. Tapping the number on a phone dials the wrong number.
- The form has **two identical "Full Name" inputs** (both `id="RT-Contact-V4-Name"`,
  name "RT Contact V4 Name") — a duplicate field, and duplicate ids are invalid.
- The form's own settings are `method: get` with no action and no redirect, and the email address
  the value links to is capitalised `Admin@...` while the visible text is lowercase.

### All six service detail pages now exist.

---

## Fencing

Built 2026-09-18 by **duplicating `/service-irrigation-drainage` in the Designer** (Sam created the
empty clone; this pass rewrote it). Page `6aac82cacfbd61d8e890591e`, slug `/service-fencing`.
Because it is a duplicate, it inherits the mobile carousel, the expandable county lists and the
shared Contact form component — no structural work was needed, only wording.

**Eight sub-services**, each traceable to the fencing copy already live on `/services`
("Installation, repair and replacement of wood, stained and custom fences"):

Fence Installation · Cedar Privacy Fences · Fence Repair & Board Replacement ·
Fence Replacement & Removal · Gates & Hardware · Post Setting & Footings ·
Fencing on Slopes & Grade Changes · Property Lines & Permits

Copy blocks: "The Posts Are the Fence" (four-point checklist) and "Built Around What Is Already
There". Step 03 is **"We Build It"**. Banner swapped to 348s-8.jpg
`67956db7406d3f1f2ebdc9b1` (cedar fence + concrete stairway) with new alt text.

**No form rename needed** — unlike the earlier pages, this template uses the shared Contact form
component, whose copy is service-neutral. Leaving it alone also avoids editing the two other pages
that share it.

### SEO
- Title `Fence Installation & Repair | Grizzly Landscape & Construction, Lynnwood WA` — the clone
  had shipped with title "Fencing" and the *irrigation* meta description verbatim.
- Description rewritten around cedar, gates, repair and replacement.
- Open Graph set to inherit title and description (was blank).
- **JSON-LD added**: `Service` + `hasOfferCatalog` of the eight sub-services, with a `LocalBusiness`
  provider, `areaServed` for both counties, plus a `BreadcrumbList`. Neither this page nor
  `/service-irrigation-drainage` had any structured data before — worth back-filling on the others.

### Stale-href trap — the important find
Duplicated pages carry the source page's **custom `href` attributes**, and in Webflow a custom
`href` attribute **overrides** the Designer link setting in published output. On this page nine
links had a setting pointing one place and an attribute pointing somewhere else:

- hero CTA: setting `/contact`, attribute `#consult` (an anchor that does not exist on this page)
- all eight card links: setting → Gallery, attributes `/projects?cat=excavation` (seven) and
  `/projects?cat=irrigation` (one) — and **`/projects` is not a page on this site**

All nine attributes removed, so the link settings now win. This is the same defect the irrigation
spec logged as "seven of the eight cards link to `/projects?cat=excavation` … being fixed
separately" — the cause was the attribute, not the setting.

### Services page
The Fencing card now links to this page and reads "Learn more"; its stale
`href="/projects?cat=fencing"` attribute was removed.

**Still broken on `/services`, not touched:** the Landscape Construction and Irrigation & Drainage
cards have the same stale attributes (`/projects?cat=construction`, `/projects?cat=irrigation`)
overriding correct page settings, so both currently go to a nonexistent path. Same one-line fix.


---

## Lighting & Hardscaping

Built 2026-09-18, same method as Fencing: Sam duplicated `/service-irrigation-drainage` in the
Designer, this pass rewrote it. Page `6aac8b3fd3df9fd0ca30b3e4`, slug
`/service-lighting-hardscaping`.

**Duplicates keep the source page's element IDs.** Every ID used on the fencing page worked
unchanged here, so the rewrite is a straight replay of the same action list with new copy. Worth
knowing for the Excavation page.

**Eight sub-services**, grounded in the `/services` card copy ("Outdoor lighting design, patios,
walkways, retaining walls and fire pits. Low-voltage runs are tidiest when they go in alongside the
irrigation during a build, but a retrofit through existing beds is very doable"):

Landscape Lighting Design · Path & Step Lighting · Uplighting & Tree Lighting ·
Low-Voltage Wiring & Transformers · Paver Patios & Walkways · Garden Paths & Stone Edging ·
Fire Pits & Seating Walls · Lighting Retrofits

**Retaining walls deliberately not given a card**, although the `/services` card names them — they
are already card 02 on `/landscape-construction` and repeating them here would have the two pages
competing for the same term. Garden Paths & Stone Edging took the slot instead; it matches what the
banner photo actually shows.

Section H2 "After Dark, and Underfoot". Copy blocks "Light the Task, Not the Yard" (four-point
checklist) and "Wire It While the Ground Is Open". Step 03 "We Build It". Banner swapped to
`679324d771e6148615a24162` (gravel path, stone edging, timber lantern) with new alt text.

Same nine stale `href` attributes removed as on the fencing page — see the stale-href trap above;
it will recur on every page duplicated from this template.

### Services page
The Lighting & Hardscaping card now links to this page, reads "Learn more", and its
`href="/projects?cat=lighting"` attribute is gone.

**Still broken on `/services`:** the Landscape Construction and Irrigation & Drainage cards keep
stale `href` attributes overriding correct page settings, so both go to a nonexistent `/projects`
path.

### SEO — handed to Sam as text, not written
Sam asked for this page's SEO as copy-paste text rather than applied through the API, so the page
still carries the clone's title "Service - Lighting & Hardscaping" and the **irrigation** meta
description until he pastes it in. Values supplied: title, meta description, Open Graph (inherit),
and the `Service` + `BreadcrumbList` JSON-LD.


---

## Excavation

Built 2026-09-18, same method again: Sam duplicated `/service-irrigation-drainage`, this pass
rewrote it. Page `6aac8dc84c9fa2ffdaffc905`, slug `/service-excavation`. Element IDs matched the
template for the third time running, so the whole rewrite was one replay of the same action list.

**Eight sub-services**, grounded in the `/services` card copy ("Site preparation, utility trenching,
grading and small-scale demolition, handled by our own crew rather than subcontracted out"):

Site Preparation & Clearing · Grading & Slope Correction · Utility Trenching ·
Small-Scale Demolition · Stump & Root Removal · Backfill & Compaction ·
Hauling & Spoil Removal · Tight-Access Excavation

Section H2 "Everything That Happens First". Copy blocks "Groundwork Decides the Finish"
(four-point checklist) and "One Crew, One Mobilisation" — the latter leans on the one real
differentiator the site already claims, that excavation is not subcontracted. Step 03 "We Dig It".

**Banner image not changed** — the inherited photo `67956db73d3f3dc62dec2788` is the excavated
trench with drain pipe, which is genuinely an excavation shot. Only the alt text was rewritten to
describe it as trenching rather than drainage installation. First page in this series where the
clone's photo was already correct.

**Not cloned**: no French drains / catch basins / re-grading-for-runoff cards. Those belong to
`/service-irrigation-drainage` and repeating them here would set the two pages competing. Drainage
appears on this page only as something trenched for, not as a service.

Same nine stale `href` attributes removed — third occurrence, it is now confirmed as a property of
every duplicate of this template.

### SEO — applied directly this time
Title `Excavation & Site Preparation | Grizzly Landscape & Construction, Lynnwood WA`, new meta
description, Open Graph set to inherit, and `Service` + `BreadcrumbList` JSON-LD written. The
title/description write hit a 429 on first attempt and succeeded on retry — worth batching page
writes if a run does many.

### Services page
The Excavation card now links here and reads "Learn more". Its link setting was `linkType: "none"`
with a stale `href="/projects?cat=excavation"` attribute — so before this change the card went
nowhere useful at all.

**Still outstanding on `/services`:** the Landscape Construction and Irrigation & Drainage cards
keep stale `href` attributes overriding correct page settings. Raised with Sam twice, not yet
actioned.
