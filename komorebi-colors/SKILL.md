---
name: komorebi-colors
description: Helps build, review and evolve color systems across UI, illustration and mixed English / Traditional Chinese / Japanese products. Covers semantic tokens, palette structure, formats, gamut, contrast and restrained color composition.
---

# Colors

Color should make the interface easier to read before it makes the interface more colorful.

A strong color system separates three different jobs:

1. **semantic UI color** — text, surfaces, controls, states and feedback;
2. **atmospheric / material color** — paper, room, light, environment and other persistent mood;
3. **illustrative color** — characters, objects, images and decorative artwork.

Do not force all three through the same rules. Semantic colors need stable meaning and measurable contrast. Atmospheric and illustrative colors may repeat, overlap and shift naturally as long as they do not impersonate semantic UI signals.

Never report a contrast value you did not measure. Never estimate a color you can compute. When legal or standards conformance matters, use the contrast method required by that standard.

Contrast requirements belong to `better-accessibility`. Surfaces, shadows and motion belong to `better-ui`. Spatial emphasis and composition belong to `komorebi-layout`.

## Start from the role, not the swatch

Before changing a color, ask what job it owns.

A value that is beautiful in isolation can still be wrong because it is:

- too loud for a supporting role;
- too weak for text;
- too close to a status hue;
- pretending to be interactive;
- fighting the material or image behind it;
- visually correct in light mode but wrong in dark mode.

Color review begins with role and context, not hue preference.

## Match the project's system

Reuse the project's tokens and notation when they are coherent.

Do not introduce `oklch()` into one component of a hex codebase merely because it is a better editing space. A consistent existing system is usually cheaper to reason about than a technically newer notation used in one corner.

For a genuinely new system, OKLCH is a strong working space because lightness, chroma and hue are easier to reason about perceptually. Production notation still follows the project's browser matrix and conventions. See [color-formats.md](color-formats.md).

## Keep the palette small, but not sterile

Most interfaces need:

- one neutral / environmental family;
- one accent family;
- only the status families the product actually uses.

That is a starting structure, not a ban on every other color in the product.

Illustration, photography, rooms, charts and category systems may legitimately contain more hues. The important question is whether those hues are carrying interface semantics or simply belonging to the world.

A color earns a semantic token when the product needs to remember its job across themes, states or components.

## Neutrals are the field

The neutral family carries most of the interface and therefore sets the atmosphere more strongly than the accent.

Pure gray is valid. So are low-chroma warm, cool or slightly green / blue neutrals when the product needs a material or environmental tone.

For a quiet Japanese-influenced visual language, consider neutrals as materials rather than empty gray:

- warm ivory rather than forced pure white;
- soft charcoal rather than automatic pure black;
- misted green-gray, ink blue-gray or muted brown when the world calls for it.

These are aesthetic options, not accessibility exemptions. Essential text and controls still need to pass their required contrast.

## Semantic colors keep stable meaning

Semantic UI color should not change meaning casually.

If the accent means interactive, using the same semantic accent treatment on static prose can mislead. If danger is red in one flow, do not reuse the same treatment for a benign promotional badge in another.

This does **not** mean the same hue can never appear elsewhere in illustration or atmosphere. Context, shape and role matter. The restriction is on semantic signaling, not on the existence of a hue in the world.

See [color-usage.md](color-usage.md).

## Primary emphasis follows product truth

Do not manufacture one dominant colored action when the product presents genuine peers.

When one next action is truly primary, a filled accent treatment can carry that hierarchy.

When choices are peers, preserve their equality. Use color, surface, placement or outline treatment consistently rather than inventing a fake winner.

Selected, active and category states may also use color without becoming “the primary action”.

## Build ramps for decisions, not completeness

A ramp exists so product roles have reliable values.

Do not generate eleven or twelve steps merely because a framework has eleven or twelve names. Generate enough values to cover the roles the system actually needs, while preserving the framework's conventions when the project already depends on them.

See [palette-structure.md](palette-structure.md).

## Lightness structure first; hue may breathe

A useful ramp normally has a clear perceptual lightness order.

Constant hue is a clean system default, especially for semantic UI ramps. But it is not an aesthetic law.

A small, intentional hue shift can make neutrals and material palettes feel more natural — for example, a warm paper family that becomes slightly cooler in shadow, or a green-gray family that loses green toward its darkest ink step.

Controlled hue drift is acceptable when:

- the family still reads as one family;
- adjacent roles remain distinguishable;
- status / accent semantics do not collide;
- the drift is intentional and documented rather than accidental interpolation noise.

