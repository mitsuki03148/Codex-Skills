---
name: komorebi-ui
description: Polishes and improves the UI through surface restraint, optical alignment, icon coherence, motion with causality, continuity and performance-aware interaction.
---

# UI polish

Polish is not the amount of visible treatment. It is the feeling that every surface, control, icon and transition belongs exactly where it is.

This skill owns surface treatment, icon language, motion behavior, state polish and the small visual details that make an interface feel settled. It does not own typography, layout structure, color semantics or accessibility.

Keep the project's component library, tokens, density and established motion language. Prefer refinement over replacement.

Text wrapping and font rendering belong to `komorebi-typography`. Hit areas, focus, keyboard support, ARIA and reduced motion belong to `komorebi-accessibility`. Grouping, section spacing, breakpoints and spatial composition belong to `komorebi-layout`. Color roles and contrast measurement belong to `komorebi-colors`.

## Polish should know when to disappear

A polished interface does not constantly advertise its polish.

Before adding a border, card, shadow, animation, blur, icon swap or extra state treatment, ask what job it performs:

- structure;
- affordance;
- state;
- depth;
- causality;
- continuity;
- feedback.

If the same meaning already exists clearly without it, the cheapest improvement may be to remove the treatment.

## Surfaces need a reason

Do not turn every group into a card.

Use a surface when something genuinely needs:

- a material object;
- an interaction boundary;
- elevation;
- containment;
- drag identity;
- a state boundary.

Where space and placement already explain the grouping, leave the area open.

Radius, borders, shadows and image-edge treatment live in [surfaces.md](surfaces.md).

## Concentric radius where the inset is real

For closely nested rounded surfaces with an even visible inset, concentric geometry is a useful construction rule:

`outer radius = inner radius + inset`

It is not a universal radius law. Independent surfaces, asymmetric padding, organic artwork and material layers may need independent optical tuning.

## Optical over geometric alignment

When mathematical centering looks wrong, align optically.

Icons, play triangles, irregular illustrations and mixed CJK / Latin labels may need small visual corrections. Structural alignment belongs to `komorebi-layout`; this skill owns the final optical nudge.

## Depth before shadow

Depth can come from:

- overlap;
- value difference;
- material;
- edge treatment;
- local contrast;
- shadow.

Use the lightest mechanism that makes the relationship clear.

A shadow is not the default replacement for a border. Borders are legitimate structure; shadows are legitimate depth. Neither should be added merely because the surface feels unfinished.

## Motion shows causality

Animate when motion helps the user understand:

- what changed;
- where something came from;
- where it went;
- what object transformed into what;
- what action caused the state change.

Do not animate simply because a property can animate.

High-frequency interactions should be immediate or nearly immediate. Repeated controls must still feel natural on the fiftieth use.

## Continuity before choreography

A transition should respect the state that was already true.

Do not reset an element to a canonical start pose just so a polished animation can play. If a drawer is half-open, reverse from there. If a character or object already occupies a real position, continue from that position.

The previous frame is part of the interface's history.

## Interruptible interactive motion

Use CSS transitions or an equivalent retargetable system for interactive state changes. Users change intent mid-transition.

Keyframes remain appropriate for one-shot sequences whose timeline itself matters.

See [animations.md](animations.md).

## Entrances earn their attention

Staged entrances are for infrequent moments where sequence communicates meaning: a first reveal, a meaningful success, a composed empty state.

Do not stagger routine screens, repeated tabs, list rows, settings panels or every page simply to make them feel designed.

Animate the smallest semantic unit that needs motion. Word-by-word title animation is rare and editorial, not a default.

See [enter-exit.md](enter-exit.md).

## Exits usually recede

The user's attention is moving elsewhere, so exits should normally demand less attention than entries.

But an exit may be immediate when motion adds no information, and spatial when the destination matters.

There is no mandatory `translateY` distance. The correct movement follows the spatial relationship.

## Contextual icon transitions

Most icon state changes need one of:

- instant swap;
- cross-fade;
- small opacity / scale change;
- rotation or morph when the icon's geometry naturally supports it.

Blur and dramatic scale changes are expressive tools, not defaults.

