# Spacing and adaptivity

Space between controls, margins against the viewport, hints at off-screen content and layouts that survive resizing, larger text and EN / Traditional Chinese / Japanese localization.

## Breathing room between targets

Where the project has no density scale, useful starting points remain:

| Between | Starting point |
| --- | --- |
| Adjacent bordered / filled controls | about `12px` |
| Around borderless controls | about `24px` |
| Clearly unrelated control groups | visibly larger than the intra-group gap |

These are interaction and grouping starting points, not an aesthetic formula.

Borderless controls need more clearance because space itself marks the boundary.

Compact professional tools may use less where hit areas stay distinct. Quiet or editorial layouts may use more where the larger pause has a real compositional job.

WCAG target sizes and pseudo-element expansion belong to `komorebi-accessibility`.

## Spacing has rhythm

Do not reduce layout spacing to one repeated number.

A good spacing system has relationships:

- within one thought;
- between sibling thoughts;
- before a new section;
- around a focal object;
- between content and controls;
- at the edge of the page.

Repeated spacing creates stability. Deliberate larger pauses create rhythm.

Do not alternate random values for decoration, but do not flatten every interval until the page becomes metronomic.

## Margins are not wasted space

Viewport margins protect content from feeling pasted to the glass.

Where no system exists, `16px` is still a reasonable mobile starting point, but do not turn it into a universal visual identity.

Large screens do not need to fill their width. A narrow content field surrounded by quiet space can be the intended composition.

## Inset controls from the edges

In content layouts, controls pressed against the viewport can look like system chrome and collide with safe areas.

Keep them inside the compositional margin unless they are deliberately platform chrome.

```css
.action-bar {
  padding-inline: 16px;
  padding-bottom: calc(16px + env(safe-area-inset-bottom));
}
```

Do not make an action edge-to-edge merely to increase its visual authority.

## Progressive disclosure needs enough evidence

Hiding complexity is useful; hiding existence is not.

Possible cues:

- partial next item;
- clipped continuation;
- subtle fade;
- scrollbar / scroll indicator;
- disclosure label;
- chevron;
- spatial continuation from one object to the next.

Pick the quietest cue that remains discoverable.

### Peeking items

A `16–32px` peek can work for card scrollers, but it is one recipe, not a universal rule.

Use enough continuation to make the next object legible as “more”, not enough to make the current object feel cramped.

Do not combine peek + arrow + badge + animation unless each cue has an independent job.

## Content bleeds, controls float

Backgrounds, atmosphere and media may extend to the viewport edge.

Controls and readable text usually stay inside safe areas and a stable content field.

But do not interpret this as “put every control in a floating card”. Controls can be visually quiet while their hit area and placement remain dependable.

## Compose with safe areas

Safe areas are physical constraints, not decoration.

Account for:

- notches;
- home indicators;
- browser / platform chrome;
- virtual keyboards;
- resizable windows;
- split view.

Do not let the safe-area solution create an unnecessary permanent bar when padding or reflow is enough.

## Hold structure until it breaks

Breakpoints belong to the composition.

Break when:

- text can no longer keep a useful measure;
- two objects lose their relationship;
- controls collide;
- an image crop destroys the subject;
- hierarchy becomes ambiguous;
- the layout starts requiring fragile exceptions.

Do not break at `768px` or `1024px` merely because those numbers are familiar.

Prefer container queries for reusable components.

## Preserve the same place across sizes

Responsive design should not feel like entering a different product.

Where possible:

- keep the same objects;
- preserve their relative importance;
- stack rather than replace;
- reflow rather than reset;
- keep the focal subject recognizable;
- preserve previous state when the container changes.

A layout can transform without erasing its identity.

## Plan for EN / Traditional Chinese / Japanese

Never rely on a universal “30% localization expansion” budget.

Test real strings.

### English

English labels can become very wide, especially product terms, names and descriptive buttons.

### Traditional Chinese

Character counts may be lower, but punctuation, line-breaking and larger optical glyph density can change vertical rhythm.

### Japanese

Kana / kanji mixtures can break differently from both English and Traditional Chinese. Long katakana product names can be unexpectedly wide.

### Mixed-script strings

Names, model numbers, dates and titles may contain Latin + CJK in one line.

Do not:

- hardcode width from the English fixture;
- hardcode height from one CJK fixture;
- assume fewer characters means less space;
- align by character count.

Do:

- let labels size from content;
- allow wrapping where the role permits it;
- use min-size instead of fixed size when a floor is needed;
- test all three supported languages on important components.

## Plan for larger text

Larger accessibility text is not just “the same layout scaled up”.

At larger sizes:

- columns may need to stack;
- side-by-side actions may become vertical;
- text-over-image may need to move off the image;
- sticky controls may need more height;
- decorative imagery may need to recede.

Keep the semantic order stable even when the visual arrangement changes.

## Image crops are responsive decisions

A crop that works at desktop can fail at phone.

Use focal positioning or alternate art direction when needed.

Do not centre-crop by habit. Preserve the subject and the negative space that the composition relies on.

When the same image supports EN / zh-Hant / ja text overlays, test every language because text width can consume different “quiet” regions.

## Clipping

Never park a critical action where it can be cut off by:

- a resizable pane;
- a fixed-height modal;
- an expanding keyboard;
- safe-area chrome;
- larger text;
- a translated label.

Keep primary actions in stable flow or stable chrome suited to the product.

Where a modal's content scrolls, its action row should remain reachable without obscuring the content.

## Adaptivity review

Before approving, test:

- smallest supported width;
- largest supported width;
- at least one awkward middle width;
- 200% zoom / large text;
- EN / zh-Hant / ja;
- keyboard open;
- split view or resizable window where relevant;
- image crops at each composition;
- hidden-content discoverability;
- RTL if the product supports it.

A responsive layout is finished when it still feels like the same place, not merely when nothing technically overflows.
