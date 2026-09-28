# Color formats

Which notation to write colors in, how to convert between them and what happens at the edge of a display gamut.

Every other rule in this skill is about rendered color and role. Notation is an implementation choice.

## Choosing a notation

| Notation | Good for | Weakness |
| --- | --- | --- |
| Hex | Compact, universal, common in tools | Hard to reason about perceptually |
| `rgb()` | Familiar, readable alpha | Channels are not perceptual design controls |
| `hsl()` | Familiar hue / saturation model | Lightness is not perceptually uniform |
| `oklch()` | Perceptual editing, controlled lightness / chroma / hue | Support policy and tooling still need project agreement |
| `color(display-p3 ...)` | Wide-gamut enhancement | Needs a deliberate browser / display support strategy |

**Match the project unless migration is the task.** A coherent hex system is better than one stray modern color function nobody else understands.

For a genuinely new system, OKLCH is a strong working representation because lightness and chroma are easier to tune perceptually. It is not a requirement that every emitted token remain written in OKLCH.

## Converting

Convert when:

- the user asks;
- a migration is in scope;
- the project has chosen one notation and this value is a straggler.

Do not convert unrelated files as cleanup.

Preserve:

- CSS keywords such as `currentColor`, `inherit`, `transparent`;
- interpolation method and gradient structure;
- third-party formats that have their own requirements;
- comments and surrounding formatting.

A bulk conversion is a migration because rounding and gamut mapping can change rendered output.

## Gamut

A color can be valid CSS but outside the gamut of a particular display.

Modern CSS can gamut-map out-of-gamut colors rather than making the declaration invalid. That does not mean every display renders the original intended chroma.

When consistent output matters:

- design the base system for the product's minimum supported gamut;
- treat wider-gamut values as enhancement;
- verify adjacent ramp steps remain visually distinct after gamut mapping.

Do not assume “Display P3” means “more beautiful”. A restrained low-chroma palette may gain almost nothing from wider gamut.

## Fallbacks follow the browser matrix

A modern browser matrix may support OKLCH and Display P3 directly. Older browsers may not.

Provide fallback when the supported matrix requires it; do not add dead fallback code to a modern-only product just because the syntax is newer.

Typical progressive enhancement:

```css
.accent {
  background: #6f897d;
}

@media (color-gamut: p3) {
  .accent {
    background: color(display-p3 0.39 0.55 0.46);
  }
}
```

Or feature-gate a modern syntax when the project supports older browsers.

## Modern CSS worth knowing

### `color-mix()`

Useful for derived states and translucent treatments.

Do not let a semantic token become an unreadable chain of mixes. Important palette roles should still be inspectable.

### Relative color syntax

Useful for a small, local adjustment to an existing color.

Avoid multi-step derivation chains where nobody can tell the rendered color without a browser.

### `light-dark()`

Can keep paired appearances together when the project uses `color-scheme` consistently.

It is a representation convenience, not a replacement for designing two appearances.

## Alpha is compositional

A color with alpha is not one color on screen. It becomes a different result on every background.

Use alpha freely for atmosphere, overlays and temporary treatment when the compositing is intentional.

For essential text or state indicators, prefer a stable rendered pair that can actually be verified.
