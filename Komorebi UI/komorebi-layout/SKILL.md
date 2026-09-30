---
name: komorebi-layout
description: Helps with grouping, alignment, reading order, progressive disclosure, responsive composition and mixed English / Traditional Chinese / Japanese layouts that feel clear, calm and spatially intentional.
---

# Layout

Position, spacing, alignment and empty space carry hierarchy before a word is read.

A strong layout does two things at once:

- structure is easy to understand;
- the composition still has air, rhythm and a sense of place.

Do not confuse visual order with making every object equally boxed, equally centred or perfectly grid-like.

Write every fix in the project's styling system. Numeric values in this skill are starting points, not aesthetic laws. Preserve deliberate platform chrome, dense professional tools and project tokens when they still pass the stress tests.

Hit areas and focus behavior belong to `komorebi-accessibility`. Radius, shadows and animation belong to `komorebi-ui`. Line length and text spacing belong to `komorebi-typography`. Thumb / finger reach, grip, regrip and attention-to-action motor flow belong to `komorebi-mobile-ux`.

## Structure first, composition second

First make ownership, reading order, interaction and grouping correct. Then compose.

Structural alignment should be reliable. Visual composition may use deliberate offset, asymmetry, overlap, depth or empty space when those choices make the hierarchy clearer or the place feel more alive.

A layout is not improved merely because more edges line up.

## Group with space before containers

Negative space is the first grouping tool.

Background shapes and cards come next when a group genuinely needs a surface, interaction boundary, drag object or material identity.

Separator lines come last, mainly where density makes space expensive.

The gap between groups should be clearly larger than the gap within a group, but do not treat a fixed 2× ratio as a law. The eye only needs the relationship to be unmistakable.

See [grouping-and-alignment.md](grouping-and-alignment.md).

## Empty space is part of the layout

Do not treat every unused region as unfinished.

Empty space can:

- separate unrelated thoughts;
- create a pause before an important object;
- protect a focal image or sentence;
- make a room feel inhabitable rather than packed;
- create anticipation before the next section.

If a space has a compositional job, filling it is a regression.

## Keep controls legible as controls

Interactive elements need an affordance, but that affordance does not always require a button-shaped container.

A control can read through:

- a surface, border or underline;
- a stable toolbar / footer / control zone;
- icon + label treatment;
- consistent placement;
- interaction feedback;
- a familiar platform convention.

Do not make static content look clickable, and do not hide real actions inside typography that reads as ordinary prose.

## Align structurally, adjust optically

Use a small set of structural alignment edges for scanning and flow.

Then inspect optical alignment. Icons, CJK glyph blocks, illustrations and irregular silhouettes can look misaligned even when their bounding boxes are mathematically equal.

A deliberate offset is allowed when it improves optical balance.

An accidental stray edge is noise. An intentional asymmetry is composition.

## Balance does not require symmetry

A calm layout can be asymmetric.

Balance visual weight using:

- scale;
- contrast;
- density;
- empty space;
- image mass;
- text mass;
- distance from the focal point.

Do not mirror or centre everything merely to make the composition feel safe.

## Reading order follows language and meaning

For normal horizontal EN / Traditional Chinese / Japanese interfaces, reading generally moves top-to-bottom and inline-start to inline-end.

Use semantic DOM order and logical CSS properties so the layout survives localization and RTL.

But visual importance does not always mean “top-left”. A focal subject, centred scene, room composition or editorial image can own the visual centre while the semantic reading order remains correct.

For vertical Chinese or Japanese, treat the writing mode as a different composition, not a rotated horizontal layout.

## Visual placement and physical reach are separate maps

A control can sit in the right visual place and still be expensive to operate on a phone or held tablet.

When the surface contains repeated touch actions, do not finalize placement from visual hierarchy alone. Route the same flow through `komorebi-mobile-ux` to check the relevant hand / grip / device configuration, regrip cost and attention-to-action path.

Do not move everything to the bottom merely because it is easier to reach. Layout still owns meaning, reading order and composition; mobile ergonomics adds physical evidence rather than a universal placement law.

## Priority without shouting

The first screenful should make the important things easy to find, but not everything needs one oversized “primary” object.

Use a dominant action when the product truly has one dominant next step.

When two or more choices are genuinely peers, let them remain peers. Do not create fake hierarchy just to satisfy a one-primary-action rule.

Secondary information can recede through space, grouping and placement before color or size is increased.

## Hint at hidden content without over-explaining

Progressive disclosure needs enough evidence that more exists.

Possible cues include:

