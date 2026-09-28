# Removed signals

What to notice on the `-` side of a change and where to route the question.

A removed signal is **evidence to inspect**, never a finding by itself.

A mature interface often improves by deleting wrappers, borders, shadows, animation, labels or duplicated cues. The question is whether the removal also removed meaning, access, hierarchy, state, continuity or recoverability.

## Accessibility leads

| Removed | Owner | Check |
| --- | --- | --- |
| `aria-label`, `aria-labelledby`, `aria-describedby`, `aria-live`, role metadata | `komorebi-accessibility` | Accessible name / description / announcement still exists |
| `alt`, `<label>`, `for`, table associations | `komorebi-accessibility` | Programmatic relationship still exists |
| Native semantic element replaced by generic element | `komorebi-accessibility` | Keyboard and assistive behavior survived |
| `:focus-visible`, focus ring, tabindex | `komorebi-accessibility` | Keyboard users still get reachability and visible focus |
| `prefers-reduced-motion`, `prefers-contrast` handling | `komorebi-accessibility` | User preferences are still respected |

## Layout leads

| Removed | Owner | Check |
| --- | --- | --- |
| Logical property replaced by physical left / right | `komorebi-layout` | Direction-aware geometry was lost |
| Container / min-size / wrapping constraint | `komorebi-layout` | Component still survives its supported containers |
| Safe-area handling | `komorebi-layout` | Controls remain reachable around platform chrome |
| Spatial continuation / disclosure cue | `komorebi-layout` | Hidden content remains discoverable |

Removing a separator, card wrapper or extra margin is not a regression when grouping remains clear or becomes clearer.

## Typography and localization leads

| Removed | Owner | Check |
| --- | --- | --- |
| `lang`, `dir` | `komorebi-typography` | Language / direction metadata still exists at the correct boundary |
| `line-break`, `overflow-wrap`, `text-wrap`, `line-clamp` | `komorebi-typography` | Real EN / zh-Hant / ja strings still wrap correctly where relevant |
| `text-autospace` or mixed-script spacing rule | `komorebi-typography` | CJK / Latin boundaries still read naturally |
| `font-variant-east-asian`, ruby or emphasis handling | `komorebi-typography` | Language-specific glyph / annotation behavior still works |
| tabular / numeric feature | `komorebi-typography` | Changing numbers still align where alignment matters |
| font fallback / family coverage | `komorebi-typography` | Required glyphs still render in the intended family |

A removed text rule is not automatically wrong if the browser / font / new representation now provides the same behavior more naturally.

## Color leads

| Removed | Owner | Check |
| --- | --- | --- |
| Semantic color token replaced by literal / primitive | `komorebi-colors` | Role ownership and theming seam survived |
| Foreground / background token changed | `komorebi-colors` | Measure the rendered pair when contrast is required |
| Status color cue removed | `komorebi-colors` + `komorebi-accessibility` | Meaning still has a persistent non-color carrier |
| Theme variant removed | `komorebi-colors` | Supported appearance still has intentional roles and contrast |

Removing decorative atmospheric color is not a regression when it carried no semantic responsibility.

## UI leads

| Removed | Owner | Check |
| --- | --- | --- |
| Persistent selected / active visual cue | `komorebi-ui` | State remains visible after motion stops |
| Icon variant / currentColor behavior | `komorebi-ui` | Icon still participates in state and theming naturally |
| Transition or motion | `komorebi-ui` | Causality / continuity was lost, not merely decoration |
| Surface / edge treatment | `komorebi-ui` | Object identity or separation still reads without it |
| image crop / focal positioning rule | `komorebi-ui` + `komorebi-layout` | Subject and quiet text region remain intact |

Deleting a shadow, border, press scale, icon blur, stagger or entrance animation is often simplification. Route it only when something the user needs to understand disappeared with it.

## Writing leads

| Removed | Owner | Check |
| --- | --- | --- |
| User-facing label / instruction / recovery hint | `better-writing` | Meaning or recoverability was lost |
| Empty / error state copy | `better-writing` | The state still tells the user what happened and what can happen next |
| Translation catalogue entry | `better-writing` / localization owner | Supported locale still has the required message |

Shorter copy is not a regression when it preserves the same meaning with less burden.

## Equivalent replacements

These commonly clear a removal lead:

- ARIA replaced by correct native semantics;
- explicit label replaced by visible text correctly referenced;
- custom focus ring replaced by another conforming visible focus treatment;
- physical layout property replaced by logical property;
- raw color replaced by a semantic token;
- custom CJK spacing replaced by language-aware browser behavior;
- animated state change replaced by a persistent state cue;
- card / border removed while grouping remains clear through space;
- shadow removed while depth is still established through overlap / value / material;
- string moved into localization rather than deleted;
- visual asset moved or recomposed rather than removed.

## Reading the removed side

Search deleted lines to find leads, then reopen the full hunk and relevant surrounding source.

Never let a grep pattern become a verdict engine.

The right question after finding a removal is:

**What responsibility did this line carry, and where does that responsibility live now?**

If the answer is “somewhere better”, there is no regression.
