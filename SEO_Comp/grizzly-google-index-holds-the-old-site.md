---
name: grizzly-google-index-holds-the-old-site
description: A site: query on 2026-09-17 returned only old-build URLs (Kirkland/Bothell/Kenmore, phone 425-599-6702) that all 404; none of the 26 current sitemap URLs are indexed
---

**Summary:** `site:grizzlylandscapeconstruction.com` returns `/`, `/pavers`, `/irrigation`,
`/excavation`, `/mulching`, `/landscape-design` — the **previous** build, targeting Kirkland,
Bothell and Kenmore with phone **(425) 599-6702**. Every one of those paths except `/` returns
**404** live. Not one of the 26 URLs in the current sitemap (`/services`,
`/service-irrigation-drainage`, the sixteen `/service-area-*` pages) appears in the index.
The live site targets **Lynnwood / Snohomish & King County** with phone **(425) 648-9443**.

Also found: `www` and non-`www` both return 200 and **no page carries a canonical tag**, so every
page exists at two indexable URLs with no consolidation signal. **Corrected 2026-09-18:** canonicals
now ship on every live page, all pointing at `www`, and the non-www host emits the `www` canonical.
The remaining host defect is that `sitemap.xml` still lists every URL as non-www, and non-www still
returns 200 rather than 301 — both fixed by setting www as Webflow's default domain. Domain whois creation
**2026-04-24**; Wayback has snapshots only for 2025–2026.

**Why it matters:** this outranks every on-page critique. No amount of title-tag or content work
moves rankings on pages Google has not crawled. It also explains why competitor comparisons look
paradoxical — Grizzly's indexed corpus is a dead site about different cities.

**How to apply:** verify in Search Console (Coverage + URL Inspection on
`/service-irrigation-drainage`) before recommending anything else; add self-referencing canonicals;
301 the five dead indexed URLs to live equivalents. See
[[grizzly-pavers-url-is-a-404-that-still-ranks]].

**2026-09-18 — the bigger cause found.** All sixteen `/service-area-*` pages are **orphans**: a sweep
of every live page (including the city pages themselves) found zero `href="/service-area…"` anywhere.
The 30-city block on each service page is plain text, not links. Sitemap-only URLs with no inbound
links is the textbook cause of "Discovered – currently not indexed", and it outranks the canonical
issue. Full remediation order in `INDEXING-FIX.md`.
