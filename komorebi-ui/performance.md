# Performance

Transition specificity, compositor-friendly motion and performance hints.

Performance exists to protect interaction feel. It is not a reason to pre-optimise every visual element.

## Transition only what changes

Avoid `transition: all`.

Name the actual properties that change.

```css
.button {
  transition-property: transform, background-color;
  transition-duration: 120ms;
  transition-timing-function: ease-out;
}
```

Explicit transitions:
- reduce accidental motion;
- make review easier;
- avoid surprising layout / color interpolation;
- document the intended interaction.

## Prefer low-cost motion where it serves the design

Transform and opacity are usually the safest tools for frequent motion because browsers can commonly composite them efficiently.

Filter, shadow, backdrop blur and large-area effects can be more expensive and should earn their place.

Do not choose a compositor-friendly effect merely because it is cheap if it is visually too loud.

Performance and attention cost are different budgets.

## `will-change` is a diagnosis tool

Do not add `will-change` as a design token or default class.

Use it when:
- the animation is real and repeated;
- profiling or direct observation shows promotion / first-frame stutter;
- the hinted property can benefit.

Typical useful cases:
- `transform`;
- `opacity`.

`filter` support and cost vary by effect and browser; verify rather than assuming every filter becomes cheap.

Never use `will-change: all`.

## Avoid permanent layer promotion

Every promoted layer uses memory.

A page full of permanently promoted cards can cost more than the animation it tried to improve.

Where possible:
- add the hint only around the animated lifecycle;
- remove it after the interaction;
- let the browser optimize ordinary static content.

## Measure real bottlenecks

Do not “fix performance” because an animation looks sophisticated.

First ask what actually failed:
- dropped frames;
- input delay;
- paint cost;
- layout thrash;
- memory;
- first-frame hitch.

Then fix that failure.

A visually calm interface with no observed performance problem does not need GPU folklore added to it.

## Large-area effects

Be especially cautious with:
- backdrop blur;
- large animated shadows;
- large filters;
- full-screen gradients that animate continuously;
- many independent ambient layers.

If the atmosphere matters, prefer fewer larger compositional decisions over dozens of small animated effects.

## Review

Check:
- no `transition: all`;
- motion properties are explicit;
- no blanket `will-change`;
- expensive effects are justified by the visual role;
- performance claims come from observation or profiling rather than assumption;
- optimization does not make the interaction louder than the problem it solved.
