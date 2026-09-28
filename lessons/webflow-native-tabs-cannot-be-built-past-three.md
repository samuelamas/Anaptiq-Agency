# Native Webflow Tabs cannot be built past three tabs through the Data API

`data_element_builder` with `{type:"Tabs"}` creates a full `TabsWrapper` → `TabsMenu`
(3 × `TabsLink`) + `TabsContent` (3 × `TabsPane`). There is **no element type for `TabsLink` or
`TabsPane`** in the builder enum, so a fourth tab cannot be created directly.

**The merge workaround half-works and must not be shipped.** Creating a second Tabs element and
`move_element`-ing its links/panes into the first does move them, with two hard limits:

1. **A Tabs element cannot be emptied.** Moving the *last* link or pane out fails with
   `MPS rejected update: … Tab Link can not be placed out of its Tabs Menu` (and the pane
   equivalent). Each donor keeps one of each, so N donors yield 2N+1 tabs, not 3N.
2. **The link↔pane pairing cannot be read or written.** `get_settings type:"all_raw_settings"` on a
   `TabsLink` returns only `domId`, `visibility`, `attributes`; on a `TabsPane` only those plus
   `tag`. Webflow's internal tab name (`data-w-tab`) is not exposed, and there is no setting to
   write it.

Each Tabs element numbers its tabs "Tab 1/2/3" independently, so after a merge the menu almost
certainly holds duplicate names and tabs 4+ would activate the *first* pane sharing their name.
That cannot be detected through the API — only by rendering the page.

**Do:** do not attempt more than three native tabs headlessly. Either keep a custom-code filter, or
have the user click "+" in the Designer's Tabs settings to add the extra tabs (they are numbered
correctly when Webflow creates them), then populate the panes by `move_element` into each
`TabsPane` — moving *into* an existing correctly-paired pane is safe.

**Related and important:** Webflow does **not execute page custom code in the Designer canvas or in
Preview** — only on a published site. A filter built as footer `<script>` therefore looks dead in
the Designer even when it is perfectly correct. Check whether the user is testing in the Designer
before assuming the code is broken.

Related: [[webflow-whtml-drops-iframes]]
