# `FormCheckboxInput` rejects `name` at creation

Passing `settings: [{key:"name", …}]` to `data_element_builder` for a
`FormCheckboxInput` fails the child with:

> Setting "name" is not applicable to this element

and the parent is still created — so you get a `partial_success` with a consent
row that has text but no checkbox. Plain `FormTextInput` / `FormTextarea` accept
`name`, `type` and `required` atomically at creation; the checkbox does not.

**Why:** asking for a `FormCheckboxInput` actually creates a
**`FormCheckboxWrapper`**, containing the real `FormCheckboxInput` plus a
`FormInlineLabel` reading "Checkbox". The `name` belongs to the inner input, not
the thing you asked to create.

**Do:** create the checkbox with **no settings**, read back the wrapper's
children, then `data_element_settings_tool > set_settings` with `key: "name"` on
the inner `FormCheckboxInput` (confirm `applied_keys` contains `name`), and
`set_text` the inline label. Same shape for the submit button: its copy is the
`buttonText` setting, not `set_text`.

Related: [[webflow-setting-keys-are-narrow]]
