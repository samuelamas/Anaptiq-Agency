# WHTML drops the class on the single root element — and never creates its style

`data_whtml_builder` applies every class in the fragment **except the ones on the root element**.
Insert `<div class="rl-page rl-hero">…</div>` and the inserted Block comes back with
`styleNames` absent, while every descendant keeps its classes. The root's `id` attribute *does*
survive as `domId`; only the classes are lost.

Worse, the style is never created either — the `.rl-hero { … }` rule in `css` is silently
discarded along with the class, so a later `set_style` fails with
`One or more styles not found: rl-hero`. There is **no warning** for this; the only warnings
returned are the site's pre-existing `._w-input parent` duplicates.

The symptom this produced: every section lost its background and padding, and the hero's
`position:absolute` scrim — whose `position:relative` parent had vanished with `.rl-hero` —
escaped to the viewport and covered the nav bar. The nav looked like it was *under* the hero.

**Do:** either wrap the fragment in a throwaway outer div so the real section is a child, or
create the section styles up front with `data_style_tool > create_style` and apply them with
`data_element_tool > set_style` after the insert. Breakpoint values go on afterwards with
`update_style` + `breakpoint_id` (`medium` = 991px, `small` = 767px, `tiny` = 479px).

**Two traps while repairing this:**

1. **A seed element with empty divs creates nothing.** `<div class="rl-hero"></div>` is discarded
   before the style is registered. Give each seed div a child (`<p>seed</p>`) or the styles still
   will not exist.
2. **`set_style` with two names means a combo class.** `style_names: ["rl-page","rl-hero"]` fails
   with `styles not found` even when both classes exist individually — it is looking for the combo
   `.rl-page.rl-hero`. Pass **one** class name per element, and do not build a page whose
   head CSS depends on a shared wrapper class being present alongside a section class.

Related: [[webflow-whtml-img-needs-s3-url]], [[webflow-hash-links-need-set-link]]
