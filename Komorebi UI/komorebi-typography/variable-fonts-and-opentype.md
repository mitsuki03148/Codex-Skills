# Variable fonts and OpenType

What a font file can do beyond drawing letters, and how to reach those abilities without forcing one script into another script's habits.

## Static vs variable

- **Static font:** one weight and one style per file.
- **Variable font:** a range of values in one file, such as `font-weight: 589`.

A variable font is not automatically better. At one or two weights, static files can be smaller. At several weights, optical sizes or custom axes, a variable font may win.

For CJK, file size matters. A technically elegant variable font can still be the wrong product choice if it makes multilingual delivery unnecessarily heavy.

## Load intended weights and styles

Use a weight or style the active family does not provide and the browser may synthesize it.

`font-synthesis` controls that behavior, but do not disable everything blindly. Verify the whole fallback stack first.

For Chinese and Japanese, synthetic oblique / italic is often a poor default because many families are not designed with an italic companion. Prefer a real style or another emphasis mechanism.

A useful targeted rule can be:

```css
:lang(ja),
:lang(zh-Hant) {
  font-synthesis-style: none;
}
```

Use it only after confirming emphasis remains distinct and the fallback stack behaves correctly.

## Axes

Variable-font controls use four-letter tags.

| Axis | Tag | Controls |
| --- | --- | --- |
| Weight | `wght` | Stroke thickness |
| Optical size | `opsz` | Details and spacing tuned for size |
| Width | `wdth` | Glyph width |
| Slant | `slnt` | Slant angle |
| Custom | e.g. `GRAD` | Whatever the designer built |

A font supports only the axes its designer included.

Do not assume a Latin custom axis improves CJK glyphs the same way. Check the font's own documentation and the actual multilingual output.

## Properties over axis tags

When a property exists, use it.

```css
.heading {
  font-weight: 650;
  font-optical-sizing: auto;
}

.heading-grade {
  font-variation-settings: "GRAD" 80;
}
```

Common properties survive fallback better than raw `font-variation-settings`.

## OpenType features

OpenType features work in static and variable fonts when the family includes them.

### Common Latin / numeric features

| Feature | Preferred CSS |
| --- | --- |
| Tabular numbers | `font-variant-numeric: tabular-nums` |
| Slashed zero | `font-variant-numeric: slashed-zero` |
| Small caps | `font-variant-caps` |
| Super / subscript glyphs | `font-variant-position` |

Use raw `font-feature-settings` only for features with no suitable CSS property.

## East Asian variants

East Asian glyph choices deserve the same first-class treatment as numeric variants.

Use `font-variant-east-asian` when the font supports the requested forms:

```css
/* Example only: use the variant the actual content requires */
:lang(ja) .historical-jis {
  font-variant-east-asian: jis90;
}

ruby {
  font-variant-east-asian: ruby;
}
```

Available values include:

- `jis78`, `jis83`, `jis90`, `jis04`;
- `traditional`, `simplified`;
- `full-width`, `proportional-width`;
- `ruby`.

Do not use these values as decorative switches. They change glyph forms or widths and must match the content, locale and font.

Traditional Chinese and Japanese may share Han code points but expect different glyph traditions. Correct `lang` is the first line of defence.

## Language-specific glyphs

Prefer HTML `lang` and the font's own language system.

Do not reach for `font-language-override` as a normal multilingual solution. It is a specialised override and browser support is not universal.

The product should normally say which language the text is, then let the font and browser choose the right language form.

## Full-width and proportional forms

Do not globally force full-width Latin or numbers to make mixed CJK text look “more Japanese”.

Use `full-width` or `proportional-width` only when the content and font call for it.

Mixed EN / zh-Hant / ja interfaces should usually keep normal Latin / numeric forms and solve spacing at the script boundary instead.

## Ruby

Ruby annotation is language content, not decoration.

Use semantic HTML:

```html
<ruby>
  明日
  <rp>(</rp><rt>あした</rt><rp>)</rp>
</ruby>
```

Use CSS such as `ruby-position` only when the language and reading design need explicit control.

Do not fake ruby with absolutely positioned tiny text. Native ruby participates in line layout and accessibility more honestly.

## Emphasis

### Latin

Italic, weight, small caps or underline may be appropriate depending on the role.

### Japanese and Traditional Chinese

Do not assume italic is the natural equivalent.

Prefer, depending on language and product:

- a real weight change;
- emphasis marks;
- underline where semantically clear;
- position or spacing;
- ruby or annotation when that is the actual linguistic function.

The goal is not to make every script use the same visual gesture. The goal is for every script to express the same semantic importance naturally.

## Stylistic sets and character variants

`ss01` = stylistic set, slot 01. `cv11` = character variant, slot 11. Their meaning differs by font.

Check the font's docs. Never activate a stylistic set globally just because one English sample looks nicer; inspect CJK glyphs, numerals and punctuation as well.
