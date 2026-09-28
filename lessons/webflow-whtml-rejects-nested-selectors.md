# WHTML `css` rejects nested selectors — and fails the whole insert

A descendant selector in the `css` parameter fails the entire action:

> Nested selectors are not allowed. Found: ".sa-step .sa-card-h". Use single class selectors only
> (e.g. .card-image instead of .card img). StyleParser drops descendant selectors.

Unlike the `dropped_style` warnings, this is a hard **error** with `data: null` — the section is
not inserted at all. One nested rule loses the whole fragment, so it is worth scanning the CSS for
spaces inside selectors before sending a large block.

**Do:** give the variant its own flat class. Instead of

```
.sa-step .sa-card-h { color:#FFFFFF; }
```

write a distinct class (`.sa-step-h`) and put it on the element. Combo classes
(`.rl-btn.rl-btn-ghost`, no space) are fine — it is the **space** that is rejected.

Recovery is cheap: the other actions in the same call still succeed, so re-send only the failed
fragment, positioned with `creation_position: "before"` against the element that now follows it.

Related: [[webflow-whtml-strips-the-root-class]], [[webflow-whtml-drops-iframes]]
