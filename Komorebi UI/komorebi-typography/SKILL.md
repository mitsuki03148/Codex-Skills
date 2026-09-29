---
name: komorebi-typography
description: Focuses on type scale, spacing, sizing, variable fonts, OpenType features, wrapping, truncation and mixed English / Traditional Chinese / Japanese typography that feels calm, legible and deliberate.
---

# Typography

Typography is mostly restraint: a sensible scale, comfortable spacing, enough contrast, and respect for the language being set. A label, a table cell, a marketing headline and an article paragraph do not share one set of rules. English, Traditional Chinese and Japanese do not share one typographic rhythm either.

When reviewing, read the rendered page instead of scanning the code. Bad wrapping, weak hierarchy, wrong CJK punctuation, fallback-glyph mismatch and truncation only show up at real content lengths.

Write every fix in the project's styling system. Treat the numeric values in this skill as starting points, not universal truths. Latin-oriented defaults must not be copied blindly onto Chinese or Japanese text. The [cheat sheet](css-cheat-sheet.md) maps each declaration to its Tailwind equivalent.

The words themselves belong to `komorebi-writing`. Semantic heading structure belongs to `komorebi-accessibility`. Spatial RTL layout and logical properties belong to `komorebi-layout`. Contrast measurement belongs to `komorebi-colors`. This skill owns how text renders, wraps and behaves across scripts.

## Language first

Set the language boundary before tuning typography.

- English: `lang="en"`
- Traditional Chinese: `lang="zh-Hant"` and, where relevant, a more specific regional tag such as `zh-Hant-HK` or `zh-Hant-TW`
- Japanese: `lang="ja"`

The browser, font and assistive technology use language information for pronunciation, glyph selection, punctuation behavior and line breaking. Do not make one script imitate another for visual consistency.

For mixed EN / Traditional Chinese / Japanese UI:

- Keep one shared hierarchy system, but let each script use its own spacing and glyph conventions.
- Do not manually convert Chinese or Japanese punctuation into English punctuation.
- Do not add handwriting, brush lettering, faux vertical text or decorative East Asian symbols just to make a design feel Japanese.
- Quiet hierarchy should come from spacing, weight, placement and proportion before display effects.
- A single well-chosen family or coordinated family set is often calmer than a conspicuous font pairing.

## Serve the right format

Use `.woff2` on the web, for Brotli compression and broad support. `.woff` is a fallback for very old browsers. `.ttf` and `.otf` are desktop formats with no web compression. How the files load is the project's concern.

CJK fonts can be large. Do not add a new webfont merely to satisfy a style preference when the existing product stack already covers the required languages well.

## Properties over raw tags

When a CSS property exists, use it.

- `font-weight: 650` instead of `font-variation-settings: "wght" 650`
- `font-optical-sizing: auto` instead of `"opsz"`
- `font-variant-numeric: tabular-nums` instead of `font-feature-settings: "tnum" 1`
- `font-variant-east-asian` for East Asian glyph variants, widths and ruby forms instead of raw OpenType tags where the property covers the need

Properties keep working when a non-variable fallback renders. Reserve raw tags for custom axes and niche features with no property of their own. Axes and features are listed in [variable-fonts-and-opentype.md](variable-fonts-and-opentype.md).

## Load intended weights and styles

Browsers synthesize a weight or style the active family does not provide, distorting the real face. Load the faces the design uses.

Synthetic oblique or italic can be especially awkward for Chinese and Japanese fonts. Do not use faux italic as a default CJK emphasis mechanism. Prefer weight, spacing, position or language-native emphasis. Disable synthesis only after checking the required forms and the fallback stack.

## Fewer fonts, sizes and weights

Rarely use more than three fonts. Weight and size define hierarchy; overusing them hurts readability fast.

Pair for contrast only when the product needs a deliberate display / reading split. A quiet interface does not need a serif headline simply to prove hierarchy exists. In mixed-script products, font pairing must work across EN / zh-Hant / ja, not only in the Latin sample.

Below `18px`, stay at weight `400` or heavier as a default. Thin CJK strokes can disappear sooner than Latin strokes, so verify real glyphs on real devices rather than trusting the numeric weight. Pairing guidance is in [choosing-fonts.md](choosing-fonts.md).

## Use a type scale with semantic names

Define a small set of sizes and deviate from it as little as possible. Hard-coded sizes with no system behind them break down at scale.

Solo, default names like `text-sm` are fine when usage rules are clear. On a team, name sizes by use (`text-body-sm`) so the rules survive other people. Scale construction is in [spacing-and-sizing.md](spacing-and-sizing.md).

A CJK-heavy interface often needs smaller jumps between roles than a Latin marketing page. Let spacing and weight carry some hierarchy instead of making every parent dramatically larger.

