# Shared Header / Footer components

Recorded 2026-09-11 after the nav sync.

| Component | ID | Notes |
|---|---|---|
| **Header** | `9fa63fb4-3b22-93a4-faaf-e9803f1c201c` | Sam built it in the Designer. 6 instances. |
| **Footer** | `ef920e9b-180c-dade-b17a-afe31713fbdb` | Originally made from the Rich-style homepage CTA + footer. |

## Page coverage after the sync

| Page | Header | Footer |
|---|---|---|
| `/home-rich-style` | component | hand-built `rl-footer` (deliberately restored 2026-09-11) |
| `/services` | component | component |
| `/projects` | component | component |
| `/faq` | component | component |
| `/contact` | component | component |
| `/service-area-edmonds-wa` | component | component (added in this pass) |
| `/` (original Home) | its own `gz-header` | its own `gzh-foot` — untouched Augusta build |

## Bug fixed in the Header component

Both phone links (`Link 1` top bar, `Link 8` nav) had `to: "+1 (425) 648-9943"` — **9943**, while the
visible text on both read "(425) 648-9443". One digit out, so every tap-to-call in the header dialled
a number that is not Grizzly's. Corrected to `+14256489443` (also dropped the spaces and brackets;
`tel:` targets should be bare E.164).

Because the instances carried no overrides, fixing the prop defaults corrected all six pages at once.

## Other Header link changes

| Prop | Was | Now | Why |
|---|---|---|---|
| Link 3 "Services" | `#services` | `/services` | the page now exists; the anchor only worked on the homepage |
| Link 5 "Gallery" | `mode:"page"` with **no target** | `/projects`, relabelled **Projects** | it was a link to nowhere |

## Homepage-only anchors — resolved 2026-09-11

Sam's call: point them at real pages.

- `Link 6` "Service Areas" `#areas` → **`/service-area-edmonds-wa`**. Repoint at a service-area
  index page if one is ever built.
- "Why Grizzly" `#why` → **removed from the nav entirely**. It named a homepage *section*, not a
  page, so it could never resolve site-wide. The `NavbarLink` element was deleted from the component
  definition and its two orphaned props (`Link 4`, `Text 4`) removed with it.
- The header's estimate button carried a bare `href="#estimate"` attribute with no Webflow link
  target — another homepage-only anchor. Bound explicitly to the **Contact** page.

**Final nav: Services · Projects · Service Areas · FAQ · Contact Us**, every item a real page.
Resolve when the homepage question is settled.

## Steps sections restored

The "Get Started Today" 3-step band had been lost from `/services` and `/service-area-edmonds-wa`
during the component swap. Both re-inserted above the footer 2026-09-11.

## Note on concurrent editing
Sam was editing in the Designer during this pass; two `remove_element` / insert calls returned
"Element not found" because he had just deleted the same elements. **Re-read the page tree
immediately before and after any structural change while he is working.**
