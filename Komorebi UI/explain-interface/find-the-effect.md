# Finding the layers behind an effect

Search by visual mechanism, not by guessing the markup.

The objective is a defensible layer stack: what visibly contributes, in what relationship, and how certain each part is.

## Start from the region

Before scanning the whole document, identify the visible region the user named.

For a point or small area, `elementsFromPoint()` is often the fastest first read because it returns the visible element stack front-to-back at that location:

```js
(x, y) => document.elementsFromPoint(x, y).slice(0, 10).map(el => {
  const s = getComputedStyle(el);
  const r = el.getBoundingClientRect();
  return {
    tag: el.tagName.toLowerCase(),
    cls: (el.className?.toString?.() ?? '').slice(0, 80),
    box: { x: r.x, y: r.y, width: r.width, height: r.height },
    position: s.position,
    zIndex: s.zIndex,
    background: s.backgroundImage,
    filter: s.filter,
    backdrop: s.backdropFilter,
    blend: s.mixBlendMode,
    opacity: s.opacity,
  };
});
```

This is visible stack evidence. `z-index` alone is not paint order: stacking contexts can make two identical numbers behave differently.

## Check element and pseudo-element layers

Gradients, noise, glows, masks and hairlines often live on `::before` or `::after`.

Inspect all three:

```js
const PROPS = [
  'backgroundImage', 'backgroundColor', 'filter', 'backdropFilter',
  'mixBlendMode', 'maskImage', 'boxShadow', 'opacity', 'transform'
];

function readLayer(el, pseudo = null) {
  const s = getComputedStyle(el, pseudo);
  const out = {};
  for (const p of PROPS) {
    const v = p === 'maskImage' ? (s.maskImage || s.webkitMaskImage) : s[p];
    if (v && v !== 'none' && v !== 'normal') out[p] = String(v).slice(0, 300);
  }
  return out;
}
```

Do not blindly discard `opacity: 1`, `transform: none` or `blur(0)` before you understand the state. They may be idle animation values and irrelevant, but they may also be the current endpoint of the effect the user asked about.

Filter noise after inspecting context, not before.

## Inspect stacking relationships

For each candidate layer, record:

- geometry;
- positioning mode;
- stacking context triggers (`position` + `z-index`, `transform`, `opacity < 1`, `filter`, `isolation`, etc.);
- clipping / overflow ancestors;
- masks;
- blend mode;
- pseudo-element ownership.

The useful explanation is relational:

> blurred color layer below → frosted translucent panel above → text/content above both

not:

> `z-index: 0`, `z-index: 1`, `z-index: 2`

unless those numbers genuinely explain the stack.

## Search the page when the region is unknown

A wider scan can locate likely effect layers:

```js
const hits = [];
for (const el of document.querySelectorAll('*')) {
  const r = el.getBoundingClientRect();
  for (const pseudo of [null, '::before', '::after']) {
    const found = readLayer(el, pseudo);
    if (!Object.keys(found).length) continue;
    hits.push({
      tag: el.tagName.toLowerCase(),
      pseudo: pseudo ?? 'element',
      cls: (el.className?.toString?.() ?? '').slice(0, 90),
      box: `${Math.round(r.width)}x${Math.round(r.height)} @ ${Math.round(r.x)},${Math.round(r.y)}`,
      found,
    });
  }
}
hits;
```

Treat it as candidate discovery, not the final answer.

## Generated values are patterns

A long gradient stop list or many repeated animation values may be compiled output from an easing helper or interpolation routine.

Do not transcribe twenty stops when the useful explanation is:

- a multi-stop easing gradient;
- a repeated cascade;
- a generated opacity ramp;
- a shared motion curve.

Give the first/last values and the relationship when those values help anchor the pattern.

## When CSS is not the effect

If visible pixels are present but the CSS layer search does not explain them, inspect media/rendering elements:

```js
[...document.querySelectorAll('canvas, svg, video, img')].map(el => {
  const r = el.getBoundingClientRect();
  return {
    tag: el.tagName.toLowerCase(),
    box: `${Math.round(r.width)}x${Math.round(r.height)} @ ${Math.round(r.x)},${Math.round(r.y)}`,
    src: (el.currentSrc || el.getAttribute('src') || '').slice(0, 120),
  };
});
```

For canvas, identifying a WebGL/WebGPU/2D context may narrow the mechanism, but do not invent a shader implementation from appearance alone.

For SVG, inspect masks, gradients and filter primitives directly.

## Is it animated?

`document.getAnimations()` can reveal active or retained Web Animations / CSS animation objects:

```js
[...document.getAnimations()].map(a => ({
  target: a.effect?.target?.tagName?.toLowerCase(),
  cls: (a.effect?.target?.className?.toString?.() ?? '').slice(0, 60),
  state: a.playState,
  duration: a.effect?.getTiming?.().duration,
  easing: a.effect?.getTiming?.().easing,
}));
```

A quiet result does not prove the page never animated. A one-shot transition may already be finished or may require a state change.

If motion matters, reproduce the relevant state or reload deliberately and observe the transition. Do not infer timing from a still frame.

## Report the effect

For each layer:

- **Layer / relation** — what is above/below or clipped by what;
- **Mechanism** — gradient, mask, blur, backdrop blur, raster, SVG filter, canvas, etc.;
- **Evidence** — computed/source/raster observation;
- **Perceptual job** — wash, separation, depth, diffusion, focus, edge softening;
- **Tier** — measured / derived / inferred.

If the stack cannot be resolved because a stylesheet, canvas or cross-origin asset is opaque, stop there honestly.
