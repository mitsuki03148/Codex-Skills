# Choosing fonts

Choosing a typeface, the right file format and why fonts look the way they do.

## Language before personality

A typeface must first cover the language correctly. Tone comes after readable glyphs, punctuation and fallback behavior.

For EN / Traditional Chinese / Japanese products, verify:

- English Latin forms;
- Traditional Chinese glyphs for the intended region;
- Japanese kanji, kana and punctuation;
- numerals and symbols used in the product;
- fallback behavior when one family does not cover all scripts.

Set `lang` correctly. A multilingual font can still choose language-specific glyph forms from the same Unicode code point.

## Choosing a typeface

Font families set the tone before the specific font does.

### Latin-oriented categories

| Category | Traits | Use for |
| --- | --- | --- |
| Serif | Contrast and finishing strokes | Long passages, editorial reading, deliberate display |
| Sans-serif | Clean, even shapes | Default for most interfaces |
| Monospace | Every glyph the same width | Code, aligned technical data |
| Display | Drawn for large headlines | Marketing or rare focal text |
| Script | Handwriting-like | Rare decorative moments |

### East Asian families

Names vary by language and foundry, but these broad families are useful:

| Family | Typical character | Good use |
| --- | --- | --- |
| Gothic / ゴシック / 黑體 | Even strokes, clean, modern | UI, controls, long-lived product text |
| Mincho / 明朝 / 明體 / 宋體 | Stroke contrast and small finishing details | Editorial reading, calm or literary accent |
| Maru Gothic / 丸ゴシック | Rounded Gothic forms | Friendly Japanese accents when the product genuinely wants softness |
| Kai / 楷體 | Calligraphic regular-script character | Traditional Chinese editorial or cultural contexts, not a default UI face |

Do not treat these as mood stickers. A Mincho heading does not automatically make a page Japanese; a brush or handwritten face does not make a product culturally authentic.

### Rules

- Fewer fonts is usually better. Rarely use more than three; one strong multilingual family can be enough.
- The same applies to sizes and weights. They define hierarchy, and overusing them hurts readability.
- Pair for contrast only when contrast has a job. A quiet interface does not need a serif + sans split by default.
- In mixed-script products, pair by optical size, stroke density, weight and tone across EN / zh-Hant / ja. Two families that look balanced in English may clash badly once CJK appears.
- Thin weights are display-only. Below `18px`, start at `400`+ and verify real CJK strokes on target screens.
- Do not use faux italic or oblique as the main CJK emphasis method.

## Mixed-script rhythm

Nominally equal font sizes do not guarantee equal optical size.

Latin x-height, CJK square glyphs and punctuation occupy the em differently. When two families share a line:

- compare capitals, lowercase, Han / kana and numerals together;
- tune by optical balance, not just matching CSS numbers;
- avoid shrinking CJK merely because it looks larger in the same `font-size`;
- avoid making Latin disproportionately bold to “catch up” with dense CJK;
- verify punctuation and brackets, not only letters.

A useful test string includes English, Traditional Chinese, Japanese, Latin numbers and punctuation in one real component.

## Font family scope

Applying or reviewing typography never requires a new typeface. Use the product's type system unless the task asks for a type change, and never introduce a paid or proprietary face to satisfy a checklist.

For UI, a system stack can be appropriate, but system UI families differ by OS and CJK locale. Do not assume `system-ui` creates identical EN / zh-Hant / ja typography everywhere.

For long-form reading, choose a family or fallback stack intentionally rather than relying on whichever UI font the operating system provides.

Example structure:

```css
:root {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
}

:lang(ja) {
  font-family: "Hiragino Sans", "Yu Gothic", "Noto Sans JP", sans-serif;
}

:lang(zh-Hant) {
  font-family: "PingFang TC", "Noto Sans TC", sans-serif;
}
```

These are examples, not a mandate to add new fonts. Prefer the project's existing stack when it already covers the languages well.

## Japanese / Chinese feeling without costume

Do not reach for:

- brush fonts;
- pseudo-calligraphy;
- excessive handwritten labels;
- random vertical text;
- decorative kanji used as ornaments;
- forced full-width Latin;
- “Japanese-looking” punctuation in English copy.

Create tone through:

- proportion;
- spacing;
- material;
- restrained hierarchy;
- language-correct punctuation;
- calm weight changes;
- consistent placement.

Typography should feel as if it belongs to the language, not as if the interface put on a costume.

## Display vs text variants

"Display" in a font's name does not make it a display font. Some families ship optical variants for large and small sizes. Use the variant matching the actual role.

CJK families may have fewer explicit optical styles than Latin families. Do not simulate them with extreme tracking or synthetic slant.

## Formats

| Format | Notes |
| --- | --- |
| `.woff2` | Brotli compression, broadly supported. Use this on the web. |
| `.woff` | Older compression. Fallback only for very old browsers. |
| `.ttf` / `.otf` | Raw formats, no web compression, larger files. Desktop only unless there is no other option. |

CJK webfonts can be large. Measure the delivery cost before adding several families or many weights.

## Anatomy of a typeface

Latin and CJK expose different visual cues.

### Latin

| Term | Meaning |
| --- | --- |
| x-height | Height of a lowercase `x` |
| Cap height | Height of uppercase letters |
| Baseline | The invisible line letters sit on |
| Ascender | Part rising above the x-height |
| Descender | Part dropping below the baseline |

### CJK

CJK glyphs are commonly designed around a square ideographic frame. Stroke density, side bearings, punctuation placement and the apparent size of the full-width glyph matter more than Latin x-height.

This is why two fonts at the same `font-size` can look radically different, and why “match the CSS number” is not a sufficient mixed-script pairing method.
