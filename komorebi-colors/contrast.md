# Contrast

Contrast is measured between a foreground and the background it actually renders against.

Identify the real rendered pair first. A text token checked against the page background tells you nothing if the text actually sits on a tinted card, translucent overlay, image or gradient.

**Report, don't repaint.** When a required pair fails, report the pair, the measured value and the threshold it misses. Change the colors only when the task includes implementation or the user asks for a fix.

`better-accessibility` decides which content is required to meet which accessibility criterion. This file covers color measurement and color-side repair.

## WCAG 2.2 is the conformance gate

When WCAG 2.x conformance applies, use the WCAG 2.2 contrast-ratio requirements:

| Content | WCAG 2.2 AA |
| --- | --- |
| Normal text | `4.5:1` |
| Large text | `3:1` |
| Required visual information for UI components / states | `3:1` against adjacent colors |
| Required graphical objects | `3:1` against adjacent colors |

WCAG 2.2 defines large text using its font-size / bold thresholds. Follow `better-accessibility` for classification.

Do not round a failing value up to the threshold.

## APCA is supplemental, not conformance

APCA can be useful as a perceptual design metric when a project explicitly adopts it.

Do not present APCA as the current W3C conformance algorithm. As of the September 2026 WCAG 3 Working Draft, the contrast algorithm is still to be determined.

If a project asks for APCA:

- report it separately from WCAG 2.2;
- name the implementation / version used;
- do not use it to waive a WCAG 2.2 failure when WCAG 2.2 conformance is required.

## Fixing a failing pair

When asked to fix a failing pair, usually change perceived lightness before changing hue identity.

A practical order:

1. confirm the actual rendered background;
2. adjust foreground or background lightness enough to pass;
3. preserve semantic hue where possible;
4. reduce chroma only when needed for gamut or visual balance;
5. remeasure the rendered pair.

A contrast repair should not silently become a palette redesign.

## Soft palettes still need a hard floor

Muted, low-chroma palettes can stay gentle while maintaining contrast.

Useful strategies include:

- darker ink rather than more saturated ink on light paper;
- lighter text rather than neon text on dark surfaces;
- stronger local surface separation instead of outlining every object;
- keeping decorative low-contrast detail separate from essential information.

Do not make body text faint merely to preserve a pastel mood.

## Mid-tone surfaces are expensive

When both foreground and background sit near the middle of the lightness range, neither dark nor light text may produce a comfortable reading result without changing the surface itself.

If text needs strong contrast, move one side of the pair toward an extreme rather than forcing chroma or hue to do a lightness job.

## What to check

- **Every appearance.** A pair that passes in light mode can fail in dark mode.
- **Every meaningful state.** Default, hover, active, selected, disabled where required, error and focus can all change the pair.
- **Translucent surfaces.** Test the lightest and darkest content that can appear behind them, or make the surface stable enough that the pair cannot fail.
- **Computed colors.** `color-mix()`, relative colors and alpha resolve at render time; measure the resolved result.
- **Text over images.** Measure worst-case regions or guarantee a stable text field with composition, scrim or surface treatment.
- **Gradients.** One average sample is meaningless; inspect the darkest / lightest relevant region behind the foreground.
- **Thin strokes.** A mathematically passing color can still render weakly when a line or glyph stroke is extremely thin. Inspect the real output.

## Contrast and non-semantic artwork

Decorative artwork can contain subtle low-contrast color relationships.

Do not force every illustration edge to meet UI-component contrast. The requirement applies when that visual information is necessary to understand content or operate the interface.

Separate “beautifully subtle” from “required to perceive”.
