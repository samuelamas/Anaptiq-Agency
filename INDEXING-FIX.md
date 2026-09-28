# Indexing fix — measured live 2026-09-18

## What is already fixed since the 09-17 audit
Self-referencing canonicals are now present on **every** live page, all pointing at `www`. The
non-www host emits the `www` canonical too. That part of
`SEO_Comp/grizzly-google-index-holds-the-old-site.md` is out of date.

## What is still broken, in order of leverage

### 1. All 16 `/service-area-*` pages are orphans — zero internal links, sitewide
Checked every live page including the service-area pages themselves: **not one `href="/service-area…"`
anywhere on the site.** The "Our Puget Sound Service Area" block on each service page lists 30 cities
as plain text, not links. Those pages exist only in the sitemap.

Sitemap-only URLs with no inbound links are the textbook cause of "Discovered – currently not
indexed". This is the single biggest reason the new build is not in the index.

**Fix:** make the 30-city list on the service pages into real links to the matching
`/service-area-*` page, and add a city row to the footer component (which is shared, so it lands
on every page at once). Cross-link the city pages to each other's neighbours.

### 2. Sitemap is on the wrong host
Every `<loc>` in `sitemap.xml` is **non-www** (`https://grizzlylandscapeconstruction.com/…`) while
every canonical is **www**. Google reads a sitemap of URLs their own pages declare non-canonical.
Non-www also returns **200 rather than 301**, so both hosts serve every page.

**Fix (one setting):** Webflow → Site settings → Publishing → set `www.grizzlylandscapeconstruction.com`
as the **default domain**. That regenerates the sitemap on www *and* makes non-www 301. Republish.

### 3. Search Console — nothing else is measurable without it
This is Sam or Danny, not me:
- Verify a **Domain property** (`grizzlylandscapeconstruction.com`) so both hosts report together.
- Submit `https://www.grizzlylandscapeconstruction.com/sitemap.xml` after fix #2.
- Read **Pages → Why pages aren't indexed**. The expected verdicts are "Discovered – currently not
  indexed" (orphans, #1), "Alternate page with proper canonical tag" (non-www, #2) and
  "Not found (404)" (the old build, #4).
- URL-Inspect → **Request Indexing** on these eight, in this order:
  `/`, `/services`, `/service-landscape-construction`, `/service-irrigation-drainage`,
  `/service-area-lynnwood-wa`, `/service-area-kirkland-wa`, `/gallery`, `/faq`.
  Do this **after** 1, 2 and 4 are live — requesting indexing on an unfixed page spends the quota.

### 4. Ten old indexed URLs all 404 — none redirect
Confirmed 404 today on www: `/pavers`, `/irrigation`, `/excavation`, `/mulching`,
`/landscape-design`, `/reviews`, `/who-we-serve`, `/ultra-renovations`, `/about`,
`/landscape-maintenance`. `/landscape-construction` is the only one that 301s correctly.

Those old URLs are what Google actually has indexed, so they are the only equity the site owns. A
404 discards it; a 301 hands it to the live page. `/pavers` still ranks ~#3 on the paver-cost query.

**Webflow → Site settings → Publishing → 301 redirects:**

| From | To |
|---|---|
| `/pavers` | `/service-landscape-construction` |
| `/irrigation` | `/service-irrigation-drainage` |
| `/excavation` | `/service-excavation` |
| `/mulching` | `/services` |
| `/landscape-design` | `/service-landscape-construction` |
| `/reviews` | `/` |
| `/who-we-serve` | `/services` |
| `/ultra-renovations` | `/services` |
| `/about` | `/` |
| `/landscape-maintenance` | see #5 |

### 5. `/landscape-maintenance` is a 404 and a sixth service is missing
The Landscape Maintenance page was built 09-11 and is still **staged, not published** — the URL
404s, it is absent from the sitemap, and nothing links to it. `/services` links only five service
pages. Either publish it (then it needs no redirect) or point the redirect at `/services`.

### 6. Prune the thin city pages before asking Google to index them
Sixteen pages at 98.4% token-identical is a thin-content pattern; Google filters those as "Crawled –
currently not indexed" and de-orphaning them will not save them. Two also carry broken slugs:
`/service-area-mukiteo-wa` (Mukilteo is misspelled) and `/service-area----mercer-island-wa`
(four hyphens).

**Fix:** delete Auburn, Renton, Hunts Point and Mercer Island — outside any plausible radius from
Lynnwood — and rewrite the remaining twelve to genuinely distinct copy. Fix the Mukilteo slug with
a 301 from the old one. Do this **before** requesting indexing.

### 7. Small things on the same pass
- `/thank-you` is in the sitemap and indexable. Add `noindex` and drop it from the sitemap.
- Five `href="#"` dead links on `/services`, plus `tel:8884567890` (wrong number — dials nothing)
  and `mailto:info@example.com` (placeholder) in the shared contact component.
- No external inbound links. Put the `www` URL of each service page into the Google Business
  Profile services section and the main citations — GBP is a genuine discovery path for a five-month-old
  domain (whois 2026-04-24).

## Sequence
2 and 4 first (settings only, 30 min) → 1 and 5 (build work) → 6 (content) → **then** 3.
