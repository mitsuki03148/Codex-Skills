# Animations

Interruptibility, tactile feedback, theme changes and motion restraint.

Staged entrances and exits live in [enter-exit.md](enter-exit.md); icon swaps in [icon-transitions.md](icon-transitions.md).

## Motion has four jobs

Most UI motion should serve one of these:

1. **Causality** — show what action caused what change.
2. **Continuity** — preserve object identity across states.
3. **Orientation** — show where something came from or went.
4. **Feedback** — acknowledge input.

If an animation serves none of them, it is probably decoration.

Decoration can still be legitimate in rare expressive moments, but it should not become the default interaction language.

## Interruptible interactive motion

Users change intent mid-interaction.

CSS transitions and retargetable motion systems are good defaults for:
- hover;
- press;
- toggle;
- open / close;
- selection;
- drag-related states.

Keyframes fit one-shot timelines such as a loader or a deliberate staged reveal.

Do not choose keyframes for an interactive element simply because the code is shorter.

## Press feedback

Press feedback can be:
- small scale;
- opacity;
- local value / color shift;
- slight translation;
- native platform highlight;
- haptic feedback.

`scale(0.96)` is a usable tactile recipe for some button styles, not a universal rule.

A quiet starting range for scale-based press feedback is approximately `0.97–0.99` for ordinary controls. Stronger compression can suit chunky game-like controls where the material supports it.

Do not stack scale + shadow collapse + color flash + haptic unless the control is intentionally physical.

## High-frequency interactions

Repeated interactions carry the highest attention tax.

For row hovers, keyboard-driven controls, tabs, common toggles and frequent toolbar actions:
- instant response is often best;
- otherwise keep motion brief and low-amplitude;
- avoid blur, bounce and staged sequences.

The fiftieth use matters more than the first demo.

## First render

A default state should not accidentally animate merely because the component mounted.

Use `initial={false}` or equivalent when the first render should already be settled.

Do not disable initial motion where the first reveal itself is intentionally part of the experience.

## Theme switching

Theme changes often touch color, background, border and shadow across the whole interface.

If the theme switch is meant to be instant, suppress accidental transitions during the swap.

If the product intentionally animates the environmental change, design that as one coordinated scene transition. Do not let hundreds of unrelated component transitions fire independently.

## Ambient motion

Ambient motion is allowed to exist without being an event.

Good ambient motion:
- low amplitude;
- low frequency;
- interruptible where interaction takes over;
- quiet enough to ignore;
- does not keep resetting or announcing itself.

A tree, light, companion or background can move without collecting attention tax.

## Motion is not the only state signal

Every important change remains legible when motion does not run.

Keep a static cue:
- color;
- icon;
- label;
- shape;
- position;
- content.

Accessibility owns the formal reduced-motion requirement; this skill owns the visual completeness of the no-motion state.

## Exact properties only

Do not use `transition: all`.

Name the properties that change:

```css
.button {
  transition-property: transform, background-color;
  transition-duration: 120ms;
  transition-timing-function: ease-out;
}
```

The exact duration and curve should follow the project's motion language unless a component has a specific reason to differ.

## Avoid animation by habit

Common unnecessary motion:
- every card lifting on hover;
- every icon blurring on swap;
- every section fading on scroll;
- every modal bouncing;
- every button shrinking;
- every navigation change replaying an entrance.

Polish can be the decision not to animate.

## Verification

Test:
- normal speed first;
- rapid reversal;
- repeated use;
- first load;
- large / slow spatial movements;
- keyboard activation;
- reduced motion;
- theme switch;
- ambient motion left running for several minutes.

Slow motion is a diagnostic lens, not the experience to optimize for.
