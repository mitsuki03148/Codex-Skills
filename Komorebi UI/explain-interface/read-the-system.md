# Reading the whole system

Use this when the question is how an interface is built in general rather than how one named effect works.

The output is a map of observed systems and fingerprints, not a design review.

## Read the stack with confidence labels

Inspect resource URLs, DOM markers and runtime globals when available.

For each framework / styling / component-library claim, report:

- the fingerprint;
- its strength;
- whether it identifies the tool or only resembles it.

A `false` fingerprint means “not detected by this probe”, not “absent”.

## Read tokens before leaf values

Custom properties often reveal the system's own vocabulary.

Group tokens by prefix and relationship:

- primitives;
- semantic roles;
- component exceptions;
- theme overrides.

If one token references another, that dependency is measured source evidence. Calling the tiers “primitive” and “semantic” may be a derived mapping unless the project names them that way.

Do not judge the token architecture here. `komorebi-colors` owns that.

## Read typography as roles and distributions

Collect rendered text styles or authored tokens and group repeated combinations of:

- family;
- size;
- weight;
- line-height;
- tracking;
- language-specific overrides.

A cluster of repeated sizes is measured.

A consistent ratio between sizes can suggest a scale, but do not claim a modular scale unless the tokens/source establish one.

For EN / Traditional Chinese / Japanese systems, inspect `lang`-specific fonts, line-height, CJK line-breaking, East Asian variants and vertical-writing rules where present.

## Read spacing as a distribution

Collect repeated padding, margin and gap values.

Useful statements:

- “8, 12, 16 and 24px account for most measured gaps.”
- “Many values are divisible by 4.”

Less defensible without source:

- “The design system uses a 4px base grid.”

That conclusion is an inference; label it if it helps.

Do not apply `komorebi-layout` review heuristics such as a fixed group-gap ratio inside an explanation. If the user asks whether the spacing is good, that is a review question.

## Read surfaces without scoring them

Inventory recurring:

- radii;
- borders/rings;
- shadows;
- translucent surfaces;
- backdrop filters;
- image edge treatments.

Counts show consistency or diversity; they do not by themselves prove quality or chaos.

“One shadow recipe appears on 38 elements” is evidence.

“Nine recipes means everyone invented their own elevation” is judgement and intent speculation.

## Read motion as relationships

Collect transition properties, durations and timing functions plus observed entrance/exit behavior.

Group repeated patterns rather than listing every element.

Distinguish:

- high-frequency interaction feedback;
- state transitions;
- page/section entrances;
- ambient motion;
- one-shot effects.

If the live state never triggers a transition, keep the claim source-level.

## Read breakpoints and responsive behavior

Collect declared media/container queries and then, if possible, inspect more than one viewport.

A breakpoint value that matches a framework default is a fingerprint, not proof it was unconsidered.

Report:

- declared values;
- which values actually change the named surface;
- container vs viewport adaptation;
- geometry differences between visited states.

Do not infer design intent from the numbers alone.

## Read images, fonts and delivery

Inspect:

- responsive image `srcset` / `<picture>` behavior;
- image optimization routes;
- raster vs SVG use;
- self-hosted vs external fonts;
- variable-font ranges;
- preload/preconnect where visible;
- wide-gamut or modern-format enhancements.

Do not turn delivery choices into a performance verdict unless the user asks for review.

## Read a second state when the answer depends on it

A system cannot always be inferred from one viewport and one theme.

Choose only the second states that matter to the question, for example:

- narrow viewport;
- dark appearance;
- focus-visible state;
- Japanese or Traditional Chinese locale;
- expanded / selected state.

Do not perform a ritual checklist when those states are irrelevant.

## Explain the system in its own language

Prefer the project's existing names when source gives them.

If source calls a token `--surface-raised`, use that rather than renaming it into our own taxonomy.

When our model helps explain a pattern, mark it as interpretation:

> “This behaves like a semantic token layer: components consume `--color-text-*`, which point to lower-level values.”

That keeps explanation separate from relabelling the project.

## Close with unknowns

Name evidence gaps such as:

- unreadable cross-origin stylesheet;
- unvisited responsive state;
- runtime-generated style not exposed;
- framework fingerprint without source confirmation;
- locale not available;
- canvas/shader internals.

Unknown is part of the system map.
