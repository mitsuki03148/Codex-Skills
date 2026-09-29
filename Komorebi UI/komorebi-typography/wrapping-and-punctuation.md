# Wrapping and punctuation

Where lines start, where they end, where they break and which characters they use.

This is the most language-sensitive part of the typography system. English, Traditional Chinese and Japanese should share layout intent without being forced into one punctuation or line-breaking model.

## Measure (line length)

Long lines make it harder for the eye to find the start of the next.

### English

For long-form text, around `60–75ch` is a useful starting range.

### Japanese

For horizontal prose, around `40ic` or less is a useful editorial ceiling.

### Traditional Chinese

Book-like body text commonly sits around `17–40ic`, with the medium, region, typeface and composition deciding the final measure.

Product UI often needs shorter lines than editorial prose.

`ch` measures against the Latin `0` glyph. `ic` measures against a typical full-width CJK ideograph. Use the unit that matches the script you are sizing.

```css
.prose-en { max-inline-size: 68ch; }
.prose-ja { max-inline-size: 40ic; }
.prose-zh-hant { max-inline-size: 36ic; }
```

These are starting examples, not hard requirements.

## Alignment

`text-align: start` is the normal UI default.

Do not globally justify application text. Editorial Chinese and Japanese can legitimately use justification, but book composition rules should not be copied into menus, forms and short interface copy.

If an editorial surface intentionally justifies CJK, test punctuation spacing and mixed Latin carefully rather than relying on a generic Western word-space model.

## CJK line breaking

Chinese and Japanese do not use spaces between ordinary words the way English does. That does not make them unbreakable strings.

Use the browser's CJK-aware line-breaking behavior.

```css
:lang(ja),
:lang(zh-Hant) {
  line-break: strict;
}
```

`strict` is a useful starting point when strong prohibition rules are desired, but verify the exact product and browser behavior. `normal` or `loose` may be better for some compact interfaces.

Do not use `word-break: break-all` as a generic CJK fix. It can damage embedded English, URLs and identifiers.

Use `overflow-wrap` for genuinely unbreakable content such as long URLs or IDs.

## Wrapping

| Property | Use |
| --- | --- |
| `text-wrap: balance` | A few short heading lines when the language actually benefits |
| `text-wrap: pretty` | Short prose, especially English, where a lonely final word looks poor |
| `overflow-wrap: break-word` | Long links, IDs or unbreakable strings |
| `white-space: nowrap` | Labels and badges where a break looks broken |
| `line-break` | CJK punctuation and prohibition rules |

Do not assume `balance` produces a more Japanese or Chinese composition. Read the rendered heading.

Skip `balance` and `pretty` in long-form text.

## Mixed CJK / Latin spacing

Traditional Chinese and Japanese text often mixes Latin names, acronyms and numbers.

Do not solve the boundary by globally inserting literal spaces into content. That creates inconsistent copy and makes localization harder.

Where browser support is acceptable, `text-autospace` can add conservative spacing between CJK and Latin / numeric runs:

```css
.mixed-cjk {
  text-autospace: normal;
}
```

Treat it as progressive enhancement. Older browsers must remain readable without it.

If the product deliberately uses a fixed house style for mixed-script spacing, apply it consistently at the typography layer rather than editing strings one by one.

## Punctuation belongs to the language

Do not run one global smart-punctuation transform across multilingual content.

### English

- Curly quotation marks in prose.
- En dash for ranges: `2010–2020`.
- Em dash where the writing style calls for it.
- Single ellipsis character: `…`.

### Traditional Chinese

Use Traditional Chinese punctuation according to region and house style, including full-width punctuation and the appropriate quotation marks.

Taiwan / Hong Kong punctuation traditions can differ from Mainland Chinese composition. `zh-Hant` is more useful than merely knowing that the characters are “Chinese”; add a regional language tag when regional typography matters.

### Japanese

Use Japanese punctuation such as `、。` and Japanese quotation marks such as `「」` / `『』` where the copy calls for them.

Do not replace them with English commas and quotes for visual uniformity.

## Prohibition rules

CJK punctuation has line-start and line-end restrictions.

The browser can handle much of this when `lang` and `line-break` are correct. Always inspect real wrapped copy.

Common failures to catch:

- closing punctuation stranded at line start;
- opening brackets or quotation marks stranded at line end;
- punctuation separated unnaturally from the phrase it belongs to;
- Latin words broken character-by-character inside CJK;
- manually inserted spaces creating awkward gaps around punctuation.

## Truncation

- Single line: `text-overflow: ellipsis` with `overflow: hidden` and `white-space: nowrap`.
- Multiple lines: `line-clamp`.

Truncation hides content. Where the missing text matters, expose the full value in a tooltip, expansion or accessible name.

Do not tune truncation against one English fixture and assume the Chinese and Japanese versions fit. CJK often reaches a different visual density at the same character count.

## Case

`text-transform` is primarily a Latin concern.

Do not uppercase Chinese or Japanese text to manufacture hierarchy. Keep the source copy natural and use visual roles instead.

## Non-breaking and discretionary breaks

Use `&nbsp;` where an English unit or phrase must stay together.

Use `&shy;` only for languages and words where discretionary hyphenation makes sense.

Do not use either as a substitute for CJK line-breaking rules or script-boundary spacing.

## Vertical writing

Vertical Chinese and Japanese composition has its own punctuation, ruby and orientation behavior.

Do not rotate a horizontal text box as a shortcut.

If the product genuinely needs vertical writing:

```css
.vertical-ja {
  writing-mode: vertical-rl;
  text-orientation: mixed;
}
```

Then verify punctuation, Latin orientation, numbers, ruby, emphasis marks, selection and accessibility in the actual writing mode.

Vertical text is not a decorative shortcut to “Japanese”.
