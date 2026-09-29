# Details and accessibility

Underlines, selection, forms, annotations, decorative text and the floors that keep everything readable.

Japanese-influenced calmness must come from proportion and restraint, not from making text smaller, thinner, fainter or harder to operate.

## Underlines

Default underline position is browser-determined. Pull position and thickness from the font's own metrics where they look right:

```css
a {
  text-underline-position: from-font;
  text-decoration-thickness: from-font;
  text-decoration-skip-ink: auto;
}
```

Tune manually only after checking the real EN / zh-Hant / ja glyphs.

A dotted underline can signal extra information, but do not assume a Western abbreviation convention automatically reads the same in every CJK interface.

## Selection

Keep useful text selectable.

- `::target-text` styles text highlighted by a shared link.
- The Custom Highlight API can style search matches without extra markup.
- `::selection` may carry brand as long as contrast stays legible.

`user-select: none` belongs only where selection conflicts with drag or gesture behavior.

## Forms and editable text

- `::placeholder` styles hints.
- `caret-color` colors the insertion caret.
- Keep placeholders subordinate without making them unreadably faint.
- Check IME composition for Chinese and Japanese input. Do not treat an in-progress composition string as a committed value.

### iOS input zoom

Safari may zoom the page when input text is smaller than `16px`.

The calm solution is not to shrink CJK text harder. Either render the input at `16px` on mobile or use a verified scaling technique while preserving the true hit area.

```tsx
<input className="text-base sm:text-sm" type="email" />
```

If using a transformed 16px input, let a wrapper draw the field surface so the hit area and visual chrome do not shrink with the glyphs.

## Ruby

Ruby is semantic annotation, commonly used for pronunciation or reading support.

Use native HTML:

```html
<ruby>
  木漏れ日
  <rp>(</rp><rt>こもれび</rt><rp>)</rp>
</ruby>
```

Use `ruby-position` only when explicit placement is needed.

Do not fake ruby with tiny absolutely positioned spans. Native ruby participates in layout and is more honest for accessibility.

Ruby should appear because the content needs annotation, not because the design wants to look Japanese.

## Emphasis marks

East Asian emphasis marks can be more natural than synthetic italic in some Japanese or Chinese contexts.

```css
:lang(ja) .emphasis {
  text-emphasis: filled sesame;
  text-emphasis-position: over right;
}
```

Japanese commonly places horizontal emphasis above the text. Chinese conventions can differ by region and design.

Use emphasis marks sparingly and semantically. They are not decoration.

## Decorative text

CSS can produce drop caps, gradients, strokes and text shadows. These are tools, not default typographic polish.

| Property | Effect |
| --- | --- |
| `::first-letter` | First-letter styling |
| `initial-letter` | Drop-cap sizing where supported |
| `background-clip: text` | Clips a background to glyphs |
| `-webkit-text-stroke` | Outlines glyph contours |
| `text-shadow` | Shadow following glyph shapes |

Do not use calligraphic effects, outlines, faux seals, vertical text or brush-like treatment as shortcuts to East Asian identity.

A restrained design often looks more culturally grounded when the typography simply behaves correctly.

## Sizes

Typography must survive zoom, larger browser font sizes, overridden line-height and user letter spacing.

| Text | Starting point |
| --- | --- |
| Long-form body | Around `16px`, verified in the actual script and measure |
| Inputs and menus | Around `14px`, except mobile input zoom constraints |
| Captions | Around `13px` |
| Floor | Rarely below `12px` |

CJK glyphs can feel denser at the same nominal size. Judge optical readability, not just the CSS number.

Do not create “quiet Japanese UI” by moving essential labels below a comfortable reading size.

## Contrast and weight

Soft palettes still need readable text.

Do not compensate for a low-contrast color by also using a thin weight. Test the real pair.

Chinese and Japanese text may need a sturdier weight than a Latin sample in the same role, depending on the font and display.

## Font smoothing

Font smoothing is not a universal quality switch.

```css
html {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

On some macOS displays this makes Latin text appear lighter. On some CJK faces it can make already delicate strokes feel weak.

Apply it at the root only after checking the actual multilingual product. Do not add it per component.

## Language and assistive technology

Correct `lang` is an accessibility feature as well as a typography feature.

When a sentence switches language, mark the boundary so screen readers can switch pronunciation and the browser can select appropriate glyph behavior.

Do not hide visible Japanese or Chinese text from assistive technology and replace it with unrelated English merely because the English label is easier to author.

## Motion and text

Hover, press and focus treatments must not make text reflow or jump.

Avoid animated tracking, font-size changes or weight changes that visibly shift multilingual labels unless the movement is deliberate and tested. A calm interface should not ask the reader to re-acquire text during interaction.

## Accessibility review for mixed EN / zh-Hant / ja

Before approving:

- zoom and larger text still work;
- CJK line-height remains comfortable;
- input methods can compose text normally;
- ruby remains attached to the correct base text;
- emphasis marks do not collide with adjacent lines;
- language changes are marked;
- focus and hover do not obscure glyphs;
- important text is not relying on thin strokes or low contrast;
- truncation does not remove the only available meaning.