## Heading sizes descend with level

Map heading levels to descending steps of the type scale, so a visually subordinate heading never overpowers its parent. Adjacent levels may share a size toward the small end of the scale, as long as weight, spacing or placement keeps them distinct.

Do not force every level to differ by size. In restrained Chinese and Japanese interfaces, section spacing and weight can carry more hierarchy than scale contrast.

The semantic element is `komorebi-accessibility`'s; this skill sets only the visual treatment.

## Line-height by role and script

Latin starting points:

- short headings: around `1.1`–`1.25`
- body copy: around `1.5`–`1.6`

Chinese and Japanese usually need more vertical breathing room because the glyphs fill more of the em box. Start more generously, then verify the actual face:

- compact UI / short headings: roughly `1.3`–`1.5`
- reading text: roughly `1.6`–`1.8`

These are starting ranges, not locale laws. Mixed-script runs should be tuned against the tallest and densest glyphs actually rendered.

Prefer unitless values so line-height scales with font size. Anything that wraps to three or more lines should read like text, not like a compressed heading.

## Letter-spacing by script

Large Latin headings often tolerate slightly negative letter-spacing. Small Latin uppercase labels may need a little positive tracking.

Do not apply either habit to CJK by default.

- Chinese and Japanese body text normally needs no tracking.
- Avoid negative tracking on CJK unless the exact font and role were visually verified.
- Do not uppercase Chinese or Japanese labels to manufacture hierarchy.
- If mixed Latin inside CJK needs spacing, handle the script boundary rather than tracking the whole run.

## Cap the measure

Long lines make it hard for the eye to find the next one.

- English long-form text: around `60–75ch` is a useful starting range.
- Japanese horizontal prose: around `40ic` or less is a useful editorial ceiling.
- Traditional Chinese body text often falls around `17–40ic` in book-like composition; UI should follow the actual component and reading task rather than chase a book measure.

`ch` approximates a Latin zero width. `ic` approximates a full-width CJK character. Do not use `65ch` as a universal multilingual measure.

See [wrapping-and-punctuation.md](wrapping-and-punctuation.md).

## Wrap deliberately

Four familiar declarations, plus CJK line-breaking:

- `text-wrap: balance` distributes text evenly across a few heading lines. Use it only when the result actually looks better in that language.
- `text-wrap: pretty` can improve short descriptions, especially English.
- `overflow-wrap: break-word` handles long links, IDs and unbreakable strings.
- `white-space: nowrap` keeps labels and badges together when a break would look broken.
- `line-break` controls CJK punctuation and prohibition rules. Use language-aware values rather than treating Chinese and Japanese as long strings with spaces missing.

Skip `balance` and `pretty` in long-form text.

## Mixed-script boundaries

Do not hand-insert spaces everywhere between CJK and Latin or numbers. That turns editorial spacing into content and becomes inconsistent across locales.

Where supported and appropriate, `text-autospace` can manage CJK / Latin / numeric boundaries as progressive enhancement. Older browsers must still read correctly without it.

Use explicit spaces only when the content itself requires a word space.

## Tabular numbers on changing values

Digits have different widths by default, so timers, counters and prices shift the layout as they update. Apply `font-variant-numeric: tabular-nums` to values that change.

Check the chosen CJK family or fallback stack actually contains the numeric style you expect.

## Truncate without losing content

For a single line, `text-overflow: ellipsis` with `overflow: hidden` and `white-space: nowrap`. For several, `line-clamp`.

Truncation hides content. When the missing text matters, keep the full value reachable in a tooltip, expanded view or accessible name.

Do not assume the same character count occupies the same width across EN / zh-Hant / ja.

## Write copy naturally, style with CSS

Store text in the punctuation and case natural to its language.

English prose uses English punctuation conventions. Traditional Chinese and Japanese use their own punctuation and quote forms according to locale and house style. Do not run one global “smart punctuation” transform across all languages.

For English:

- Curly quotes in prose, straight quotes in code.
- En dash for ranges: `2010–2020`.
- Single ellipsis character, not three periods.
- `&nbsp;` where an English unit pair such as `16 px` must not break.
- `&shy;` only where a Latin word may break.

For CJK, let language-aware line breaking and punctuation rules do the work. Do not use `&nbsp;` or manual spaces to simulate inter-script typography.

## Underlines from the font

Pull position and thickness from the font's metrics with `text-underline-position: from-font` and `text-decoration-thickness: from-font`. Tune only when the real font needs it.

A dotted underline can indicate extra information, but do not assume a Western abbreviation pattern maps naturally to every CJK interface. Keep the semantic cue clear.

Color is the only part of a real underline that animates reliably. For more elaborate motion, use a separate element rather than forcing `text-decoration`.

## Inputs at 16px on mobile

