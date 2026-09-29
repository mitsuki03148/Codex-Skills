# Icon transitions

How icons change by state without turning a small control into a visual event.

Icon weight, color and direction live in [icons.md](icons.md).

## Default to the smallest transition that explains the change

Most icon state changes need no choreography.

Start here, in order:

1. instant swap;
2. opacity cross-fade;
3. small scale + opacity;
4. rotation or morph when geometry naturally supports it;
5. blur or more expressive transformation only when the moment genuinely benefits.

Do not start from `scale(0.25)` plus `blur(4px)`. That recipe is highly visible and quickly becomes attention tax on repeated controls.

## Preserve identity

If the old and new icons represent two states of the same control, the transition should feel like one object changing state.

Examples:
- play ↔ pause: instant swap, morph or quiet cross-fade;
- bookmark outline ↔ filled: fill / opacity change;
- disclosure chevron: rotation;
- visibility eye ↔ eye-off: swap or morph.

A state transition that makes the icon disappear into a tiny blurred dot before returning often destroys continuity more than it helps.

## CSS cross-fade

A simple cross-fade is a good default when both glyphs must overlap.

```css
.icon-state {
  position: absolute;
  inset: 0;
  transition-property: opacity, transform;
  transition-duration: 120ms;
  transition-timing-function: ease-out;
}

.icon-state[data-active="false"] {
  opacity: 0;
  transform: scale(0.92);
}
```

The exact values should match the project's motion language. The important constraints are:
- brief;
- interruptible;
- small amplitude;
- static state remains clear.

## Motion library

Use the project's installed motion library only when it already exists or when the transition genuinely needs orchestration.

Do not add a dependency just for an icon swap.

Follow nearby import conventions (`motion/react` vs `framer-motion`) rather than mixing packages.

## When blur belongs

Blur can work for:
- a magical / atmospheric transformation;
- an infrequent success state;
- a deliberately soft material transition.

Avoid it for:
- every hover;
- tabs;
- repeated toggles;
- common toolbar state changes.

Blur is visually expensive even when computationally cheap.

## When not to animate

Do not animate:
- static navigation icons;
- utility symbols that change frequently;
- icon changes where the state is already obvious and motion adds no causality;
- reduced-motion modes where the effect is not essential.

## First render

Do not animate a default icon merely because the component mounted.

Where a motion library would replay the state-change entrance on mount, use the library's initial-state controls to start settled.

Keep an intentional first reveal only when it is part of the composition.

## Verification

Test:
- rapid toggling;
- reversal mid-transition;
- first render;
- keyboard activation;
- reduced motion;
- the fiftieth repeated use.

If the transition becomes the thing you notice, it is probably too loud for a utility icon.
