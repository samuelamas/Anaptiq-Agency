# WHTML silently drops `<iframe>` — use an HtmlEmbed element

An `<iframe>` inside a `data_whtml_builder` fragment is discarded. The surrounding markup is
created normally and **no warning is returned** — the only sign is that the wrapper `<div>` comes
back as an empty Block and a later `query_elements` with `element_filter: {tag: "iframe"}` returns
zero matches.

**Do:** create a `HtmlEmbed` element with `data_element_builder` inside the wrapper, then write the
markup to its **`code`** setting via `data_element_settings_tool > set_settings`
(`static_text.value`). Verified with a Google Maps embed:

```
data_element_builder → { type: "HtmlEmbed" }   // no settings at creation
set_settings → key "code", static_text.value = "<iframe …></iframe>"
```

Inline `style` on the iframe is the reliable way to size it — the embed's markup is not parsed into
Webflow styles, so a class alone only works if the rule also exists in page head CSS.

A keyless map embed needs no API key: `https://www.google.com/maps?q=<place>&output=embed`.

Related: [[webflow-whtml-strips-the-root-class]], [[webflow-whtml-img-needs-s3-url]]