iOS Safari zooms the page when an input's text is smaller than `16px`. Keep the input at `16px` on mobile or use the verified scaling recipe in [details-and-accessibility.md](details-and-accessibility.md).

Do not shrink Chinese or Japanese input text to create a quieter field. Quietness is not a readability tax.

## Size and contrast floors

Start long-form body text around `16px`, then verify the actual typeface, script and measure.

UI text can go smaller. `14px` is a useful starting point for inputs and menus, `13px` for captions and rarely below `12px`. CJK may need equal or larger optical size than Latin at the same nominal `font-size`.

When text looks low-contrast, use `komorebi-colors` to measure the rendered pair and `komorebi-accessibility` to classify the requirement. Do not create “Japanese softness” by making essential text faint.

## Font smoothing

Do not add font smoothing as a universal aesthetic rule.

On some macOS setups, `-webkit-font-smoothing: antialiased` can make Latin text feel lighter; it can also make already delicate CJK strokes feel too thin. Apply it once at the root only when the project's actual EN / zh-Hant / ja rendering has been checked on target devices.

## Language, bidi and writing mode

Set `lang` at the document and at content boundaries where language changes. Set `dir` where direction changes. Preserve digit order and use `<bdi>` when adjacent RTL text disturbs a mixed value.

Vertical writing can be beautiful, but do not introduce `writing-mode: vertical-rl` merely to signal “Japanese”. Use it only when the content and composition genuinely call for vertical text, then verify punctuation, ruby, orientation and accessibility in that mode.

## Keep useful text selectable

Keep text selectable by default. `::selection` can carry brand into the reading experience as long as the selected combination stays legible.

`user-select: none` belongs on a draggable or gesture-driven surface where accidental selection interferes. Never across the interface and never because a button label can be highlighted.

## Before you finish

| Mistake | Fix |
| --- | --- |
| Latin rules applied unchanged to CJK | Recheck line-height, measure, tracking, punctuation and wrapping by language |
| Wrong glyph form inside mixed CJK content | Set the correct `lang`; verify the fallback family |
| Japanese / Chinese heading made huge just to show hierarchy | Let spacing, weight and placement carry more of the hierarchy |
| Negative tracking copied onto CJK | Return to normal tracking unless the exact font proves otherwise |
| `65ch` used for every language | Use `ch` for Latin-oriented measure and `ic` for CJK-oriented measure |
| Punctuation stranded at a bad CJK line boundary | Use correct `lang` and `line-break`; inspect real wrapping |
| Manual spaces inserted between every CJK / Latin boundary | Keep content natural; use language-aware spacing or `text-autospace` where appropriate |
| Handwriting / brush font used as a shortcut to “Japanese” | Return to a readable family; create tone with rhythm, spacing and material instead |
| Synthesized italic distorts CJK | Prefer a real style or a different emphasis mechanism |
| Synthesized face differs from the design | Load the real face; disable only the verified synthesis mode |
| Child heading visually overpowers its parent | Map that section's hierarchy to descending roles |
| Heading element picked for its default size | Choose semantics first, then style it |
| Orphan on a short English description | `text-wrap: pretty` |
| Lopsided short heading | Test `text-wrap: balance` rather than applying it blindly |
| Justified text in an interface | Use start alignment; reserve justification for intentional editorial layouts |
| Underline cuts through glyphs | Verify font metrics and `text-decoration-skip-ink` |
| Mixed-direction value renders in the wrong order | Correct `lang` / `dir`; isolate with `<bdi>` |
| Selection disabled across application chrome | Restore it; suppress only where drag / gesture requires it |
| Thin weight on small UI text | Use a sturdier weight and verify the actual script |
| Tight leading on a multi-line description | Increase line-height until the real rendered block reads comfortably |

## Reporting

**Severity.** `HIGH` makes text unreadable, uses the wrong language/glyph behavior, or hides important content with no recovery. `MEDIUM` breaks the type system, hierarchy or mixed-script behavior. `LOW` is isolated polish.

**Verification.** Without a browser: inspect declared family, language, size, weight, line-height, measure, line-breaking and truncation rules against realistic EN / zh-Hant / ja strings. With one: resize the viewport and read the rendered page in every language the component actually supports. Check fallback glyphs, punctuation, mixed-script spacing, widows and truncation. Report every check you could not run as `Not verified`.

**Format.** Group findings under the principle each violates, ordered by severity, one row per root cause listing every location it appears in:

| Severity | Location | Before | After | Why |
| --- | --- | --- | --- | --- |

`Location` is `path/to/file:line`. `Why` names the principle and user impact.

End with `Block` when any `HIGH` remains, `Approve` otherwise, leaving the rest in the table as work to do. Never `Approve` coverage you did not inspect. With nothing to report, state "No actionable typography findings" and report verification.
