# Webflow input placeholders cannot be set through the Data API

A `FormTextInput` created by `data_whtml_builder` keeps `name`, `type` and `required`
from the source HTML but **silently drops `placeholder`**. Both recovery routes fail:

- `set_settings` with `key: "attributes"` → `attributes[0]: "placeholder" is a reserved attribute name`
- `set_settings` with `key: "placeholder"` → `Setting "placeholder" is not applicable to this element`

`get_settings type:"all_raw_settings"` on the input lists only
`domId, visibility, name, required, type, attributes` — there is no placeholder key at all,
yet the attribute writer still treats the name as reserved.

**Do:** design the form with **visible labels** instead of placeholders. Wrap each control in a
field div (`<div class="rl-field"><div class="rl-label">Phone</div><input …></div>`) and make the
field div the grid child. That is better for accessibility anyway, and it survives WHTML intact.

**Recovery** if a placeholder-only form was already inserted: WHTML the replacement form
`after` the existing `FormWrapper`, then `remove_element` the old wrapper, then re-apply the
form settings (name / method / redirect / domId) to the *new* `FormForm` id.

Related: [[webflow-checkbox-name-is-set-after-creation]]
