---
name: komorebi-writing
description: Improves interface copy, terminology, tone, recovery language and multilingual EN / Traditional Chinese / Japanese product writing while preserving product meaning, natural grammar, register and each language's own voice.
---


# Interface writing


Interface writing helps the user understand where they are, what can happen next and what changed.


Clarity comes first where the user must act or recover. Elsewhere, warmth, restraint, character and a little silence can belong when they serve the product rather than compete with it.


Do not confuse brevity with clarity. The shortest label is not automatically the best one, and the most explicit sentence is not automatically kinder. Write only the amount the moment needs.


How copy renders belongs to `komorebi-typography`. Error markup, accessible names and announcements belong to `komorebi-accessibility`. Space for localized strings belongs to `komorebi-layout`. Visual emphasis belongs to the relevant visual owner.


## Language first


Write each language as itself.


For EN / Traditional Chinese / Japanese products:


- preserve one product meaning and terminology system across locales;
- let sentence structure, pronouns, politeness, punctuation and information order follow the language;
- do not translate an English microcopy pattern word-for-word merely because the English is concise;
- test the copy in the real component, because a natural Japanese or Traditional Chinese label may occupy the geometry differently from English;
- use the project's regional conventions where `zh-Hant-HK`, `zh-Hant-TW`, Japanese or English variants differ.


A shared product voice does not require identical grammar.




## Naturalness by locale


Treat English, Traditional Chinese and Japanese as related product voices, not three skins over one English sentence.


### English


- follow the product's actual English locale; UK / US spelling, nouns and conventions are product terminology, not cosmetic variants;
- concise active phrasing is often natural, but do not shorten until the wording becomes telegraphic or loses responsibility;
- do not turn English idioms, phrasal CTAs or source-string word order into translation templates.


### Traditional Chinese


- `zh-Hant` is a script family, not one universal locale. `zh-Hant-HK` and `zh-Hant-TW` may differ in terminology, register, punctuation and ordinary product vocabulary; follow the project's locale source of truth;
- subject omission is often natural. Do not add 你／您 or 請 to every sentence or control merely because English uses “you” or an imperative;
- avoid translated-English habits such as long noun stacks, repeated possessives, unnecessary passives and sentence structures that are technically grammatical but feel imported;
- when a product deliberately uses a Hong Kong / Cantonese conversational voice, preserve that voice. Do not “correct” it into Taiwan / Mandarin-style written Chinese unless the current content guide asks for that;
- high-stakes copy should remain clear and region-appropriate even when low-stakes surfaces use warmer or more colloquial language.


### Japanese


- choose a stable relationship and politeness level for each surface. Messages may use natural です／ます, while compact controls often should not be expanded into repeated 〜してください;
- omit 私／あなた when context already carries the subject. Repeating あなた can sound mechanical, confrontational or unnecessarily explicit;
- use familiar Japanese UI wording and distinguish the real action. Labels such as 次へ, 続ける, 完了, 保存 and 削除 are not interchangeable translations of an English CTA family;
- avoid literal English word order, noun stacks, unnecessary katakana and over-polite phrasing that hides what actually happened;
- in errors, permissions, payments and destructive confirmations, politeness must not dilute the consequence, owner or recovery step.


Natural localization preserves the same product truth, not the same sentence shape.


## Recon the existing voice


Before writing or reviewing, read nearby copy, the current flow, the product terminology, localization conventions and any voice or content guide.


Separate three things:


1. **Meaning** — what the user must understand.
2. **Voice** — the product's stable character.
3. **Tone** — how that voice changes with the stakes.


A deliberate brand voice is not a defect. Raise it only when it creates ambiguity, inconsistency, translation risk, false reassurance, or a tone the moment cannot support.


## One voice, flexible tone


The product may be recognizably itself without sounding equally playful everywhere.


| Context | Tone |
| --- | --- |
| Routine controls, settings, forms | Quiet, direct, low-attention |
| Onboarding, success, empty or reflective moments | Warm when useful; character can breathe |
| Errors and recovery | Calm, specific, useful |
| Destructive actions, money, privacy, security, data loss | Explicit, serious, no decorative wit |


Low-stakes copy can carry personality. High-stakes copy must carry truth first.


## Directness is language-aware


In English, direct second-person language is often clear: “Choose a date”, “Your draft is saved”.


Do not make `you` a multilingual rule.


Traditional Chinese and Japanese often omit the subject naturally when context is obvious. Repeating 你／您／あなた can feel heavy, overly personal or unnatural depending on locale and relationship.


Prefer the most natural sentence that keeps agency and responsibility clear.


