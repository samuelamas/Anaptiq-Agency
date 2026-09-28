# A JS-free "show more" expander: `BY_CUSTOM_TAG` checkbox + `:checked ~` CSS

## `<details>` cannot do a faded preview — do not reach for it

The obvious tool is wrong here. A closed `<details>` hides **every** non-`<summary>` child, so
there is no way to leave the first three rows showing with the fourth fading. Keeping the preview
outside the element means splitting one grid into two, which breaks a multi-column city list.

Also do not set `display:flex` on `<details>` to reorder the summary below the content — that has a
history of breaking the closed-state hiding in WebKit.

## What works: a real `<input type="checkbox">` as a sibling

`data_element_builder` with **`type: "BY_CUSTOM_TAG"`** creates genuine DOM elements for tags
Webflow has no native element for. Verified for `input` and `label`:

```
{ type:"BY_CUSTOM_TAG", custom_tag:"input",
  set_attributes:{ attributes:[{name:"type",value:"checkbox"}] },
  settings:[{ key:"domId", static_text:{ value:"sno-more" } }] }
```

comes back as `type:"DOM"`, `settings.dom.tag:"input"`, `attributes:{id:"sno-more",type:"checkbox"}`.
Note `id` is written through the **`domId` setting**, not `set_attributes` — `id` behaves like the
reserved names in [[webflow-input-placeholder-is-not-writable]]. A `label` takes
`for` through `set_attributes` normally.

Do **not** use `FormCheckboxInput` for this — it expands into a wrapper with an inline label
(see [[webflow-checkbox-name-is-set-after-creation]]). `BY_CUSTOM_TAG` gives the bare input.

The order matters: input, then the clipped content, then the label. The input must be a **preceding
sibling** of everything the `~` selector targets, so the label cannot wrap the input.

## Split the work: native styles for appearance, head CSS for state

Put everything that defines the resting appearance on Webflow classes — including
`opacity:0;width:1px;height:1px;position:absolute` on the checkbox, so the raw control is hidden in
the Designer canvas too. Head CSS then only carries the sibling rules, which Webflow's style
engine cannot express:

```
.sa-more-toggle:checked ~ .sa-more-clip{max-height:1400px;}
.sa-more-toggle:checked ~ .sa-more-clip .sa-more-fade{opacity:0;}
.sa-more-toggle:checked ~ .sa-more-btn .sa-more-arrow{transform:rotate(180deg);}
.sa-more-toggle:focus-visible ~ .sa-more-btn{outline:2px solid #AB9114;outline-offset:4px;}
```

Consequence: the **collapsed** state renders correctly in the Designer, but the toggle only works on
the published site, because Webflow does not run page custom code in the canvas or Preview
(see [[webflow-native-tabs-cannot-be-built-past-three]]). Say so when handing over.

## Two measurement traps

1. **Match the fade to the real section background.** The gradient must end on the section's own
   colour (`.sa-area` is `#F5F7F8`, not white) or it shows as a grey smear.
2. **Measure the row pitch; don't guess the clamp.** `.sa-city` is 33px tall on a 35px pitch
   (2px grid gap), so `max-height:122px` = three full rows plus half of the fourth. A fade taller
   than the last row washes out rows that should stay readable — 40px over a 122px clip was right,
   58px was too much.
3. When verifying an expand animation, **re-read after the transition settles**. A measurement
   taken mid-transition reported the collapsed height while the screenshot showed it open.

Related: [[webflow-style-api-accepts-scroll-snap]]
