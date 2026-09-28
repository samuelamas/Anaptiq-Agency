# Hardscape SERP plan — /service-landscape-construction

Written 2026-09-18 against the five-competitor study. Every "live now" fact below was pulled from
served HTML today, not assumed.

## Live state of the page (measured 2026-09-18)

| | Grizzly | Bar to beat |
|---|---|---|
| URL | `/service-landscape-construction` (`/landscape-construction` 301s here) | Greenway `hardscapes-in-<city>-wa` |
| Title | `Landscape Construction & Hardscaping \| Grizzly Landscape & Construction, Lynnwood WA` — good | — |
| Words | 1,097 | New Life Lynnwood wall page 1,438 |
| City mentions | 23 total across 10 cities | New Life 68 on one page |
| JSON-LD | **zero blocks served** | New Life also zero — but Classic has the best in market |
| Prices | zero `$`, zero "price" | Sta-Built publishes $8,000–$25,000 |
| "seating wall" | 0 | Sta-Built is the only firm with it |
| "permit" | 0 | nobody has it |
| Hardscape city pages | **0** | Greenway 5, Retaining Walls Seattle 47 URLs |

## The five competitors, and what actually displaces each

1. **New Life Rockeries** — beat with *served* schema. They are React; anything they inject is
   client-side. Webflow ships static HTML, so correct `Service` + `FAQPage` in the source is a
   structural advantage they cannot match without an SSR rebuild.
2. **Sta-Built** — 400+ reviews is unbeatable this year. Their content moat is prices and
   seating walls. Take both. They have no `Service` or `AggregateRating` markup, so priced
   `FAQPage` answers on Grizzly's pages can win the snippet their reviews can't.
3. **Greenway** — ranking on a 5×2 grid alone with 4.4 on 7 reviews. Build the same grid with real
   photos, a live licence and real numbers behind it. Lowest-resistance target in the set.
4. **Rich Landscaping** — their `AggregateRating` ships `ratingValue: null`, which earns nothing.
   Valid markup is the whole gap.
5. **Retaining Walls Seattle** — **do this one first.** 47 city URLs, zero reviews, and a UBI that
   resolves to Horizon Concrete & Design of Renton registered 8 months ago against an "over 10
   years" claim. Nothing is holding those pages up. Retaining-wall city pages displace them
   before the paver pages displace anyone.

Ace 1 (5.0 on 3 reviews) and Grizzly (5.0 on 7) have the same weakness — see the rating note below.

---

## Fix order

### 1. Two Grizzly pages are competing for "hardscaping" (30 min)
`/service-landscape-construction` is titled "…& Hardscaping" and `/service-lighting-hardscaping`
is H1'd "Outdoor Lighting & **Hardscaping**". Worse, that second page is still shipping the clone's
title `Service - Lighting & Hardscaping` and the **irrigation meta description** verbatim —
confirmed live today, the SEO text handed to Sam on 09-18 was never pasted.

Decision: construction owns every hardscape term. Retitle the lighting page to
`Landscape Lighting Design & Installation | Grizzly Landscape & Construction, Lynnwood WA`,
drop "hardscaping" from its H1 and title, paste the real meta description.

### 2. JSON-LD on this page (1 hr)
Fencing and Excavation got `Service` + `BreadcrumbList`. This page — the most valuable one — has
**zero blocks served**. Paste the block at the bottom of this file into page head custom code.

**Do not add `AggregateRating` yet.** Grizzly is 5.0 on 7 Google reviews; that is precisely the
weakness the study flags against Ace 1. Ship it at 20+ reviews. Google no longer renders stars for
self-serving `LocalBusiness` reviews anyway, so the win here is entity clarity, not stars.

**Do not put a `postalAddress` in it** until the three conflicting addresses are settled — a wrong
address in schema is worse than none.

### 3. Restore the priced paver content (2 hrs, needs Danny)
`/pavers` 404s and still ranks ~#3 for "how much does a paver patio cost in kirkland wa" with an
indexed snippet reading roughly $25–$45 per square foot installed. It also produced the only
generative answer in the entire market — cited to Sta-Built, not Grizzly.

- 301 `/pavers` → this page, and `/landscape-design`, `/reviews`, `/who-we-serve`,
  `/ultra-renovations` to their nearest live pages.
- Add a **Cost** section to this page: per-square-foot paver range, retaining-wall range per face
  foot, and what moves the number (access, excavation depth, wall height, drainage).
- Every number in it confirmed by Danny before publish. Ranges, not single figures.

### 4. Seating walls + fire pits section (1 hr)
Zero mentions today. It is Sta-Built's only unique content and Grizzly already sells it. New H3
block on this page, plus one FAQ ("Can a seating wall double as a retaining wall?").

### 5. The hardscape city grid — 10 pages (the actual ranking lever)
The house rule holds: one service, one city, both in the title. This page is a hub and hubs do not
rank here. Build, walls first:

```
/retaining-walls-lynnwood-wa      /paver-patios-lynnwood-wa
/retaining-walls-kirkland-wa      /paver-patios-kirkland-wa
/retaining-walls-bothell-wa       /paver-patios-bothell-wa
/retaining-walls-kenmore-wa       /paver-patios-kenmore-wa
/retaining-walls-edmonds-wa       /paver-patios-edmonds-wa
```

(Confirm the five cities match the study's set — Kirkland is a separate market from Lynnwood and
should be treated as its own campaign, not a spoke.)

Titles: `Retaining Wall Contractor in Lynnwood, WA | Grizzly Landscape & Construction`.

