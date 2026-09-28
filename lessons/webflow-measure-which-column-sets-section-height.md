# Before compacting a section, measure which column actually sets its height

The contact section's three info cards *looked* like the reason the section was tall. On desktop
they were not: measured on the live page at 1280px, the text column was **578px** and the form
column **927px**, so the section was 1087px and the left column carried **349px of slack**.
Compressing the info cards there would have saved exactly nothing.

The same cards *were* the problem at 375px, where `.rt-contact-us-main-block` switches to
`flex-direction:column` and the two columns add instead of overlapping: section 1825px, of which the
info block alone was 526px.

**Do:** before touching anything, run this on the real page at both widths —

```js
const h=el=>el.getBoundingClientRect().height;
h(section); h(leftCol); h(rightCol);   // which is bigger?
```

If the section is a side-by-side flex/grid row, its height is `max(columns)`. Only the taller column
is worth compressing. When the columns stack at a breakpoint, both count.

## Two template traps this surfaced

1. **A hardcoded px width inside a combo class.** `.rt-category-cards-text-2.rt-text-lowarcase` had
   `width: 385.78125px` at the `medium` breakpoint — a Designer drag, baked in. On a 345px phone
   card the email overflowed and `overflow:hidden` clipped it. Override with `width:auto` +
   `max-width:100%`; `overflow-wrap` alone will not help because the width is explicit.
2. **A flex child with default `min-width:auto` squeezes its sibling to zero.** `.rt-info-details`
   refused to shrink below its content, so the 30px icon computed to **width 0** and vanished. Fix
   is `min-width:0` on the shrinking child plus `flex-shrink:0` on the icon. The icon was missing on
   the live site and nobody had noticed.

## Test the CSS against the live DOM before writing it to Webflow

Inject a `<style>` into the published page with the browser tool, measure, screenshot, iterate — then
write the settled values through `update_style`. Real fonts, real content, real breakpoints, and
nothing is saved until it is right. This caught three separate problems that a hand-built mock
would have missed, because the mock would have used *my* assumptions about the markup.

Related: [[webflow-set-text-silently-ignored-on-blocks]]
