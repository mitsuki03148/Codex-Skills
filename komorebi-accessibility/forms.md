# Forms

Labels, input purpose, validation, submission, autofill and multilingual text entry.

## Labels

Every form control needs an accessible name.

Prefer visible labels associated through `<label for>` or a wrapping `<label>`.

A placeholder is not a replacement for a label. It can provide an example or format hint when that information remains useful after typing begins.

```html
<label for="email">Email</label>
<input id="email" type="email" autocomplete="email" />
```

For checkbox and radio controls, make the visible text part of the target where possible so there is no precision-only dead zone.

Required state should be conveyed programmatically and visibly when users need to know it before submission.

## Input purpose

Use the native input semantics that fit the data.

Relevant fields about the user should expose appropriate `autocomplete` tokens where WCAG 1.3.5 applies.

Use suitable `type`, `inputmode` and `name` values to work with mobile keyboards, autofill and password managers.

Common examples:

| Field | Useful configuration |
| --- | --- |
| Email | `type="email" autocomplete="email"` |
| Phone | `type="tel" autocomplete="tel"` |
| Login | `autocomplete="username"` + `current-password` |
| New password | `autocomplete="new-password"` |
| One-time code | text input with `autocomplete="one-time-code"` where supported |
| Card number | text semantics with the appropriate autocomplete and numeric input mode |

Do not replace text semantics with `type="number"` for values that are identifiers rather than quantities.

## Do not fight user tools

Do not block paste into credentials or codes.

Stay compatible with password managers, browser autofill, text expansion and assistive input.

For Chinese and Japanese input methods, do not validate, transform, submit or reject text while an IME composition is still in progress. Composition text is not yet the committed value.

Do not filter ordinary free-text characters as the user types simply to force one expected format. Normalize and validate at a moment that does not fight entry.

## Validation timing

There is no single accessible timing model for every form.

Possible patterns include:

- validation on submit;
- validation after leaving a field;
- restrained validation after committed input where the feedback does not constantly interrupt the user.

Whatever timing the product uses:

- error messages identify the problem and recovery;
- `aria-invalid` reflects the invalid field state when appropriate;
- `aria-describedby` can associate inline help or error text with the field;
- color is not the only error cue;
- repeated announcements do not fire on every keystroke.

After an unsuccessful submit, move focus or provide an error summary when doing so helps the user recover orientation. Focusing the first invalid field is often useful, but not a law for every multi-step or complex form.

## Submit availability

Do not disable or enable submit by ideology.

Keeping submit enabled can be useful when submission is how the user discovers validation problems.

Disabling can be appropriate when the action genuinely cannot run yet, provided users can still understand:

- that the action exists;
- why it is unavailable;
- what must change to enable it.

Do not hide the only recovery explanation behind an unreachable disabled control.

When a request begins, prevent accidental duplicate submission in a way that preserves the button's identity and communicates progress.

## Submission feedback

Keep the action recognizable while busy. A spinner can accompany the label rather than replacing all meaning.

Success updates can use a polite announcement when the visual change would otherwise be missed.

Field-specific errors should be associated with their fields. Use urgent alert behavior only when the error is genuinely urgent and not already conveyed by focus or field association.

## Preserve user work

Do not lose entered values, focus or error context because of hydration, rerendering, validation or navigation.

Warn about unsaved changes when loss would be meaningful and the project has a workflow for that warning.

Keyboard submission shortcuts beyond native form behavior are product conventions, not accessibility defaults. If the product adds one, keep the normal visible submission path too.
