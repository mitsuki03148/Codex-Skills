# Spacing and sizing

A sensible scale and comfortable spacing do more for typography than most effects. In quiet multilingual interfaces, spacing itself can carry hierarchy.

## Units

| Unit | Behavior |
| --- | --- |
| `px` | Fixed |
| `em` | Scales with the current font size |
| `rem` | Scales with the root font size |
| `%` on `font-size` | Relative to the parent's font size |
| `ch` | Approximate advance width of the Latin `0` glyph |
| `ic` | Approximate advance measure of a full-width CJK ideograph |

Use `ch` for Latin-oriented measures and `ic` when a CJK character count is the meaningful unit.

## Type scale

A small set of sizes used across a product, deviated from as little as possible. Hard-coding sizes with no system behind them breaks down at scale.

```css
:root {
  --text-sm: 0.875rem;
  --text-base: 1rem;
  --text-lg: 1.125rem;
  --text-xl: 1.5rem;
  --text-2xl: 2rem;
}
```

Pick an existing scale or define one. Tailwind's scale is a usable starting point, not a language rule.

Solo, default names work when usage rules are clear. On a team, semantic names such as `text-body-sm` preserve intent.

## Role-based scales

A role should normally decide size, line-height and weight together.

### Latin-oriented starting point

| Role | Size | Line-height | Weight |
| --- | --- | --- | --- |
| Display | `2.25rem` (36px) | `1.1`–`1.2` | `600` |
| Title | `1.5rem` (24px) | `1.2` | `600` |
| Heading | `1.125rem` (18px) | `1.3` | `600` |
| Body | `1rem` (16px) | `1.5`–`1.6` | `400` |
| Caption | `0.8125rem` (13px) | `1.4` | `400` |

### Quiet CJK starting point

Use smaller scale jumps and more breathing room before making headings louder:

| Role | Size | Line-height | Weight |
| --- | --- | --- | --- |
| Display | `2rem` (32px) | `1.25`–`1.35` | `600` |
| Title | `1.5rem` (24px) | `1.3`–`1.4` | `600` |
| Heading | `1.125rem` (18px) | `1.4`–`1.5` | `500`–`600` |
| Body | `1rem` (16px) | `1.6`–`1.8` | `400` |
| Caption | `0.8125rem` (13px) | `1.45`–`1.6` | `400` |

These are visual starting points, not standards. The actual font, platform, line length and role decide the final values.

For mixed EN / zh-Hant / ja in one component, use one semantic role and tune the line box for the densest script rather than assigning three unrelated scales.

## Heading hierarchy

Hierarchy does not have to come from dramatic size contrast.

In a restrained CJK interface, a section can become clearly subordinate or dominant through:

- space before and after;
- weight;
- placement;
- alignment;
- local grouping;
- slight size difference.

A child heading should not overpower its parent, but adjacent levels may share the same size when spacing and weight keep the structure clear.

Never pick a heading element for its browser-default size.

## Spacing is hierarchy

Do not solve every hierarchy problem by increasing font size.

Before making a heading larger, ask:

- Does it need more space above?
- Should it sit closer to the content it owns?
- Would one weight step be enough?
- Is the group boundary unclear?
- Is the surrounding layout too crowded?

This is especially important in Japanese-influenced calm layouts, where large scale jumps can make the interface feel louder than intended.

## Kerning and letter-spacing

Kerning adjusts specific pairs; `letter-spacing` adds uniform space between characters.

```css
/* Latin display only after visual verification */
.display-heading {
  letter-spacing: -0.02em;
}

/* Latin uppercase label */
.uppercase-label {
  text-transform: uppercase;
  letter-spacing: 0.05em;
}
```

Do not inherit those recipes into CJK.

- Chinese and Japanese body text normally stays at `letter-spacing: normal`.
- Avoid negative CJK tracking unless the exact face and role were checked.
- Do not add positive tracking merely to make CJK look airy; create air around the text block first.
- If mixed-script boundaries feel crowded, solve the boundary rather than spacing every glyph.

## Line-height

The more of the em box the glyph fills, the more vertical room the line often needs.

Latin body text commonly starts around `1.5`–`1.6`. Chinese and Japanese reading text commonly needs a more generous starting point such as `1.6`–`1.8`.

Short headings can be tighter, but do not copy `1.1` onto CJK automatically.

A tightly-leaded paragraph is harder to read than a slightly taller block is to fit.

## Measure

For prose:

- English: roughly `60–75ch`
- Japanese horizontal: roughly up to `40ic`
- Traditional Chinese book-like text: roughly `17–40ic`, with the actual medium and font deciding the final measure

Product UI often uses shorter lines than editorial prose. Measure should serve the reading task, not imitate a book.

```css
.prose-en { max-inline-size: 68ch; }
.prose-ja { max-inline-size: 40ic; }
.prose-zh-hant { max-inline-size: 36ic; }
```

These are starting examples.

## Mixed-script vertical rhythm

When English and CJK share a line:

- check Latin lowercase and punctuation do not look lost beside full-width glyphs;
- check CJK does not collide with the line above or below;
- do not vertically nudge isolated spans unless the full fallback chain has been tested;
- prefer adjusting family choice, size or line-height over per-string transforms.

## Text trimming with text-box

Fonts reserve space above and below glyphs, which can make labels look optically low.

`text-box` can trim those metrics, but the common `cap alphabetic` recipe is Latin-oriented:

```css
.badge {
  text-box: trim-both cap alphabetic;
}
```

Do not use Latin cap / alphabetic trimming as a universal CJK alignment fix.

CJK-specific ideographic text edges exist in the CSS model but are not uniformly available across browsers. Treat `text-box` as progressive enhancement and inspect EN / zh-Hant / ja separately. Unsupported browsers should remain comfortably aligned without it.
