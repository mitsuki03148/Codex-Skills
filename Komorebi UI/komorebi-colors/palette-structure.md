# Palette structure

What a color system is made of before exact values exist.

For computing values see [palette-generation.md](palette-generation.md); for naming see [token-naming.md](token-naming.md).

## Separate system color from world color

The semantic interface palette and the visual world do not need identical boundaries.

### Semantic UI palette

Usually contains:

- neutral / environmental roles;
- one main accent family;
- only the status families the product actually uses.

### World / illustrative palette

May contain:

- character colors;
- room / environment colors;
- material colors;
- decorative or seasonal accents;
- chart / category colors when the product genuinely needs them.

Do not automatically promote every illustrative swatch into a semantic token.

## Neutrals carry atmosphere

Neutrals are not merely “colors with no personality”. They define the field behind almost everything else.

A neutral system may be:

- true gray;
- warm ivory / paper;
- cool gray / mist;
- faint green-gray;
- faint blue-gray;
- muted brown-gray.

Keep chroma low enough that the field remains supporting.

A tinted neutral should feel like atmosphere, not like a second accent.

## Semantic role inventory

A practical system often needs roles such as:

| Group | Roles |
| --- | --- |
| Surfaces | page / environment, surface, raised, sunken, scrim |
| Text | primary, secondary, disabled, inverse, on-accent |
| Borders | subtle, default, strong, focus ring, separator |
| Accent | subtle surface, border, solid, hover / active, text |
| Status | per shipped state: subtle surface, border, solid, text |

Add only roles the product actually needs.

A role can share the same value as another role today while keeping a separate semantic name when the responsibilities may diverge later.

## Framework steps are containers, not aesthetic truth

Tailwind and Radix provide useful conventions, but the project should not generate unused steps merely to fill the framework.

If the project already uses a full ramp convention, preserve it for consistency.

For a new compact system, fewer explicit primitives can be cleaner when each one maps to a real decision.

## Surfaces can vary by temperature as well as lightness

Depth does not have to mean “same hue, darker by 4%”.

A material system may use subtle temperature or hue movement to distinguish:

- page vs paper card;
- daylight vs shadow;
- raised vs sunken material;
- room atmosphere vs control surface.

Keep the shifts small enough that the hierarchy still reads as one environment.

## Accent is a light, not a flood

A single accent family is often enough for interface semantics.

Use it where attention or state genuinely benefits. Large persistent areas of accent color can make the accent stop feeling special.

A second accent hue earns its place when it creates a real distinction that cannot be expressed more clearly through hierarchy, shape, label or one existing ramp.

## Status colors

Convention constrains status colors, but convention varies by locale and domain.

Do not infer gain / loss, danger or success from language alone. Verify the actual market or product convention.

Every status should remain distinct from the main accent in the context where they can appear together.

Status color is not the only carrier of state; pair it with label, icon or shape where meaning matters.

## Dark appearance

Dark mode is a second composition, not an inverted screenshot.

Preserve role relationships:

- page remains the quietest field;
- raised / sunken surfaces remain distinguishable;
- primary text remains primary;
- accent remains accent without turning neon;
- atmospheric tint remains present without muddying the dark field.

The dark system may need different chroma and temperature trajectories than the light system.

## Audit an existing palette

Before restructuring:

1. inventory literals and tokens;
2. group them by actual role and visual family;
3. identify near-duplicates;
4. distinguish intentional material variation from accidental drift;
5. locate semantic values used outside their role;
6. identify unused or unreachable tokens;
7. report the inventory before consolidation.

Do not average near-duplicates automatically. One may be a deliberate optical correction or material state.

Consolidation changes rendered output across many screens and should remain a proposal until approved.