Likewise, first-person product language is not automatically wrong. A companion, character or branded guide may speak as itself in low-stakes moments. Do not let that voice blur responsibility in errors, permissions, payments or system state.


## Plain does not mean personality-free


Choose words the intended reader can understand on the first pass.


Avoid cleverness when it makes the action, consequence or recovery harder to understand. But do not ban metaphor, humor, softness or poetic language from every surface. They can belong in ambient, editorial or emotional moments when:


- the user is not under time pressure;
- the meaning remains clear without decoding the flourish;
- localization can recreate the intent naturally rather than translate the words literally;
- the line does not become another task the user has to process.


A sentence that exists only to prove the brand has a voice has not earned its place.


## Terminology carries continuity


Use the same product concept consistently within a locale and across a flow.


If an object is “Archive” in one English surface, do not rename the same concept “Storage” elsewhere without a product reason. The localized equivalent may use a different linguistic form, but it should still point to the same concept.


Keep a terminology source of truth where the product is large enough to need one. Do not solve local awkwardness by inventing synonyms that split the mental model.


## Action labels describe the action


A control label should let the user predict what activation does.


In English this often means a concise verb or verb phrase: `Save`, `Delete project`, `Continue`.


Do not enforce “verb first” as a literal cross-language grammar rule. Traditional Chinese and Japanese should use their natural action wording and established platform conventions.


Avoid labels such as `OK`, `Yes`, `No`, `Let's go` when the consequence matters and a more specific action fits.


A destructive confirmation should make the consequence recognizable from the action area itself. `Delete project` is better English than `Yes`; the equivalent in other languages should preserve that explicit consequence naturally.


## Peer choices stay peers


Writing must not invent hierarchy the product does not have.


If several choices are genuinely equal, label them distinctly and let layout / interaction preserve that equality. Do not manufacture one “recommended-sounding” option merely because a generic UX recipe expects one primary action.


## Multi-step flows need conceptual continuity


A flow should not rename the same progression every step.


For English, choose a progression vocabulary such as `Continue` or `Next` and use it consistently where the action is genuinely the same.


Other languages should preserve the same progression meaning using their natural conventions. Do not force an English synonym rule onto Japanese or Traditional Chinese where repetition or omission works differently.


Change the label when the action changes. Consistency is not an excuse to call a final commit action `Next`.


## Links describe destination or purpose


Link text should remain understandable with limited surrounding context.


Avoid repeated generic labels such as several identical `Learn more` links when the destination matters. Add enough context to distinguish them.


Do not mechanically add “click”, “tap” or “select”. Name the destination or action unless the interaction method itself is important.


Accessible-name requirements belong to `komorebi-accessibility`; this skill owns the visible wording.


## Capitalization and punctuation belong to the language


Do not turn an English capitalization preference into a multilingual rule.


For English, sentence case is a calm, low-maintenance default when the product has no established policy. Keep the chosen policy consistent by role.


Traditional Chinese and Japanese do not use title case in the same way. Preserve their natural script conventions and punctuation. `komorebi-typography` owns rendering and line-breaking behavior.


## Settings describe the state clearly


A toggle label should make the enabled state understandable without making the sentence harder to parse.


Positive labels often work well: `Send read receipts` rather than `Don't send read receipts`.


But do not rewrite a product's established platform convention merely to satisfy a positivity rule. The test is whether the on/off meaning is immediately clear in that language.


When referencing another setting, link to it directly where possible instead of describing a fragile navigation path.


## Errors carry truth and recovery


An error should answer the parts the user actually needs:


- What did not happen or what needs attention?
- Where did it happen?
- What can the user do next, if anything?


Do not promise a recovery step that is speculative. `Try again` is useful only when retrying may reasonably succeed.


Avoid blame and decorative panic. Do not add `Oops!`, exclamation marks or jokes merely to soften failure.


Specificity must also respect international input. Never invent restrictions such as `Use only letters for your name` unless the real domain contract genuinely requires them. Names can contain spaces, hyphens, apostrophes, diacritics, Han characters, kana and other valid forms.


Good recovery examples describe the actual constraint:


| Weak | Better when true |
| --- | --- |
| Invalid password | Use at least 8 characters |
| Something went wrong | Unable to save. Check your connection and try again. |
| Invalid date | Enter a date in the format shown below |


The exact wording must match the actual validation rule. Copy must not invent a system contract.


When the same recoverable error happens repeatedly, consider whether the interaction can prevent or clarify it earlier. Redesign is sometimes the best writing fix.


## Hints arrive before the mistake when useful


If the user needs a constraint to succeed, reveal it before submission when that reduces avoidable failure.


