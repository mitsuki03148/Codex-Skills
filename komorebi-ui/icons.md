# Icons

Icon weight, states, sizing, direction and optical character.

## One optical language per surface

Consistency matters more than a single numeric recipe.

A coherent icon set usually shares:
- stroke or fill logic;
- corner character;
- grid proportions;
- optical weight;
- level of detail.

Avoid mixing libraries whose personalities visibly disagree in the same toolbar or control family.

Where a project already uses a mixed set successfully, fix the outlier rather than replacing the whole system.

## Match optical weight, not just stroke width

An icon beside text should feel like it belongs to the same visual sentence.

Stroke width can help, but do not mechanically map font weights to `1.5 / 2 / 2.5px`.

The correct result depends on:
- icon grid size;
- stroke caps and joins;
- glyph density;
- adjacent font;
- CJK vs Latin visual mass;
- whether the icon is inline or standalone.

If the set exposes designed weight variants, use them. Otherwise keep the set's intended stroke and adjust size, color or emphasis before redrawing it.

## Size at render size

Test the smallest real render size.

- Prefer native grid sizes such as `16`, `20`, `24`.
- Simplify small glyphs instead of shrinking detailed artwork.
- Keep SVG for interface icons.
- Check optical centering after scaling.

An icon can be mathematically crisp and still be visually too dense.

## One asset, state from style

Where state color belongs to the UI system, use `currentColor`.

```html
<svg fill="none" stroke="currentColor">…</svg>
```

Let CSS / component state own color and opacity rather than exporting separate colored assets.

Separate assets remain legitimate when the geometry itself changes meaningfully.

## Outline vs fill is not a universal state law

Outline-default / fill-active is one useful pattern, especially for bookmarks, hearts and tabs.

Do not force it onto every icon family.

Active state may instead be carried by:
- color;
- background;
- position;
- label;
- weight;
- a genuinely different symbol.

Use the state language already established by the product.

## Familiar symbols beat novel ones

Do not redesign a mature convention merely to make the interface distinctive.

Common actions such as close, search, play, pause, back and disclosure should remain immediately recognizable unless the product has a strong reason to depart.

Originality belongs more safely in material, composition and illustration than in turning utility icons into riddles.

## Decorative icon vs semantic icon

A decorative mark may be subtle or even disappear.

A semantic icon must stay legible at its working size and state.

Do not apply the same opacity / blur / animation treatment to both just because they share an SVG component.

## Icons in RTL

Mirror direction-dependent icons and preserve icons whose meaning is physical or conventional.

Typical directional cases:
- back / forward navigation;
- reading-direction chevrons;
- indent / outdent;
- layout alignment symbols.

Usually stable:
- logos;
- checkmarks;
- clocks;
- cameras;
- physical objects;
- media play / pause convention unless the product explicitly localizes it.

Composite icons require judgment: the base may mirror while a badge or slash does not.

Accessible names for icon-only controls belong to `komorebi-accessibility`.

## Icon review

Ask:
- Does the glyph remain recognizable at its smallest render size?
- Does it belong to the same optical family as its neighbors?
- Is the active state still readable without motion?
- Is a novel symbol replacing a mature convention?
- Is an optical correction local to the glyph or incorrectly baked into every use?
