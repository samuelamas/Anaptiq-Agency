# `set_text` is silently ignored on TextBlock and on nested `children[]`

This shipped placeholder copy to a page and reported **success** while doing it. Always read the
text back.

## What fails

`data_element_builder` with `type: "TextBlock"` and `set_text` returns
`status: "success"` — and the element is created with Webflow's default
**"This is some text inside of a div block."** The intended text is never written. It comes back
typed as `"Block"`, and a follow-up `data_element_tool > set_text` on it then fails with
*"This element doesn't support text"*, so there is no repair path — the element has to be deleted
and rebuilt.

The same silent drop happens for any `set_text` inside a nested **`children[]`** array, even on
element types that do accept text at the top level.

## What works

| Element | `set_text` at top level | `set_text` inside `children[]` |
|---|---|---|
| `Paragraph` | ✅ | ❌ |
| `TextBlock` | ❌ (always placeholder) | ❌ |
| `BY_CUSTOM_TAG` `span` | ✅ | ❌ |

So: create **one builder action per text element**, positioned with `creation_position`
`before`/`after` against a sibling, rather than one call that builds a whole subtree with text in it.
Build the container with `children[]` if you like, but write every text node as its own action.

`BY_CUSTOM_TAG` with `custom_tag: "span"` accepts `set_text`, and also accepts
`settings: [{key:"text", static_text:{value:"…"}}]`. Both were verified. A span is the right choice
inside a `<label>` anyway, since `<label>` takes phrasing content only — a `TextBlock` or a
`DivBlock` (both `<div>`) is invalid there, as is a `Paragraph`.

## The rule this earns

**A `status: "success"` from the element builder does not mean the content is right.** After any
build that carries copy, `query_elements` with `children_depth: 2` and read the `String` nodes. Four
labels on the service-area expanders went out reading "This is some text inside of a div block."
because the build was verified for *structure* and not for *text*.

Related: [[webflow-jsless-expander-via-custom-tag-checkbox]]
