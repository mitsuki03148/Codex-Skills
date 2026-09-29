# Motion and zoom

Reduced-motion preference, automatically moving content, timing, resize and reflow.

## Reduced motion

Respect `prefers-reduced-motion`.

A motion-safe default can be useful in new code:

```css
.card {
  /* final static state */
}

@media (prefers-reduced-motion: no-preference) {
  .card {
    transition: transform 180ms ease-out;
  }
}
```

In an existing motion system, targeted reduced-motion overrides may be less disruptive than introducing a second architecture. Follow the project's established mechanism when it works.

Reduced motion does not mean "remove every transition".

Prioritize removing or replacing:

- parallax;
- large spatial travel;
- zooming or scaling that can trigger vestibular discomfort;
- decorative looping movement;
- auto-advancing motion that competes for attention.

Often safe to retain, when useful:

- instant state changes;
- stable focus indication;
- restrained opacity changes;
- progress indication whose meaning remains clear.

The owning UI skill decides the visual replacement. Accessibility decides that the reduced state remains usable and understandable.

## Automatically moving or updating content

Keep WCAG 2.2.2's actual scope intact.

For moving, blinking or scrolling information that:

- starts automatically;
- lasts more than five seconds; and
- appears in parallel with other content,

provide a way to pause, stop or hide it unless the movement is essential.

Auto-updating information presented in parallel with other content requires a way to pause, stop, hide or control the update frequency unless essential; there is no five-second exemption for auto-updating content.

Do not convert this into a blanket rule that every toast must last at least five seconds.

## Timed messages and actions

Ask what information would be lost when the timer ends.

Low-stakes confirmations may disappear automatically when users do not need them to proceed.

Errors, undo opportunities, required actions and information users may need time to perceive should remain available or have an equivalent persistent path.

Timing requirements can also fall under other WCAG criteria depending on the interaction. Evaluate the actual timer rather than applying one universal duration.

## Autoplay media

Autoplaying audio has its own WCAG requirements.

Moving or autoplaying visual media may also fall under Pause, Stop, Hide when it meets that criterion's conditions.

Regardless of the minimum standard, visible playback controls are often the clearest product choice when media continues independently of the user's current task.

## Resize Text

WCAG 1.4.4 requires text, except captions and images of text, to be resizable up to 200% without loss of content or functionality, subject to the criterion's conditions.

Do not fake this check by only narrowing the viewport.

Verify that users can actually obtain the required enlargement.

## Reflow

WCAG 1.4.10 is a separate check.

For vertically scrolling content, content must work without loss of information or functionality and without requiring two-dimensional scrolling at a width equivalent to 320 CSS px, except for content that genuinely requires a two-dimensional layout for meaning or use.

A common test is 400% zoom from a 1280 CSS-pixel-wide starting viewport, but the criterion is about the equivalent width, not one magic browser setup.

For horizontal writing, horizontal scrolling of ordinary prose or controls is usually a warning sign. Tables, maps, diagrams and similar two-dimensional content can be exceptions.

## Flexible geometry

Text containers should normally grow.

Use `min-height` instead of fixed height when text can wrap or enlarge.

Do not assume a `px` breakpoint is automatically inaccessible or a `rem` breakpoint automatically accessible. Choose units that fit the project and verify behavior under actual text enlargement and reflow.

A responsive switch should happen when the content needs it.

## Viewport zoom

Do not cap user zoom in the viewport meta configuration.

Interfaces should survive the user's browser and OS enlargement tools rather than protecting a composition by preventing magnification.
