# Focus and keyboard

Visible focus, keyboard order, modal focus management, skip links and custom-widget interaction.

## Separate the focus requirements

WCAG 2.2 has several related but different requirements.

### Focus Visible — Level AA

Keyboard-operable interfaces need a mode where the focus indicator is visible.

The criterion does not prescribe one shape or a mandatory 2px outline.

Prefer the browser indicator unless the project has a verified custom treatment.

```css
:focus-visible {
  outline-offset: 2px;
}
```

### Focus Not Obscured (Minimum) — Level AA

When a component receives keyboard focus, author-created content must not entirely hide that component.

Sticky headers, bottom bars, drawers and persistent overlays are common failure sources. Use layout, scroll padding or interaction design so focus remains discoverable.

### Focus Appearance — Level AAA

WCAG 2.2 Focus Appearance defines stronger minimum area and contrast expectations. A solid 2 CSS-pixel perimeter is a simple way to satisfy its area requirement, and the changed pixels need the required contrast between focused and unfocused states.

Treat this as AAA unless the project explicitly adopts it as its own stronger standard. Do not report the lack of a 2px perimeter as an AA failure by itself.

## Custom focus styling

A custom focus indicator has to work on the real surface.

Check:

- default and selected surfaces;
- light and dark appearances;
- images or gradients behind the control;
- forced-colors mode;
- sticky or overlapping UI that can cover it.

Do not assume `currentColor`, the brand hue or a token name automatically produces sufficient visibility.

Never remove focus styling without an effective replacement.

## Natural tab order

Prefer DOM order that already matches the task.

- `tabindex="0"` joins the natural sequential order when a custom element genuinely needs to be focusable.
- `tabindex="-1"` allows programmatic focus without adding a Tab stop.
- positive tabindex values create a second manual navigation order and should be avoided; repair DOM order instead.

Custom composite widgets may use roving tabindex so the widget occupies one Tab stop and arrow keys move inside it.

## Keyboard behavior belongs to the widget

Native controls already have expected keyboard behavior.

For custom widgets, follow the relevant ARIA APG pattern rather than one global key recipe.

Common patterns include:

| Widget | Typical behavior |
| --- | --- |
| Modal dialog | Tab / Shift+Tab remain inside; Escape closes |
| Tabs | Arrow keys move among tabs; activation can be automatic or manual |
| Menu | Arrow keys navigate; Escape closes and returns focus appropriately |
| Disclosure | Button toggles expanded state with its native activation keys |
| Combobox / listbox | Use the APG pattern appropriate to the chosen interaction model |

A role is a promise of the corresponding interaction.

Do not add custom keyboard shortcuts where the platform or native element already supplies the expected behavior.

## Modal focus is contextual

When a modal opens, focus moves inside it, but not always to the first interactive control.

Good initial focus can be:

- the first useful field or action in a short simple dialog;
- a static heading or first paragraph with `tabindex="-1"` when substantial structured content needs to be perceived first;
- the least destructive action in an irreversible confirmation;
- another task-specific control when that is the most logical starting point.

On close, normally return focus to the invoking control. If it no longer exists or the workflow logically advances elsewhere, move focus to the next sensible point.

Prefer native `<dialog>` and `showModal()` when the browser behavior matches the product. A custom modal must implement modal semantics, contained keyboard navigation, focus placement, restoration and background inoperability deliberately.

Do not put focus on the dialog container merely because it is easy; a large focused container can be difficult to perceive and can produce poor screen-reader output.

## Skip links and anchored content

When repeated navigation or chrome precedes the main content, a skip link can provide a direct path to `<main>`.

Hide it visually until focus without removing it from the accessibility tree.

Sticky headers can cover anchored destinations. Use `scroll-margin-*` or an equivalent layout solution so the target remains visible.

## Focus-within

Use `:focus-within` where a composite visual surface should indicate that an inner control owns focus.

Do not make the wrapper itself an extra focus stop unless it has an independent interactive purpose.

## Focus and visual quietness

A focus indicator may be quiet in its resting absence and clear only when needed.

Accessibility does not require permanent high-contrast decoration around every control.

When focus arrives, however, the interaction point must become perceivable. Do not trade that moment away to preserve an immaculate static composition.

## SPA route changes

Client-side navigation may leave focus stranded in the old view.

When route changes substantially replace the current context:

- update the document title appropriately;
- move focus when needed to restore orientation, often to the new main heading or main region;
- preserve logical back/forward scroll behavior.

Do not force focus movement on every tiny in-place state update. Use it when the user's context actually changed.
