# Scenario axes

The menu used by step 2 of [SKILL.md](SKILL.md).

Each axis has a cue. The axis stays only when the component contract can genuinely produce that kind of variation.

An axis that stays contributes the scenarios below plus any real value from the project that is obviously more demanding.

Do not multiply every axis together. After the single-axis cases, choose only a few high-risk seam combinations.

## Baseline

**Cue: always.**

Render one representative normal case first.

The baseline is not a gold-standard design. It is the control case that makes stress-induced change visible.

## Content length

**Cue: the component renders text it does not fully author.** User input, CMS content, API data or translations.

| Scenario | What it catches |
| --- | --- |
| Empty string, where valid | Collapsed boxes, missing fallback, placeholder-only state |
| Short / one-word value | Over-padded badges or controls that assume more content |
| Typical content | Baseline behavior |
| Long wrapping content | Multi-line growth, line-height, fixed-height assumptions |
| Long unbreakable value, only where valid | URL / identifier overflow and missing break strategy |

Breaks usually land in `komorebi-typography`, `komorebi-layout` or `better-writing` depending on the cause.

## Language and script

**Cue: text can vary by locale or user / external data.**

Use realistic strings rather than transliterated filler.

| Scenario | What it catches |
| --- | --- |
| English | Horizontal growth, Latin wrapping and control width |
| Traditional Chinese (`zh-Hant`) | Dense glyph blocks, punctuation, vertical rhythm |
| Japanese (`ja`) | Kana / kanji rhythm, long katakana, CJK line breaking |
| Mixed Latin + CJK | Baseline mismatch, spacing seams, number / product-name wrapping |
| RTL locale, when supported | Mirroring, punctuation and directional layout |
| Emoji / diacritics, when external text allows them | Clipping, line-box assumptions, grapheme truncation |

Typography breaks land in `komorebi-typography`; spatial mirroring and container behavior land in `komorebi-layout`.

## Quantity

**Cue: the component repeats over items.** Lists, tables, grids, tags, chips, avatar groups.

| Scenario | What it catches |
| --- | --- |
| Zero items | Blank region, missing empty state |
| One item | Layouts designed only around plural content |
| Realistic count | Baseline |
| High but plausible count | Wrapping, scrolling, pagination, sticky behavior |

Prefer a plausible production high-water mark over an arbitrary 10× multiplier when the domain provides one.

Zero-state copy can land in `better-writing`; spatial behavior usually lands in `komorebi-layout`.

## Container

**Cue: always.** Components live inside containers they do not fully control.

Render fixed containers together on the harness page.

| Scenario | What it catches |
| --- | --- |
| Narrow, around 320px where relevant | Clipping, escape, horizontal scroll |
| Squeezed by sibling | Min-content blowout, refusal to shrink |
| Representative / normal width | Baseline |
| Very wide | Unbounded measure, stretched controls, lost grouping |

Use the component's actual supported environment where a smaller or larger bound is known.

Breaks usually land in `komorebi-layout`.

## State

**Cue: the component exposes the state through props or supported local interaction.**

| Scenario | What it catches |
| --- | --- |
| Loading | Missing skeleton space, inaccessible busy state, unstable geometry |
| Empty | Content region with no meaning |
| Error | Long recovery copy, color-only failure, displaced actions |
| Disabled | Contrast, misleading affordance |
| Selected / active | State collision with emphasis or layout |
| Validation state | Error copy growth, icon / label collision |

Only render states the real component owns.

Accessibility failures land in `komorebi-accessibility`; visual state styling may land in `komorebi-ui`; geometry in `komorebi-layout`.

## Interaction and transition

**Cue: the component owns a transition or disclosure whose movement changes geometry or visibility.**

| Scenario | What it catches |
| --- | --- |
| Collapsed → expanded | Reflow, clipping, hidden actions |
| Loading → content | Layout shift, late overflow |
| Validation → error | Sudden growth and action displacement |
| Placeholder → media | Crop / aspect shift |

Do not infer transition quality from static side-by-side states. Run the sequence only when it can be exercised without inventing test-only component behavior.

## Media

**Cue: the component accepts an image, illustration, avatar, video poster or other visual asset.**

| Scenario | What it catches |
| --- | --- |
| Missing / unavailable media | Broken placeholder or collapsed geometry |
| Portrait asset | Bad object-fit / crop |
| Landscape asset | Excess crop or stretched frame |
| Focal subject near an edge | Centre-crop destroying meaningful content |
| Transparent / irregular silhouette, where supported | Unexpected background seams or bounds |

Composition and crop breaks usually land in `komorebi-layout`; surface treatment can land in `komorebi-ui`; contrast over media in `komorebi-colors` / `komorebi-accessibility`.

## Environment

**Cue: the project supports the mode or user setting.**

These are real viewing modes. Use the production mechanism or let the viewer toggle them.

| Scenario | What it catches |
| --- | --- |
| Dark appearance | Theme token, contrast and image-treatment failures |
| 200% zoom / large text | Reflow, clipping, unreachable controls |
| Reduced motion | Meaning that disappears without motion |
| Increased contrast, where supported | Token / border / focus regressions |
| Keyboard open / safe-area change, where relevant | Covered actions, clipped inputs |

Do not recreate environment tokens inside the harness.

## High-risk seams

After the applicable single-axis cases, choose two to four combinations whose interaction is plausible and risky.

Good examples:

- narrow container × Japanese long label;
- narrow container × many tags;
- long zh-Hant error copy × validation state;
- large text × peer action row;
- English overlay × portrait image crop;
- dark appearance × translucent overlay over media;
- mixed-script title × selected state.

Bad approach: generate every combination of every axis.

The seam case is useful only when it tests a relationship the single-axis rows cannot expose.
