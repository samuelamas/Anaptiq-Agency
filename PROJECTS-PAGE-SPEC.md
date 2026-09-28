# Grizzly Projects page — Cedar Rustic clone

Built 2026-09-11. Site `6782ba7cbc95e18c7f76bd66`, page **Projects** `6aa35754c7447e733ada72a9`,
slug `/projects`. **Staged, NOT published.**

## Reference
`https://cedarrustic.com/projects` (Webflow). Layout cloned; palette and type match the rest of the
new Grizzly pages (navy `#0B2735`, slate `#48586A`, gold `#AB9114`, grey `#F5F7F8`;
Plus Jakarta Sans + Inter).

## Sections
1. **Hero** — full-bleed photo under a 68% navy scrim; gold rules flanking a 24px uppercase eyebrow
   ("Residential Work" where theirs says "Since 1927"), 72px uppercase H1 "Projects" at 2.88px
   tracking, subtitle, gold Free Estimate button. Their exact type scale.
2. **Breadcrumbs.**
3. **Stats band** — navy, three across. **Placeholder figures**: each number reads `[ NUMBER ]` in
   grey with a visible note underneath. Sam is supplying the real numbers (his call, 2026-09-11);
   the grey styling means no figure can render as fact if the page is published early.
4. **Residential Projects** — two-tone H2 (56px navy "Residential" + 72px gold "Projects", matching
   Cedar Rustic's 56/72 split), filter tab row, 2-up card grid, Load More.
5. **Customer inquiry form** — the same 8-field form as `/contact`, reusing its `gc-*` classes.
6. **Footer.**

## Per Sam's instructions
- **Residential only.** Cedar Rustic's entire Commercial block was dropped; the page says
  "Residential Work" and "Residential Projects" throughout.
- **No cities.** Cedar Rustic titles cards "Rustic Cedar Fence in Joliet, Illinois"; these are
  titled by the work shown.
- **Grizzly's own categories** replace their fence types.

## Categories and cards (12, all real Grizzly photos)

| Card | Category | Asset |
|---|---|---|
| Paver Driveway & Retaining Wall | Landscape Construction | `67956db74a42c429001d5f76` |
| Cedar Fence & Concrete Stairway | Fencing | `67956db7406d3f1f2ebdc9b1` |
| Drip Line Installation | Irrigation & Drainage | `6a2b964eacceb3126a5effdb` |
| Perforated Drain Line | Excavation | `67956db73d3f3dc62dec2788` |
| Hedge Pruning & Shaping | Landscape Maintenance | `67956db78a347375dc8f8282` |
| Garden Path & Stone Feature | Lighting & Hardscaping | `67956db75d39af6db142db65` |
| Japanese-Influenced Garden | Landscape Construction | `6a2b964eb10d0d51771434f9` |
| Rotor Adjustment & System Tune-Up | Irrigation & Drainage | `6a2b97ff807242bd162f1541` |
| Trench Line Along a Hedge | Excavation | `6aa2db6b8fce9271ae23969d` |
| Waterfront Planting Bed | Landscape Construction | `6a2cc427d8c767bf9a8f0a30` |
| Mulch Bed Renewal | Landscape Maintenance | `67956db73d3f3dc62dec2785` |
| Planting Plan & Layout | Landscape Construction | `6a2b964e0914b4c1fc3e9ac6` |

Every card was matched to a category by what the photo actually shows. All six service lines have
at least one card, so no tab returns an empty grid.

## Filter mechanics
Cards carry `data-cat`, tabs carry `data-filter` — both survive WHTML intact. A ~30-line script in
the **page footer** code handles filtering, the active-tab state (`.is-on`, gold) and Load More
(6 at a time, button hides when the filtered set is exhausted). Tabs are keyboard-operable
(`role="button"`, `tabindex="0"`, Enter/Space).

## Form
Native Webflow form. Name `Projects - Customer Inquiry`, domId `projects-customer-inquiry`,
method POST, redirect `/thank-you`. Fields: First-Name · Last-Name · Phone · Email · Address ·
ZIP-Code · How-Did-You-Hear · Project-Details. Submit reads "Send My Request".
Identical in structure to the Contact and FAQ forms.

## Claims deliberately NOT made
No licensed/insured/bonded claim, no warranty, no hours, no pricing, no review or rating claim.
The stats band is the only numeric element and it ships as a marked placeholder.

## Open items
1. **Sam to supply the three stat figures** and delete the placeholder note.
2. Cedar Rustic's cards link to individual project detail pages; these are static tiles, since
   Grizzly has no per-project content. Worth adding later if photo sets exist per job.
3. Several cards use 348x348 gallery thumbnails and are visibly soft at card size — full-resolution
   originals would help most on the Fencing, Excavation and Maintenance cards.

## Filter interactivity — investigated 2026-09-17

Sam reported the category tabs were not clickable. **The filter was not broken.** Webflow does not
run page custom code in the Designer canvas or in Preview, only on a published site, and nothing on
this site has been published — so the footer script had never executed where he was looking.

Verified intact: 7 tabs with `data-filter`, 12 cards with `data-cat`, and the footer script itself.

**Category assignments audited — all 12 correct**: construction 4 (paver driveway, Japanese garden,
waterfront bed, planting plan), irrigation 2 (drip line, rotor), excavation 2 (drain line, hedge
trench), maintenance 2 (pruning, mulch), fencing 1, lighting 1.

**Navigator labels added** so photos can be identified and re-assigned visually in the Designer:
each card reads `CARD • <category> • <title>` and each tab `TAB • <category>`. Re-assigning a photo
is then: select the card → Settings → Custom attributes → change `data-cat`.

**Native Tabs rebuild attempted and reverted.** The Data API cannot build more than three native
tabs, and cannot verify the link-to-pane pairing that a merge would put at risk — see
`lessons/webflow-native-tabs-cannot-be-built-past-three.md`. The page was restored to its working
state rather than left with tabs that would likely open the wrong pane.

