# Reading a screenshot

A screenshot supports visual reconstruction, not source-code archaeology.

The aim is to separate what the raster genuinely tells you from what merely looks plausible.

## Evidence buckets

| Directly observable in the raster | Derived from raster relationships | Not available from the screenshot alone |
| --- | --- | --- |
| Pixel colors at sampled coordinates | Relative spacing / size ratios | DOM / component structure |
| Visible boundaries and overlaps | Repeated rhythm ratios | Token names and semantic roles |
| Visible text and imagery | Relative lightness / color-family relationships | Framework / styling library |
| Which visible colors recur | Approximate compositional balance | Real breakpoints and hidden responsive states |
| The captured crop | Likely layer order from occlusion | Motion implementation / easing / duration |
| | | Hover, focus, loading, error and other uncaptured states |
| | | Authored CSS values unless independently known |

A sampled pixel is exact for the image file, not automatically for the authored interface.

## Do not manufacture scale

The capture may be:

- device-pixel scaled;
- browser zoomed;
- resized after capture;
- compressed;
- color-managed differently from the source display.

Therefore:

- do not convert screenshot pixels directly into CSS px;
- do not assume body copy is 16px to create a fake scale;
- express spacing, radius, stroke and type size as ratios unless a reliable scale anchor exists.

If the screenshot includes a verified device frame, known asset size or other trustworthy anchor, say what the anchor is before converting.

## Color sampling

Sample stable interior pixels rather than antialiased edges.

Then distinguish:

- **sampled raster color** — exact for that pixel;
- **derived color relationship** — relative lightness / hue family / contrast between stable flat regions;
- **authored color** — unavailable unless source is known.

Compression, transparency, blur, overlays, gradients and color profiles can make the raster differ from the authored token.

For contrast, use `komorebi-colors` once you have defensible foreground/background samples. If text antialiasing or an image background makes the pair unstable, report that limitation rather than one overconfident number.

## Typography: describe visible character, not font identity

From a screenshot you can discuss:

- serif / sans / mono / display character;
- geometric / grotesque / humanist tendencies when visible;
- apparent x-height / density / stroke contrast;
- number of visibly distinct size and weight roles;
- relative type-scale ratios;
- CJK vs Latin optical balance;
- line-height and measure as image-space relationships.

Do not identify an exact typeface from appearance alone unless another source confirms it.

Do not force English typography vocabulary onto CJK where it does not fit.

## Spacing and composition

Look for repeated relationships:

- within-group vs between-group spacing;
- structural vs optical alignment;
- large pauses / negative space;
- focal subject vs supporting text;
- symmetry or asymmetric balance;
- edge relationships;
- visible continuation beyond the crop.

A repeated smallest gap can be used as a ratio unit, but do not automatically name it the design system's base spacing token.

## Surfaces and material

From visible evidence you may describe:

- hard vs soft edges;
- border / ring / shadow cues;
- translucency;
- blur;
- paper-like or glass-like appearance;
- image cutouts vs rectangular media;
- apparent depth relationships.

Whether that appearance comes from CSS, raster texture, SVG, canvas or baked artwork remains unknown.

## Reconstruction recipe

When the user wants to reproduce the look, give a plausible recipe in layers:

1. composition / geometry;
2. surface or image;
3. color/material treatment;
4. typography relationship;
5. depth / edge treatment;
6. optional motion only if another source shows it.

Mark inferred implementation choices as inferred.

Do not present the reconstruction as the original author's code.

## Say what the screenshot hides

Close with the uncaptured parts that matter:

- responsive behavior;
- EN / Traditional Chinese / Japanese variants;
- dark/light appearance;
- hover/focus/active/disabled states;
- keyboard and accessibility behavior;
- motion;
- source tokens and framework.

A live URL or source can answer those. The screenshot cannot.
