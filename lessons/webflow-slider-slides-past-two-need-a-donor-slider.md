# Webflow Slider slides past the first two must be harvested from a donor Slider

`data_element_builder` has `{type:"Slider"}` but **no `SliderSlide` type**, exactly as with Tabs.
A new Slider is created with a SliderMask holding **two** SliderSlides. Appending a plain
`DivBlock` into the mask looks right in the element tree and renders, but Webflow's slider script
only cycles elements carrying `w-slide` — so the extra cities **never appear** and the rotator
silently loops the first two. This is how `/service-excavation` shipped: 17 city "slides" of which
only Kirkland and Redmond were real slides, and after a trim to three, Redmond was a dead `Block`.

**The donor workaround works cleanly here, unlike Tabs.** Slides have no link↔pane pairing to
corrupt, and the nav dots are generated at runtime from the slide count:

1. `data_element_builder {type:"Slider"}` appended to Body — one donor per slide needed.
2. `move_element` one of its two SliderSlides into the real SliderMask (`append`).
3. `set_style` the moved slide to the project's slide class (replaces the default styles).
4. `move_element` the label Block into the new slide, then `remove_element` the old stray Block.
5. `remove_element` each donor SliderWrapper (it keeps one slide, which is fine — the whole
   wrapper goes).

A donor yields exactly one usable slide, because a Slider cannot be emptied of its last slide.

**Verify by element type, not by text.** `query_elements` on the mask and read each child's
`type`: every city must be `SliderSlide`, never `Block`. A text-only check passes on a broken
rotator. Rotation itself cannot be confirmed in the Designer — Webflow's slider JS runs on the
published site, so publish before judging it.

Related: [[webflow-native-tabs-cannot-be-built-past-three]]