- a disclosure control;
- a partial next item;
- clipped continuation;
- a subtle edge fade;
- a familiar scroll affordance;
- spatial continuation;
- a short label such as “Show 12 more”.

Use the quietest cue that remains discoverable.

Do not add a loud chevron, badge and animation when one cue already does the job.

## Breathing room between targets

Where no density system exists, these remain useful starting points:

- about `12px` between adjacent bordered / filled controls;
- about `24px` around borderless text- and icon-only controls.

They are not a visual style. Compact layouts can use less where hit areas stay distinct; spacious layouts can use more where the extra air strengthens grouping.

See [spacing-and-adaptivity.md](spacing-and-adaptivity.md).

## Inset controls from physical edges

In content layouts, keep controls inside margins and safe areas.

Edge-to-edge actions are valid when they are deliberate platform chrome and remain distinguishable from system UI.

Do not use the viewport edge merely because it creates a stronger-looking button.

## Content can bleed; meaning still needs a place

Backgrounds and media may extend to viewport edges.

Text, controls and focal content usually need a stable compositional relationship to safe areas and margins.

When text overlays an image, protect both:

- do not cover the subject's face, hands or important detail;
- look for naturally quiet image regions;
- add a scrim only when composition alone cannot preserve readability;
- do not crop away the part that gives the image meaning.

## Layer the scene

Treat persistent spaces as layers rather than one flat stack:

1. environment / background;
2. content / subject;
3. controls;
4. temporary feedback or system state.

A background can be alive without asking for attention. Controls should not permanently sit on top of the focal subject when they can appear only when needed.

## Hold structure until it breaks

Breakpoints come from content, not device presets.

Keep the expanded composition while it genuinely fits. Collapse when the content or hierarchy stops working, not because a library happens to define `768px`.

Prefer container queries for component-level adaptation.

## Plan for EN / Traditional Chinese / Japanese

Do not budget localization with one expansion percentage.

Test real content in every supported language where the component matters.

English may grow horizontally. Traditional Chinese and Japanese may be shorter in character count but denser, break at different punctuation, or grow vertically because a line can wrap earlier.

Avoid fixed widths and heights on text containers.

Use the same semantic hierarchy across locales, while allowing each language's typography to change the resulting geometry.

## Preserve continuity when adapting

Responsive layout should preserve identity where possible.

Do not rebuild the whole composition at every breakpoint if the same objects can reflow, stack or change relationship.

The user should still recognize “the same place” after resizing, localization or larger text.

## Before you finish

| Mistake | Fix |
| --- | --- |
| Every group becomes a card | Remove surfaces that space and placement already explain |
| Fixed 2× spacing treated as aesthetic law | Keep a clear hierarchy of gaps, then tune optically |
| Every object forced to one shared edge | Keep structural edges; allow intentional optical offsets |
| Everything centred to feel balanced | Balance visual weight instead of forcing symmetry |
| One giant CTA invented for peer choices | Preserve true peer hierarchy |
| Hidden content gets three affordances | Keep the quietest cue that remains discoverable |
| Decorative empty space filled because it looks unused | Keep it when it carries pause, focus or atmosphere |
| Text sits on the busy part of an image | Recompose, crop, move text or add the lightest readable treatment |
| EN fixture used to size every locale | Test EN / zh-Hant / ja with real strings and wrapping |
| Breakpoints copied from device presets | Break where the composition stops fitting |
| Responsive variant feels like a different product | Preserve object identity and relationships where possible |
| `margin-left` / `padding-right` in localizable UI | Use logical properties unless the geometry is truly physical |

## Reporting

**Severity.** `HIGH` blocks content or an action, destroys reading order, or makes an important state unreachable at a supported viewport. `MEDIUM` harms hierarchy, grouping, discoverability, localization or adaptability. `LOW` is isolated compositional polish.

**Verification.** Without a browser: inspect DOM order, logical properties, fixed dimensions, container / media queries and the hierarchy of spacing. With one: test supported widths, 200% zoom, larger text, EN / zh-Hant / ja, RTL where supported, and any meaningful image crops. Report every check you could not run as `Not verified`.

**Format.** Group findings under the principle each violates, ordered by severity, one row per root cause listing every location it appears in:

| Severity | Location | Before | After | Why |
| --- | --- | --- | --- | --- |

`Location` is `path/to/file:line`. `Why` names the principle and the user impact.

End with `Block` when any `HIGH` remains, `Approve` otherwise. Never `Approve` coverage you did not inspect. With nothing to report, state "No actionable layout findings" and report verification.
