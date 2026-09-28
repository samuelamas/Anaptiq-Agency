# WHTML `<a href="#anchor">` needs a follow-up `set_link`

`data_whtml_builder` resolves `href` for `mailto:`, `tel:` and path URLs into a real
Webflow link setting (`settings.link.linkType` = email / phone / url). A **hash href does not
resolve**: the Link element comes back with `attributes: {href: "#estimate"}` and **no
`settings.link` at all**, so Webflow has no link target of its own for it.

Fixing it via the settings tool fails —
`set_settings key:"href"` → `Setting "href" is not applicable to this element`.

**Do:** use `data_element_tool > set_link` with `linkType: "url"` and `link: "#estimate"`.
That applies cleanly and can be batched (33 in one call succeeded).

Section anchors themselves are fine: an `id="estimate"` on a div **does** become the element's
`domId`, so only the links need repair.

Related: [[webflow-whtml-img-needs-s3-url]]
