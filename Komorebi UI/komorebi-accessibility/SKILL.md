---
name: komorebi-accessibility
description: Helps interfaces meet accessibility standards and work reliably across keyboard, screen reader, zoom, touch, motion-preference and multilingual use.
---

# Accessibility

Accessibility is not an extra visual layer. It is whether the same interface remains understandable and operable when someone reads, sees, points, types, zooms, listens or moves through it differently.

Prefer the platform. Native elements already carry semantics, keyboard behavior and browser integration that custom rebuilds have to recreate.

Write fixes in the project's own system. Keep accessibility requirements separate from optional best practices and from aesthetic preferences. A quiet interface can remain quiet; accessibility does not require adding visual noise when structure, semantics and existing affordances already communicate the state.

WCAG 2.2 is the conformance baseline for the web unless the project names another target. ARIA Authoring Practices describe interaction patterns for custom widgets; they are guidance for implementing the promised behavior, not a substitute for native HTML.

Contrast measurement belongs to `komorebi-colors`. Text rendering and language-aware typography belong to `komorebi-typography`. Spatial adaptation belongs to `komorebi-layout`. Motion styling belongs to `komorebi-ui`; this skill owns whether motion remains accessible. `komorebi-mobile-ux` owns embodied comfort, grip / regrip, reach direction and repeated finger travel; target-size conformance and motor-accessibility requirements stay here.

## Review by modality, not by checklist volume

Start from the real task and inspect only the modalities the surface actually exposes.

At minimum for an interactive web flow:

1. **Keyboard** — can the task complete without pointer input, in a logical order, with visible focus?
2. **Accessibility tree / screen reader** — do controls expose useful names, roles, values and states?
3. **Resize / reflow** — does content survive enlargement and narrow equivalent widths?
4. **Pointer / touch** — are targets operable without precision or overlapping hit regions?
5. **Motion / timing** — where the interface moves or acts on a timer, can user preferences and required controls be respected?

For multilingual EN / Traditional Chinese / Japanese surfaces, also verify the language boundaries, accessible names and announcements in the language actually rendered.

Do not manufacture findings in a modality the component does not use.

## Native elements first

Use native semantics when they match the job:

- `<button>` for actions;
- `<a href>` for navigation;
- native form controls for input;
- `<dialog>` where its browser behavior fits the modal interaction.

A custom role is a promise to reproduce the corresponding keyboard model, state and semantics.

No ARIA is better than incorrect ARIA. See [semantics-and-aria.md](semantics-and-aria.md).

## Focus must be visible and reachable

WCAG 2.2 AA requires a visible keyboard focus indicator and requires focused components not to be entirely hidden by author-created content.

Prefer the browser's focus indicator unless the design has a verified project treatment. If you customize it, verify the rendered focused state against the surfaces it actually crosses, including forced-colors mode.

A 2 CSS-pixel perimeter with 3:1 change-of-contrast is a useful robust design target and corresponds to WCAG 2.2 Focus Appearance at Level AAA; do not report its absence as an AA failure by itself.

Never remove focus styling without an effective replacement. Sticky headers, footers and overlays must not completely cover the focused component.

See [focus-and-keyboard.md](focus-and-keyboard.md).

## Keyboard behavior follows the control

Every pointer-operable task needs an equivalent keyboard path unless the interaction is inherently path-dependent.

Native controls already implement their normal keyboard behavior. Custom composite widgets follow the relevant ARIA APG pattern rather than a home-grown universal key map.

Use natural DOM order. Positive `tabindex` is almost never the answer; fix structure instead. Roving tabindex belongs to composite widgets that need one Tab stop.

## Modal focus follows the task

A modal keeps interaction inside itself while open and returns focus to a sensible place when it closes.

Initial focus is contextual:

- the first useful field or action for a simple dialog;
- a static heading or paragraph with `tabindex="-1"` when users need to perceive substantial structured content first;
- the least destructive action for an irreversible confirmation when that is the safer workflow.

Do not force "first focusable element" as a universal rule.

Prefer native `<dialog>` with `showModal()` where it fits. For custom modal patterns, implement the full semantics, keyboard containment and background inertness intentionally.

## Target size: conformance and comfort are different

WCAG 2.2 SC 2.5.8 Level AA uses a 24×24 CSS-pixel minimum target size with defined exceptions, including spacing, equivalent controls, inline targets, user-agent controls and essential presentations.

Larger targets are usually easier to operate. Around 44×44 CSS px is a useful touch-oriented usability target, not the WCAG AA floor.

Keep visual size and hit size separate when needed. Extended targets must not create ambiguous overlapping activation areas.

A large compliant target can still sit in a physically expensive place. For repeated phone / tablet touch actions, route placement and regrip questions to `komorebi-mobile-ux`; do not turn a 44px usability target into a claim that the action is ergonomically well placed.

See [hit-areas.md](hit-areas.md).

## Labels, names and forms

Every form control needs an accessible name. Prefer visible labels and native associations; a placeholder is not a label.

Use appropriate `autocomplete`, `type`, `inputmode` and `name`. Stay compatible with password managers, one-time-code autofill, paste and IME composition.

Validation should be discoverable without forcing one timing model on every form:

- errors identify the field and explain recovery;
- `aria-invalid` and `aria-describedby` connect the programmatic state and message where appropriate;
- a submission error can move focus or provide a summary when that best restores orientation;
- validation during typing must not fight IME composition or constantly interrupt screen-reader users.

A disabled submit button is not automatically inaccessible and an enabled one is not automatically better. Preserve discoverability: if the action is unavailable, the user should be able to understand why and how to make it available. See [forms.md](forms.md).

## Accessible names should belong to the visible language

Visible label text should normally contribute to the accessible name. Keep WCAG Label in Name intact for voice users.