See [palette-generation.md](palette-generation.md).

## Chroma should know when to leave

High chroma attracts attention.

Reserve it for things that genuinely need presence: an accent, a status, a focal illustration detail, a temporary highlight.

Persistent surfaces, large areas and frequent controls often feel calmer when chroma steps down.

Dark mode especially needs care: a color that feels calm on warm white can feel electric on near-black.

## Black and white are tools, not defaults or taboos

Off-white and off-black often create a softer material field and preserve hue identity. That makes them useful defaults for quiet compositions.

Pure white and pure black remain valid when the product, artwork or contrast requirement needs them. Do not avoid them on principle.

## Gradients should have a job

A gradient can express light, depth, state or material transition. It should not appear merely because a flat fill feels “too simple”.

For restrained interfaces:

- shallow lightness / temperature shifts are often enough;
- large rainbow sweeps need a real semantic or illustrative reason;
- gradients behind text need worst-case contrast inspection;
- if a gradient is only hiding an otherwise weak composition, fix the composition first.

Interpolation space changes the look. See [color-usage.md](color-usage.md).

## Mixed EN / Traditional Chinese / Japanese

Color meaning is not universal, and language alone does not determine color meaning.

For EN / zh-Hant / ja products:

- do not assume a semantic convention transfers unchanged between regions;
- verify finance, alert and status conventions against the actual locale and domain;
- keep icon / label / shape support so color is never the sole carrier of meaning;
- test real localized screens, because typography density can change how much visual weight a color block appears to have.

Do not “make it Japanese” by adding sakura pink, red seals, indigo, gold or washi beige without a role. Cultural tone should come from the whole composition, not a symbolic swatch list.

## Measure the rendered pair

Measure foreground against the background it actually renders on.

Opacity, overlays, images, gradients and backdrop filters change the effective pair. A token-to-token check is insufficient when compositing changes the result.

WCAG 2.2 contrast is the conformance gate when WCAG 2.x applies. APCA may be used as a supplemental design metric only when the project explicitly adopts it; it does not replace WCAG 2.2 conformance. See [contrast.md](contrast.md).

## Before you finish

| Mistake | Fix |
| --- | --- |
| Semantic UI rules applied to illustration / ambient color | Separate semantic, atmospheric and illustrative roles |
| Accent hue used decoratively in a way that makes static content look interactive | Recompose or change the semantic treatment; do not ban the hue from artwork |
| One giant filled CTA invented for peer choices | Preserve peer hierarchy |
| Every screen gets another accent hue | Ask what new semantic distinction the hue owns |
| Constant-hue ramps treated as mandatory | Keep them for clean systems; allow controlled drift when material identity benefits |
| Hue drift appears accidentally across a semantic ramp | Normalize or document an intentional trajectory |
| Quiet palette achieved by low-contrast essential text | Restore required contrast; softness is not a readability tax |
| Pure black / white banned by style doctrine | Use or avoid them according to role, material and contrast |
| Large gradient added to make an empty layout feel designed | Fix hierarchy / composition first |
| Light mode palette mechanically reversed into dark mode | Reassign roles, reduce glare / chroma where needed and remeasure |
| Raw value used where a semantic token exists | Reuse the role token |
| Primitive token applied directly in a component | Point a semantic token at the primitive |
| Status hue confused with accent | Separate the semantic treatments and test side by side |
| Locale convention inferred from language alone | Verify the actual region, domain and product convention |
| P3 / modern syntax added with no browser-matrix decision | Follow the project's support policy and provide fallback where required |

## Reporting

**Severity.** `HIGH` makes content unreadable, hides required state, or uses semantic color in a way that materially misleads. `MEDIUM` is a noticeable token, theme, gamut, localization or hierarchy failure. `LOW` is isolated polish.

**Verification.** Without a browser: inspect token roles, declared values, theme mappings and supported color syntax. With one: inspect the actual rendered background, compositing, images / gradients and all supported appearances. Measure required contrast against the rendered pair. Test important localized surfaces in EN / zh-Hant / ja where color hierarchy interacts with different text density. Report every check you could not run as `Not verified`.

**Format.** Group findings under the principle each violates, ordered by severity, one row per root cause listing every location it appears in:

| Severity | Location | Before | After | Why |
| --- | --- | --- | --- | --- |

`Location` is `path/to/file:line`. `Why` names the principle and user impact.

End with `Block` when any `HIGH` remains, `Approve` otherwise. Never `Approve` coverage you did not inspect. With nothing to report, state "No actionable color findings" and report verification.
