# The style API accepts CSS properties the Designer UI never exposes

`data_style_tool > update_style` stored **`scroll-snap-type: x mandatory`**,
**`scroll-snap-align: start`**, **`scroll-padding-left`**, `overflow-x` and `overflow-y`
without complaint, and read them straight back in `query_styles`. None of these have a control
in the Designer's Style panel.

That matters because a scroll-snap carousel built this way is a **native Webflow style**, so it
renders in the Designer canvas and in Preview — unlike a carousel built in page custom code, which
Webflow does not execute outside a published site (see
[[webflow-native-tabs-cannot-be-built-past-three]]).

**Do:** try the real CSS property name first. Only fall back to page head CSS for things the style
engine genuinely cannot express — pseudo-elements above all. Hiding the scrollbar still needs
custom code, because `::-webkit-scrollbar` is a pseudo-element:

```
.sa-cards.is-carousel{scrollbar-width:none;-ms-overflow-style:none;}
.sa-cards.is-carousel::-webkit-scrollbar{display:none;}
```

## Scope a responsive change with a combo class, not the base class

`.sa-cards` / `.sa-card` are shared by every cloned service-detail page. Editing them at the
`small` breakpoint would have silently restyled all of them. Instead:

1. `create_style` with `parent_style_names: ["sa-cards"]` and **`properties: []`** — an empty base
   is accepted, so the combo is inert at desktop.
2. `update_style` with `breakpoint_id: "small"` puts the whole carousel on the combo only.
3. `set_style` with `["sa-cards","is-carousel"]` applies it. Two names = the combo, which now
   exists, so this succeeds — the failure mode in
   [[webflow-whtml-strips-the-root-class]] is passing two names for a combo that was never created.

Specificity handles the rest: `.sa-cards.is-carousel` (0,2,0) beats the base `.sa-cards` small-
breakpoint rule inside the same media query, so `display:flex` overrides `display:grid` cleanly.

## Edge-bleed maths that does not overflow the page

The track sits inside `.gf-shell` (`padding: 0 24px`). Giving the track `margin: 0 -24px` +
`padding: 0 24px` makes it exactly viewport-wide: verified `documentElement.scrollWidth === clientWidth`
at 375px, so there is **no horizontal page overflow**. Keep the trailing gutter as the track's own
`padding-right` — adding `:last-child{margin-right:24px}` on top double-counts it and the last card
ends 48px from the edge against 24px at the start.

Related: [[webflow-native-tabs-cannot-be-built-past-three]]
