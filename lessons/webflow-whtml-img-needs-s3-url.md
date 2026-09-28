# WHTML `<img src>` only binds when the URL is the S3 form

Inserting `<img src="https://cdn.prod.website-files.com/<site>/<asset>">` through
`data_whtml_builder` returns `partial_success` with:

> skipped … since the image does not exist in asset library

even when the asset does exist and the CDN URL returns 200. `create_asset` hands
back **both** `assetUrl` (`https://s3.amazonaws.com/webflow-prod-assets/…`) and
`hostedUrl` (`https://cdn.prod.website-files.com/…`). The builder matches the
asset library on the **s3.amazonaws.com** form — which is also what `list_assets`
returns as each asset's `hostedUrl`.

**Do:** use the `s3.amazonaws.com/webflow-prod-assets/<siteId>/<id>_<name>` URL in
WHTML `<img>` tags and in `background-image:url(...)`. Verified: the footer logo
inserted with that form reported *"1 image(s) linked to existing assets in the
library"*.

**Recovery** if one was already skipped: the Image element still exists with its
alt text, just no asset — bind it with `data_element_tool > set_image_asset` and
the asset id.

Related: [[webflow-mcp-build-order]]
