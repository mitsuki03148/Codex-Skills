# Screen readers

Hidden supporting text, live regions, alternative text, SVG, media and multilingual announcements.

## Visually hidden supporting content

Use a proven visually-hidden utility when information should remain available to assistive technology.

```css
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0 0 0 0);
  clip-path: inset(50%);
  white-space: nowrap;
  border: 0;
}
```

Prefer the project's existing utility such as Tailwind `sr-only`.

Do not use `display: none` or `visibility: hidden` when the content is intended to remain exposed to accessibility APIs.

Visually hidden text is not a licence to duplicate everything sighted users see. Add only context the visual presentation conveys but the accessible representation otherwise loses.

## Announcing dynamic changes

Use the least intrusive mechanism that keeps the user oriented.

1. **Focus already moves to the new content** — often no live announcement is needed.
2. **Information belongs to one control** — associate it with that control where appropriate.
3. **Routine untied update** — use a polite status mechanism.
4. **Urgent untied error** — use alert behavior sparingly.

A stable live region that exists before its text changes is often more reliable for repeated polite messages than repeatedly mounting a new filled region.

Do not make all state changes assertive. Interrupting the user's current speech output has a real attention cost.

Test critical announcements in the browser / screen-reader combinations the project supports; live-region behavior has implementation differences.

## Loading states

When a region is updating, `aria-busy` can describe that state where appropriate.

Announce progress only when the user needs the update to understand what is happening. Do not create a stream of low-value "loading / still loading / almost done" announcements.

When results arrive, announce the information the user would otherwise miss, such as a changed result count, rather than narrating the visual animation.

## aria-hidden

`aria-hidden="true"` removes a subtree from the accessibility tree.

Use it for decorative or intentionally duplicated visual content.

Never put it on or above focusable or uniquely informative content.

Pseudo-elements are not accessibility-tree content by themselves; do not add ARIA for CSS decoration that has no DOM node.

## Alternative text by purpose

For `<img>`:

| Purpose | Alternative |
| --- | --- |
| Decorative or redundant | `alt=""` |
| Informative | Describe the information the image contributes |
| Functional image that supplies the control's name | Describe the action or destination |
| Image of essential text | Provide the equivalent text, preferably as real text |
| Complex chart / diagram | Concise alternative plus the equivalent data or explanation needed for the task |

Do not duplicate a button's accessible name in a nested image if the button already has its own visible or programmatic label.

Describe meaning, not every visible pixel.

## SVG

Decorative inline SVG inside an already-named control can use `aria-hidden="true"`.

A meaningful standalone SVG can expose an image role and accessible name when that is the most appropriate representation.

Prefer the project's established SVG pattern and verify the computed accessibility tree rather than adding redundant `role`, `title` and `aria-label` layers all at once.

Legacy `focusable="false"` may still appear for older browser support; do not add it mechanically when the project's browser matrix no longer needs it.

## Language and pronunciation

Screen readers need correct language metadata as much as visual typography does.

Set the document language and mark meaningful language changes when pronunciation should switch.

For mixed EN / Traditional Chinese / Japanese content:

- do not force English pronunciation onto Chinese or Japanese labels;
- keep hidden supporting text localized with the control it describes;
- keep identifiers, product names and code tokens in the language / pronunciation treatment the product intends.

Ruby and other visual language aids belong to typography, but verify the accessible reading remains understandable and is not redundantly announced in a confusing way.

## Captions, audio alternatives and media controls

Provide the alternatives required by the media type and project conformance target.

Prerecorded synchronized video commonly requires captions under WCAG. Audio-only and video-only content have their own media-alternative requirements.

Do not collapse every media requirement into "always add a transcript"; inspect what the content contains and which criterion applies.

Autoplay and continuing motion are handled with the timing / motion requirements in [motion-and-zoom.md](motion-and-zoom.md).