Do not dump every validation rule under every field. Show the constraint that materially changes what the user should enter.


Phrase restrictions naturally. Positive wording can be easier to act on, but accuracy matters more than grammatical positivity.


## Empty states explain the absence, not perform a template


An empty state does not always need a title, description and CTA.


Give it only what the user needs to understand why the space is empty and what, if anything, can happen next.


Different absences need different writing:


- **First use** may need orientation and a creation action.
- **Search / filter empty** should name the condition and offer an exit when useful.
- **Intentional quiet state** may need only a short line or no prose at all when the surrounding interface already explains it.
- **Permission or sync empty** must explain the cause rather than pretending nothing exists.


Do not park persistent instructions in an empty state if they disappear the moment content arrives.


## Placeholders are not labels


A placeholder may show an example or optional hint. It disappears during input, so it cannot be the only programmatic or visible identity of a field when a label is needed.


Examples must be locale-aware. `DD/MM/YYYY`, `MM/DD/YYYY` and `YYYY/MM/DD` are not interchangeable universal date examples. Prefer a localized example or a date control where appropriate.


Form semantics belong to `komorebi-accessibility`.


## Variables belong inside complete localized messages


Do not assemble sentences from translated fragments around a variable.


Use complete messages with the localization system's plural, grammatical and interpolation support.


Numbers, names and counts may move to different positions in English, Traditional Chinese and Japanese. The translator needs the whole intent, not a bag of English fragments.


Do not treat interpolation as word substitution. English plural / possessive shape, Traditional Chinese classifiers or measure words, and Japanese particles, counters or politeness may require the surrounding sentence to change. If the localization system cannot express that grammar safely, redesign the message rather than forcing fragments together.


## Preserve useful silence


Not every surface needs helper text.


If placement, label, state and surrounding context already make the next step clear, another sentence can become an attention tax.


Before adding copy, ask what uncertainty it resolves. If the answer is none, leave the space alone.


## Before you finish


| Mistake | Fix |
| --- | --- |
| English grammar rule applied to every locale | Preserve the intent; let each language use natural structure |
| `zh-Hant` treated as one universal locale | Follow the current `zh-Hant-HK` / `zh-Hant-TW` terminology and register |
| English CTA translated literally into Japanese | Choose the natural Japanese control wording for the actual action |
| `you` / 你 / あなた repeated by default | Use the language's natural subject handling |
| Consequential action labelled `Yes` | Name the consequence naturally in that locale |
| Same product object renamed for variety | Restore the established terminology |
| Brand joke in a destructive or security message | Return to calm, explicit language |
| Error copy invents a validation constraint | State only the real contract |
| Name field restricted to “letters” | Accept the domain's real international input range |
| English capitalization policy applied to CJK | Keep capitalization language-specific |
| Every empty state gets title + body + CTA | Keep only what explains the absence and useful next step |
| Date placeholder assumes one regional format | Localize the example or use an appropriate date control |
| Sentence assembled from translated fragments | Localize one complete message with variables |
| Helper copy repeats what the interface already says | Remove it and let the interface breathe |


## Reporting


**Severity.** `HIGH` misleads the user, states the wrong consequence, invents a system rule, or hides how to recover from a consequential failure. `MEDIUM` meaningfully harms comprehension, terminology, localization, tone or flow continuity. `LOW` is isolated wording polish.


**Verification.** Source is enough for literal wording and terminology. For copy whose quality depends on rendering, truncation, layout, dynamic state or locale, inspect the real component or route that evidence to the owning layout / typography / accessibility skill. Test real EN / zh-Hant / ja strings where those locales are supported; do not infer localized quality from English alone.


For release-critical multilingual copy, inspect each supported locale directly or mark that locale `Not verified`. Do not approve Japanese or Traditional Chinese merely because the English source is strong.


**Format.** Group findings under the principle each violates, ordered by severity, one row per root cause listing every location it appears in:


| Severity | Locale | Location | Before | After | Why |
| --- | --- | --- | --- | --- | --- |


`Locale` is the inspected locale such as `EN`, `zh-Hant-HK`, `zh-Hant-TW`, `ja-JP` or `Cross-locale`. `Location` is `path/to/file:line`. `Why` names the principle and the user impact.


State the checked scope explicitly, for example `Scope checked: EN, zh-Hant-HK, ja-JP`.


End with `Block` when any `HIGH` remains, `Approve` otherwise **within the checked scope**, leaving the remaining findings in the table as work to do. Never `Approve` a locale, flow or surface you did not inspect. With nothing to report, state "No actionable writing findings" and report verification.
