# Hit areas

Conformance-sized targets, larger usability targets, expansion and collision.

## Separate the WCAG floor from usability guidance

WCAG 2.2 SC 2.5.8 Target Size (Minimum), Level AA, uses a 24×24 CSS-pixel minimum target size with defined exceptions.

A target smaller than 24×24 may still conform through an applicable exception, including spacing, equivalent control, inline, user-agent control or essential presentation.

Larger targets are often easier to operate:

- around 44×44 CSS px is a strong touch-oriented usability target;
- platform design systems may recommend their own sizes;
- dense desktop tools may use smaller visible controls while still maintaining usable hit geometry.

Do not report "under 44px" as a WCAG AA failure.

## Visible size and hit size can differ

A visually small icon can have a larger interactive box.

Prefer real box geometry when the layout can afford it:

```css
.icon-button {
  min-inline-size: 44px;
  min-block-size: 44px;
  display: inline-grid;
  place-items: center;
}
```

When the composition needs a smaller visible footprint, a pseudo-element or wrapping label can expand the interactive target.

Do not put pseudo-elements on replaced inputs and expect consistent behavior across browsers; expand the wrapping interactive element instead.

## Spacing exception

WCAG's spacing exception can allow an undersized target when sufficient space separates it from other targets.

Evaluate the actual geometry rather than applying one memorized gap to every shape.

The goal is that the specified target-sized circles around undersized targets do not intersect other targets in the way the criterion prohibits.

## Prevent ambiguous overlap

Extended hit areas should not create two controls that both respond in the same physical region.

Even when a conformance calculation passes, overlapping pointer activation is a usability defect because the user cannot reliably predict which action will fire.

When targets are close:

- shrink the expansion;
- increase spacing;
- enlarge the visible control;
- combine the interaction if the two regions are actually one action.

## Labels expand useful targets

Checkboxes, radios and similar controls should normally let their visible label activate the same input.

This improves both target size and comprehension without visually enlarging the native glyph.

## Decorative layers

A real DOM layer painted over controls can intercept pointer events.

Decorative glows, scrims or overlays that should never receive input use `pointer-events: none`.

If the decorative DOM node would otherwise enter the accessibility tree and conveys no information, hide it appropriately from assistive technology.

A clickable modal scrim is not decoration; it is part of the interaction and keeps its pointer behavior.

## Touch behavior

Do not disable browser gestures globally to make custom interaction feel cleaner.

`touch-action: none` can remove scrolling and pinch behavior. Use it only on a bounded surface that genuinely implements its own gesture interaction, and verify users retain an accessible way to operate and zoom the surrounding experience.

Do not add `touch-action: manipulation` everywhere as a generic performance or polish rule. Modern browsers do not need it as a universal tap-delay fix, and gesture behavior is part of the user's platform.

Keep native tap feedback unless the project supplies an equally perceivable replacement. Removing `-webkit-tap-highlight-color` purely for visual cleanliness can erase useful touch confirmation.

Gate hover-only styling so touch does not get stuck in a misleading pseudo-hover state.

## Precision is a design cost

Tiny drag handles, narrow hover zones and densely adjacent icon controls demand motor precision.

Where a larger target or simpler action preserves the same product meaning, prefer that before inventing gesture-specific workarounds.
