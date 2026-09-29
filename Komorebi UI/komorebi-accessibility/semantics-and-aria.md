# Semantics and ARIA

Native elements, landmarks, names, states and the ARIA contracts that custom widgets must keep.

## Native first

Use the native element whose semantics and behavior match the job.

| Element | Use for |
| --- | --- |
| `<a href>` | Navigation or destination changes |
| `<button>` | Actions, toggles, disclosure, submission |
| native form controls | Inputs and choices |
| semantic landmarks | Page regions and navigation |

A clickable `div` has no useful keyboard or control semantics by default.

ARIA should fill semantic gaps, not repaint native HTML with roles it already has.

## A role is a contract

When you add a custom interactive role, you also take responsibility for:

- keyboard behavior;
- focus behavior;
- accessible name;
- state and value;
- the correct relationship to owned or controlled content.

Do not add `role="menu"` to ordinary site navigation or `role="button"` to an actual button.

Never put `aria-hidden="true"` or presentation semantics on a subtree that still contains focusable controls.

## Accessible names

Prefer names derived from visible content and native labels.

Accessible naming can also come from `aria-labelledby`, `aria-label`, `alt` and other native mechanisms depending on the element.

Do not rely on an imagined universal precedence list as a substitute for checking the browser's computed accessible name.

Important principles:

- every interactive control has a useful name;
- the visible label is included in the accessible name where WCAG Label in Name applies;
- icon-only controls receive a name while the decorative icon itself stays hidden from the accessibility tree;
- `aria-labelledby` / `aria-describedby` references resolve to real elements;
- names are localized with the visible UI.

```tsx
<button>
  <TrashIcon aria-hidden="true" />
  Delete
</button>

<button aria-label="Close">
  <CloseIcon aria-hidden="true" />
</button>
```

For EN / Traditional Chinese / Japanese, keep the programmatic name semantically aligned with the displayed language. Mark language changes when pronunciation needs to switch.

## Button vs link

A visual treatment does not decide semantics.

A button that navigates should usually be a link styled as required. A link that only mutates local state should normally be a button.

Native semantics preserve platform behavior such as opening links in a new tab or using standard activation keys.

## Landmarks and headings

Use landmarks and headings to expose the structure users need for navigation.

Multiple landmarks of the same type may need labels to distinguish them.

Do not report "more than one h1" or a skipped heading level as an automatic WCAG failure without showing the concrete structural problem. Heading markup should reflect the document hierarchy; CSS owns the visual size.

A meaningful document title should track the current context.

## State attributes

Expose interactive state where the native element does not already do it.

Examples:

- `aria-expanded` for a disclosure that controls hidden content;
- `aria-pressed` for a toggle button;
- `aria-selected` inside patterns that define selection;
- `aria-current` for the current item in a set when appropriate;
- `aria-invalid` for invalid form fields.

Do not add ARIA states because the attribute name sounds related. Use the state defined for the actual semantic pattern.

## Disabled and unavailable states

Native `disabled` is appropriate when a native control is genuinely unavailable and removing it from the sequential tab order matches the task.

`aria-disabled="true"` only exposes a disabled state; it does not block activation, change focusability or style the element. Use it when keeping the control discoverable or focusable is intentional, then block the actual activation in code and explain the reason where needed.

Do not treat either native disabled or enabled submit as a universal accessibility rule. Ask what the user needs to understand and do next.

Avoid putting essential explanations only in a tooltip attached to a natively disabled control, since that control may not be reachable by keyboard or touch in the way the tooltip expects.

## Decorative duplication

If sighted users see an icon, flourish or duplicated word solely as visual reinforcement, do not make screen-reader users consume it again.

Conversely, `aria-hidden` must not erase information or controls that exist only once.

The goal is equivalent meaning, not identical output channel by channel.