Use the quietest transition that preserves identity and causality. See [icon-transitions.md](icon-transitions.md).

## Icons belong to one optical language

Prefer one coherent icon strategy per surface:

- consistent stroke / fill logic;
- compatible grids;
- compatible corner character;
- similar optical weight.

Match adjacent text optically, but do not force every icon to a numeric stroke formula if the set was designed as a complete system.

Use `currentColor` where state color belongs to CSS. Icon sizing and RTL behavior live in [icons.md](icons.md).

## Press feedback is contextual

A press may use:

- a small scale change;
- opacity;
- local value / color change;
- a slight physical translation;
- platform-native highlight;
- haptic feedback where the platform provides it.

`scale(0.96)` is one recipe, not a law.

Do not make every button visibly shrink. Choose a feedback language that fits the control's material and frequency.

## Ambient motion has an attention budget

Persistent elements may move, breathe or respond without repeatedly asking to be noticed.

A useful test:

**If the user ignores this element for ten minutes, does the space still feel comfortable?**

Ambient movement should be slow, sparse and low-amplitude. Life does not need to prove that it is alive.

## First render should be intentional

Do not accidentally replay state-change motion on page load.

Use `initial={false}` or the equivalent where the initial state should already be settled. Keep a first-load entrance only where the first reveal itself is intentional.

## Theme changes should not smear

A theme switch should normally feel like the environment changed, not like every component independently animated its CSS.

Suppress broad color / shadow transitions during an instantaneous theme flip when the project's theme mechanism needs it. If the product intentionally animates theme changes, treat that as a designed scene transition rather than an accidental cascade.

## Transition only what changes

Name the properties that actually transition. Avoid `transition: all`.

This prevents accidental motion and keeps the interface easier to reason about.

## Performance supports feel

Use compositor-friendly properties where possible, but do not cargo-cult performance hints.

`will-change` is a targeted fix for observed rendering problems, not a polish token. See [performance.md](performance.md).

## Motion restraint

Motion is a budget.

- high-frequency actions: instant or minimal;
- ordinary state changes: brief and causal;
- infrequent narrative moments: may be more expressive;
- ambient motion: sparse and ignorable.

Every state change must still leave a static cue when motion is absent.

## Before you finish

| Mistake | Fix |
| --- | --- |
| Every section becomes a rounded card | Remove surfaces that have no containment or material job |
| Shadow added because a card looks flat | First check overlap, value, material and edge treatment |
| Same radius recipe forced onto independent layers | Use concentric geometry only for true visible insets |
| Every button shrinks on press | Pick feedback appropriate to the control and frequency |
| Icon swaps shrink to a dot and blur by default | Use instant swap or a quiet cross-fade unless expression has a job |
| Every page staggers in | Reserve staged entrances for infrequent meaningful reveals |
| Transition resets from a canonical pose | Continue from the state that is actually on screen |
| Ambient element keeps moving to prove it is alive | Reduce frequency and amplitude; let it be ignored |
| `transition: all` | Name the exact changing properties |
| `will-change` added everywhere | Add only after an observed compositing problem |
| UI polish changes semantic hierarchy | Return that decision to layout, typography, color or accessibility |

## Reporting

**Severity.** `HIGH` breaks an interaction, makes a state unreadable or unreachable, or leaves meaning visible only while motion runs. `MEDIUM` meaningfully harms surface coherence, icon clarity, continuity or interaction feel. `LOW` is isolated polish.

**Verification.** Without a browser: inspect every defined state, motion trigger, duration, easing, transitioned property and surface treatment. With one: walk real states at normal speed first, then slow motion only when needed to diagnose continuity or timing. Test repeated interactions, interruption / reversal, first render and the fiftieth-use feel where relevant. Report every check you could not run as `Not verified`.

**Format.** Group findings under the principle each violates, ordered by severity, one row per root cause listing every location it appears in:

| Severity | Location | Before | After | Why |
| --- | --- | --- | --- | --- |

`Location` is `path/to/file:line`. `Why` names the principle and user impact.

End with `Block` when any `HIGH` remains, `Approve` otherwise. Never `Approve` coverage you did not inspect. With nothing to report, state "No actionable UI-polish findings" and report verification.
