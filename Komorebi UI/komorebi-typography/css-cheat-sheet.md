# CSS cheat sheet

One-line lookup for the typography CSS declarations covered by this skill. Pick plain CSS or the project's utility system. Tailwind arbitrary-value forms are shown where no dedicated utility is assumed.

This sheet is a compiled view of the guidance in the other files. It should not invent a second set of typography rules.

## Font

| Declaration | What it does | Tailwind / utility form |
| --- | --- | --- |
| `font-family: sans-serif` | Generic sans family | `font-sans` |
| `font-family: serif` | Generic serif family | `font-serif` |
| `font-family: monospace` | Monospace family | `font-mono` |
| `font-size` | Size from the type scale | `text-*` |
| `font-weight` | Weight | `font-*` |
| `font-style: italic` | Italic style where the font / script supports it | `italic` |
| `font-synthesis-style: none` | Suppress synthetic italic / oblique | `[font-synthesis-style:none]` |
| `font-synthesis: none` | Disable all synthesis only after verifying fallbacks | `[font-synthesis:none]` |
| `font-feature-settings` | Niche OpenType feature | `[font-feature-settings:"ss01"]` |
| `font-variation-settings` | Variable-font custom axis | `[font-variation-settings:"GRAD"_80]` |
| `font-optical-sizing` | Optical size | `[font-optical-sizing:auto]` |
| `font-variant-caps` | Real small capitals | `[font-variant-caps:small-caps]` |
| `font-variant-position` | Real super / subscript glyphs | `[font-variant-position:super]` |
| `font-variant-numeric: tabular-nums` | Equal-width digits | `tabular-nums` |
| `font-variant-numeric: slashed-zero` | Distinguish 0 from O | `slashed-zero` |
| `font-variant-east-asian` | JIS / traditional / simplified / width / ruby variants | `[font-variant-east-asian:ruby]` |

## Language and writing mode

| Declaration / markup | What it does | Example |
| --- | --- | --- |
| HTML `lang` | Selects language-aware glyph, pronunciation and layout behavior | `lang="ja"`, `lang="zh-Hant"` |
| `direction` / HTML `dir` | Text direction | `dir="rtl"` |
| `writing-mode` | Horizontal / vertical writing | `[writing-mode:vertical-rl]` |
| `text-orientation` | Glyph orientation in vertical text | `[text-orientation:mixed]` |

## Spacing and layout

| Declaration | What it does | Tailwind / utility form |
| --- | --- | --- |
| `letter-spacing` | Tracking; do not copy Latin tracking defaults onto CJK | `tracking-*` |
| `line-height` | Space between lines | `leading-*` |
| `font-kerning` | Kerning on or off | `[font-kerning:none]` |
| `text-box` | Trim font box metrics where supported | `[text-box:trim-both_cap_alphabetic]` |
| `max-inline-size: 68ch` | English-oriented prose measure | `max-w-[68ch]` |
| `max-inline-size: 40ic` | CJK-oriented measure | `max-w-[40ic]` |
| `text-align` | Where lines start and end | `text-start` / `text-center` |

## Wrapping and mixed scripts

| Declaration | What it does | Tailwind / utility form |
| --- | --- | --- |
| `text-wrap: balance` | Balance a few heading lines | `text-balance` |
| `text-wrap: pretty` | Improve short prose wrapping | `text-pretty` |
| `line-break: strict` | CJK prohibition / punctuation line breaking | `[line-break:strict]` |
| `text-autospace: normal` | Progressive CJK / Latin / numeric boundary spacing | `[text-autospace:normal]` |
| `overflow-wrap: break-word` | Break long strings | `break-words` |
| `white-space: nowrap` | Stop wrapping | `whitespace-nowrap` |
| `text-overflow: ellipsis` | Single-line ellipsis | `truncate` |
| `line-clamp` | Cut after N lines | `line-clamp-*` |
| `text-transform` | Latin case presentation | `uppercase` / `capitalize` |

## Ruby and emphasis

| Declaration / markup | What it does | Tailwind / utility form |
| --- | --- | --- |
| HTML `<ruby><rt>` | Semantic ruby annotation | markup |
| `ruby-position` | Ruby placement | `[ruby-position:over]` |
| `text-emphasis` | East Asian emphasis marks | `[text-emphasis:filled_sesame]` |
| `text-emphasis-position` | Position emphasis marks | `[text-emphasis-position:over_right]` |

## Decoration and interaction

| Declaration | What it does | Tailwind / utility form |
| --- | --- | --- |
| `text-decoration-line: underline` | Underline | `underline` |
| `text-decoration-color` | Underline color | `decoration-*` |
| `text-decoration-thickness` | Underline thickness | `decoration-1` / `decoration-2` |
| `text-underline-offset` | Underline offset | `underline-offset-*` |
| `text-underline-position: from-font` | Underline position from font metrics | `[text-underline-position:from-font]` |
| `text-decoration-style` | Dotted / dashed / wavy | `decoration-dotted` / `decoration-wavy` |
| `text-decoration-thickness: from-font` | Thickness from the font | `decoration-from-font` |
| `text-decoration-skip-ink` | Gaps around glyph ink | `[text-decoration-skip-ink:auto]` |
| `caret-color` | Caret color | `caret-*` |
| `user-select: none` | Suppress selection only on verified drag / gesture conflicts | `select-none` |
| `text-shadow` | Shadow following glyph shapes | `text-shadow-*` |
| `-webkit-text-stroke` | Outline glyphs | `[-webkit-text-stroke:1px_black]` |
| `background-clip: text` | Clip background to glyphs | `bg-clip-text` |
| `initial-letter` | Drop cap where supported | `[initial-letter:3]` |

## A few script-aware reminders

- `65ch` is not a universal multilingual measure.
- Negative tracking is not a default CJK heading treatment.
- `text-autospace` is progressive enhancement; do not depend on it for basic readability.
- `line-break` is part of CJK wrapping, not decorative polish.
- Ruby and emphasis marks are semantic language tools, not Japanese styling effects.
- Correct `lang` belongs in the markup even when the visible text already “looks right”.
