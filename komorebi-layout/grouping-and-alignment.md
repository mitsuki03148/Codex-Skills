# Grouping and alignment

How space, surfaces, shared edges, visual weight and ordering communicate what belongs together and what matters.

## Group with space before lines

Three common grouping tools, in order of restraint:

1. **Negative space** — the default.
2. **Background shapes / material surfaces** — when a group needs a shared object or interaction boundary.
3. **Separator lines** — when density makes space expensive or explicit row division genuinely helps.

The gap between groups should read clearly larger than the gap within a group. A 2× relationship is a useful debugging heuristic, not a design law.

```css
.field-group { display: flex; flex-direction: column; gap: 8px; }
.form { display: flex; flex-direction: column; gap: 24px; }
```

Where a separator is genuinely needed, keep it quiet. If space already explains the grouping, a line is usually redundant.

## Space can carry meaning

Empty space is not only separation.

It can create:

- pause;
- anticipation;
- protection around a focal subject;
- a threshold between modes;
- a sense that objects belong to a larger place.

Do not normalize all gaps until the layout loses its rhythm.

A page with one sentence may legitimately give most of the page to the space around that sentence.

## Keep controls distinct from content

Interactive elements need a signal, but “signal” does not always mean a filled button.

Possible affordances include:

- background or border;
- underline;
- icon + label;
- stable toolbar / footer placement;
- familiar platform convention;
- hover / focus / press treatment;
- consistent spatial zone.

Do not let a non-clickable badge imitate a button, and do not let a real action disappear into ordinary prose.

## Structural alignment vs optical alignment

Structural alignment supports scanning:

- shared column starts;
- common container edges;
- baseline or row systems;
- consistent indents.

Optical alignment corrects what the eye actually sees.

Examples:

- a circular icon may need to sit slightly outside the text edge;
- a CJK glyph block can feel heavier than adjacent Latin;
- an illustration with an irregular contour may need a small offset;
- punctuation can make a mathematical edge look visually indented.

Do not create dozens of unrelated edges. But do not “fix” a deliberate optical adjustment merely because the bounding boxes differ.

## Asymmetry can be balanced

Symmetry is one way to balance a composition, not the definition of balance.

In an asymmetric layout, compare visual weight:

- large vs small;
- dark vs light;
- dense vs empty;
- image vs text;
- near vs far;
- detailed vs quiet.

A heavy object can be balanced by a larger quiet region rather than another heavy object.

This is especially useful in restrained Japanese-influenced graphic composition, where silence around a focal object can be part of the hierarchy.

## Logical properties, not physical habits

Express direction-dependent position as inline-start / inline-end so localization and RTL can mirror naturally:

| Physical (avoid when directional) | Logical |
| --- | --- |
| `margin-left` | `margin-inline-start` |
| `padding-right` | `padding-inline-end` |
| `left: 0` | `inset-inline-start: 0` |
| `text-align: left` | `text-align: start` |
| `border-right` | `border-inline-end` |

Reserve physical properties for genuinely physical geometry: safe-area hardware, a real image crop, a gesture tied to a physical side, or an illustration that must not mirror.

## Reading order is not identical to visual focal point

For ordinary horizontal EN / zh-Hant / ja interfaces, semantic reading order is top-to-bottom and inline-start to inline-end.

Keep DOM order logical.

The visual focal point may still be centred, offset or image-led.

A large hero object can sit in the middle while the accessible reading order remains sensible. Do not move semantic content around merely to mimic the graphic composition.

For vertical writing, use the correct writing mode and revisit the whole composition.

## Order by actual importance

Do not bury the one thing the user came for under metadata.

But importance can be expressed by more than “put it top-left and make it big”.

Use:

- isolation;
- proximity;
- scale;
- contrast;
- position;
- surrounding empty space.

Within utility rows, identifying content often leads and metadata / actions often trail. In spatial or editorial views, follow the composition that best preserves meaning.

## Do not overload the entry point

The first screenful should orient, not exhaust.

Show what is needed to understand where the user is and what can happen next.

Do not force every view to have exactly one primary action. If several choices are genuinely peers, preserve that equality.

If one action truly dominates, make it clear without turning the rest of the screen into decoration.

## Let support elements stay supporting

Bad hierarchy is not only “everything looks equal”. It can also be a supporting layer becoming too prominent.

Examples:

- metadata louder than the title;
- helper copy bigger than the task;
- a decorative badge stealing the focal point;
- navigation chrome dominating the content;
- AI hints becoming more memorable than the user's work.

A supporting element should know what it improves and what it has no right to own.

## Compose around imagery

When text and images share a field:

- protect faces, hands and semantically important detail;
- use naturally quiet image regions for text where possible;
- preserve intentional breathing room around the subject;
- avoid cropping just to fill a rectangle;
- do not add a heavy text panel if a small positional adjustment solves the collision.

The image is not a background texture if its subject matters.

## Before you finish

Ask:

- Can I tell what belongs together without reading every label?
- Is any separator doing a job space already did?
- Are the main structural edges stable?
- Are optical offsets intentional?
- Does asymmetry still feel balanced?
- Is the focal point clear without shouting?
- Are supporting elements staying supporting?
- Is the visual focal point compatible with the semantic reading order?
- Would removing one container make the composition calmer without losing meaning?