**Each page needs 1,200+ words that could not be published about another city.** That is the one
rule that matters, because 98.4%-identical city pages is the exact defect already logged against
Grizzly's existing sixteen. Per page:

- the soil and what it means for a footing — Vashon glacial till and hardpan, perched water
  tables, why a wall on that ground drains or fails
- the permit threshold for that city, **verified against that city's own code page before it is
  written** (a Kirkland permit claim was already retracted once on this account — every sentence
  gets a source URL in a comment)
- critical-area / steep-slope overlay if the city has one
- named neighbourhoods and the slope conditions in them
- one real Grizzly job in or near that city, with a photo and what the site conditions were
- 4–6 FAQs, at least two with a number in the answer, marked up as `FAQPage`
- the licence number, displayed

Nobody in the set has permit or geology content except New Life, and they have it in one city.

### 6. Housekeeping (20 min)
`sitemap.xml` lists every URL as **non-www** while the canonical is **www** — and non-www returns
200 rather than redirecting, so both hosts serve. Regenerate the sitemap on www and add the ten new
URLs.

---

## Expected order of wins

Walls city pages take Retaining Walls Seattle's positions first (nothing behind them), then
Greenway's (structure only). Sta-Built's pack positions are not winnable this year — take their
snippets with priced answers instead. New Life is the long fight: schema and permit depth.

---

## JSON-LD to paste (page head, `/service-landscape-construction`)

Replace `LICENCE-NUMBER` with the verified L&I number. No address, no rating — see §2.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Service",
      "@id": "https://www.grizzlylandscapeconstruction.com/service-landscape-construction#service",
      "name": "Landscape Construction & Hardscaping",
      "serviceType": "Hardscape construction",
      "description": "Paver patios, retaining walls, stairs and pathways, rockeries, seating walls, grading and drainage across Snohomish and King County, Washington.",
      "url": "https://www.grizzlylandscapeconstruction.com/service-landscape-construction",
      "provider": { "@id": "https://www.grizzlylandscapeconstruction.com/#business" },
      "areaServed": [
        { "@type": "City", "name": "Lynnwood", "containedInPlace": { "@type": "AdministrativeArea", "name": "Snohomish County, WA" } },
        { "@type": "City", "name": "Kirkland", "containedInPlace": { "@type": "AdministrativeArea", "name": "King County, WA" } },
        { "@type": "City", "name": "Bothell" },
        { "@type": "City", "name": "Kenmore" },
        { "@type": "City", "name": "Edmonds" }
      ],
      "hasOfferCatalog": {
        "@type": "OfferCatalog",
        "name": "Landscape construction services",
        "itemListElement": [
          { "@type": "Offer", "itemOffered": { "@type": "Service", "name": "Paver Patios & Walkways" } },
          { "@type": "Offer", "itemOffered": { "@type": "Service", "name": "Retaining Walls" } },
          { "@type": "Offer", "itemOffered": { "@type": "Service", "name": "Seating Walls & Fire Pits" } },
          { "@type": "Offer", "itemOffered": { "@type": "Service", "name": "Stairs & Pathways" } },
          { "@type": "Offer", "itemOffered": { "@type": "Service", "name": "Rockeries & Stone Features" } },
          { "@type": "Offer", "itemOffered": { "@type": "Service", "name": "Outdoor Living Spaces" } },
          { "@type": "Offer", "itemOffered": { "@type": "Service", "name": "Grading & Drainage" } },
          { "@type": "Offer", "itemOffered": { "@type": "Service", "name": "Land & Soil Preparation" } },
          { "@type": "Offer", "itemOffered": { "@type": "Service", "name": "Planting & Garden Design" } }
        ]
      }
    },
    {
      "@type": "LandscapingBusiness",
      "@id": "https://www.grizzlylandscapeconstruction.com/#business",
      "name": "Grizzly Landscape & Construction",
      "url": "https://www.grizzlylandscapeconstruction.com/",
      "telephone": "+1-425-648-9443",
      "priceRange": "$$",
      "hasCredential": {
        "@type": "EducationalOccupationalCredential",
        "credentialCategory": "Washington State Contractor Registration",
        "identifier": "LICENCE-NUMBER"
      },
      "areaServed": [
        { "@type": "AdministrativeArea", "name": "Snohomish County, WA" },
        { "@type": "AdministrativeArea", "name": "King County, WA" }
      ]
    },
    {
      "@type": "BreadcrumbList",
      "itemListElement": [
        { "@type": "ListItem", "position": 1, "name": "Home", "item": "https://www.grizzlylandscapeconstruction.com/" },
        { "@type": "ListItem", "position": 2, "name": "Services", "item": "https://www.grizzlylandscapeconstruction.com/services" },
        { "@type": "ListItem", "position": 3, "name": "Landscape Construction & Hardscaping" }
      ]
    }
  ]
}
</script>
```

Second block, added once the Cost section and its answers exist on the page — the answer text must
match the visible copy word for word or it is a violation:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    { "@type": "Question", "name": "How much does a paver patio cost in the Lynnwood area?",
      "acceptedAnswer": { "@type": "Answer", "text": "PASTE THE VISIBLE ANSWER — Danny-confirmed range only." } },
    { "@type": "Question", "name": "Do I need a permit for a retaining wall?",
      "acceptedAnswer": { "@type": "Answer", "text": "PASTE THE VISIBLE ANSWER — verified against the city's own code page." } },
    { "@type": "Question", "name": "Can a seating wall also hold back soil?",
      "acceptedAnswer": { "@type": "Answer", "text": "PASTE THE VISIBLE ANSWER." } }
  ]
}
</script>
```