For mixed EN / zh-Hant / ja:

- mark language changes with `lang` when pronunciation needs to change;
- keep accessible names semantically aligned with visible copy;
- do not expose an unrelated English-only accessibility label on a Chinese or Japanese control simply because it is convenient to author;
- keep brand names, identifiers and code tokens intact where translation would corrupt them.

## Color is never the only signal

Status and state need a redundant cue when color alone would carry the meaning.

Use the owning color and accessibility requirements together: this skill decides which contrast requirement applies; `komorebi-colors` measures the actual rendered pair.

Do not make "accessible" UI louder than necessary. One clear redundant cue is enough when it reliably carries the state.

## Reduced motion: respect the preference, preserve meaning

Honor `prefers-reduced-motion` for non-essential motion and vestibular-risk movement. Prefer removing large spatial movement, parallax and decorative looping while keeping the final state obvious.

Reduced motion does not require erasing all feedback. Instant state changes, small non-vestibular cues and necessary progress indication can remain when appropriate.

WCAG's five-second rule is specific to automatically starting moving, blinking or scrolling content that continues for more than five seconds while presented alongside other content. Auto-updating information has its own control requirement and no five-second exemption. Do not generalize that rule to every toast or timer.

See [motion-and-zoom.md](motion-and-zoom.md).

## Timed and transient UI must not make the user race

When UI disappears, changes automatically or contains a time-limited action, inspect the actual accessibility requirement before choosing a duration.

- use platform accessibility timeout recommendations where available;
- important information should remain available through a persistent or recoverable path;
- transient controls need enough time to perceive, understand, reach and operate;
- a short redundant success status can be auto-dismissed more freely than a consequential action or error;
- do not turn one WCAG time threshold or one platform example into a universal toast duration.

This skill owns timing accessibility, Reduce Motion and applicable WCAG / platform requirements. `komorebi-mobile-ux` owns the broader human interaction timing question: whether read + decide + reach + act is comfortable in the actual phone / tablet flow.

## Dynamic content should announce only what matters

Use the quietest mechanism that preserves orientation:

1. if focus naturally moves to the new content, that focus change may be enough;
2. field-specific help or validation can be associated with the field;
3. routine untied updates can use a polite status region;
4. urgent untied errors can use an alert.

Do not make every UI update a live-region announcement. Over-announcing is another accessibility failure mode because it interrupts the user's current task.

Repeated polite updates often work more reliably through a stable region that exists before its text changes. Test important announcements with the screen readers the project actually supports.

See [screen-readers.md](screen-readers.md).

## Images and media: describe purpose, not pixels

Decorative or redundant images use empty alternative text when represented by `<img>`. Informative images communicate the information they add. Functional images communicate the action or destination when the image itself supplies the control's accessible name.

If a button or link already has a visible or programmatic name, its decorative icon or image should not duplicate that name.

Complex graphics need equivalent information at the level required to understand the task, not an exhaustive narration of every mark.

## Structure supports orientation

Use semantic regions, headings and landmarks so users can navigate by structure.

Do not turn conventions such as "exactly one h1" or "never skip a heading level" into automatic WCAG findings. Report the concrete orientation or comprehension problem when the structure becomes misleading.

Repeated blocks before the main content may justify a skip link. Anchored targets need enough scroll offset to remain visible below sticky chrome.

## Resize and reflow

WCAG 2.2 Resize Text requires text to be enlargeable to 200% without loss of content or functionality, subject to its exceptions.

WCAG Reflow requires vertically scrolling content to work without two-dimensional scrolling at a width equivalent to 320 CSS px, except for content that genuinely requires a two-dimensional layout.

Do not confuse the two checks. A 320px reflow test does not replace the 200% text-enlargement check.

Use flexible containers and avoid fixed text heights that clip translated or enlarged content.

## Before you finish

| Mistake | Fix |
| --- | --- |
| Best practice reported as a WCAG AA failure | Name the actual conformance criterion or label it guidance |
| Custom focus ring judged only by token name | Inspect the rendered focused state and adjacent surfaces |
| 2px Focus Appearance rule treated as AA | Keep visible focus at AA; treat 2px/3:1 as AAA or a stronger project target |
| 44px target reported as the WCAG AA minimum | Use 24px + exceptions for AA; keep 44px as a usability target |
| Every motion removed under reduced motion | Remove or replace problematic motion while preserving useful state feedback |
| Five-second moving-content rule applied to every toast | Evaluate timed content under the criterion that actually applies |
| Submit disabled/enabled by dogma | Preserve task clarity, error recovery and discoverability |
| Every update sent to a live region | Announce only information the user would otherwise miss |
| English accessibility labels left on zh-Hant / ja controls | Align accessible names with the visible language and mark language changes |
| Visually quiet control made semantically quiet too | Keep the visual restraint; restore the missing name, role, state or keyboard path |

## Reporting

**Severity.** `HIGH` prevents a task, hides required content from assistive technology, causes a systemic keyboard or naming failure, or loses user work. `MEDIUM` meaningfully harms orientation, comprehension or efficiency. `LOW` is isolated polish or best-practice improvement.

**Verification.** State exactly what was inspected. Separate source inspection, browser keyboard testing, accessibility-tree / screen-reader testing, zoom / reflow checks, pointer / touch checks and automation. A check you did not run is `Not verified`, not a failure.

**Format.** Group findings under the principle each violates, ordered by severity, one row per root cause listing every confirmed location:

| Severity | Location | Before | After | Why |
| --- | --- | --- | --- | --- |

`Location` is `path/to/file:line`. `Why` names the requirement or principle and the user impact.

End with `Block` when any `HIGH` remains and `Approve` otherwise, but never claim coverage you did not inspect. With nothing actionable, state "No actionable accessibility findings" and report verification.
