# Interaction timing and transient UI

Interaction timing is part of embodied UX because a user does not only move through space. They also wait, re-aim, repeat taps, read transient feedback and decide whether the system heard them.

Primary research synthesis for this reference:

- `10_Admin_Documents/Search Results/Mobile_UI_Interaction_Timing_Button_Response_and_Transient_UI_Research_20260929`
- Google Drive File ID: `13K7_GWpEeQcDIIvm0pWVNMlMy_2kp-gd1CgAf6xAHsI`

The source separates current platform guidance, peer-reviewed / academic latency evidence, WCAG requirements and classic UX heuristics. Preserve those evidence boundaries.

## Two clocks: human input and system completion

A tap has at least two meaningful times:

1. **Acknowledgement** — when the interface makes it clear the input was received.
2. **Completion** — when the requested work actually finishes.

These should not be confused.

A network action may take seconds while still feeling responsive if acknowledgement is prompt and the working state is clear. A fast backend can still feel broken if the first visible response arrives late or inconsistently.

Useful sequence:

**TOUCH → FEEDBACK → ACCEPTED / WORKING → RESULT → NEXT ACTION**

The first feedback should preserve cause and effect. The final result can arrive later.

## Immediate feedback is a perceptual target, not a magic constant

Touch-latency research in the source reports perceptual quality dropping as feedback delay grows, with visual button feedback becoming noticeably worse around the low hundreds of milliseconds and several hundred milliseconds of silence feeling poor.

Use this as evidence that first feedback should be prompt. Do not promote one study's millisecond values into a universal platform requirement.

Good first feedback can be:

- pressed / highlighted state;
- ripple or local value change;
- haptic confirmation where appropriate;
- immediate selected state;
- a local working state.

Do not wait for a network round trip before acknowledging a tap.

## Consistency matters as well as average speed

Variable latency can feel less trustworthy than a modest but stable response.

Watch for:

- one tap responding instantly and the next appearing dead;
- haptics arriving noticeably after the visual state;
- repeated taps caused by uncertainty;
- state changes that sometimes queue behind animation.

Jitter is an interaction-quality signal even when average timing looks acceptable.

## Response-time bands are heuristics, not laws

The classic `~0.1 / 1 / 10 second` bands and progress-indicator guidance are useful orientation, not physiological or platform requirements.

A practical interpretation:

- **Very fast:** acknowledge locally; do not flash a heavy loader just because loading UI exists.
- **Noticeable wait:** keep the local action in an accepted / working state.
- **Longer wait:** explain progress or system status in context.
- **Long wait:** where feasible, allow cancel, leave, background work or later notification.

Do not hardcode a spinner delay or progress threshold merely because an industry article used one number. Test the actual task and preserve project conventions.

## Loading UI should not make a fast operation feel slower

A loader that appears for a fraction of a second can create visual instability and make a quick operation feel heavier than it is.

Prefer:

- immediate local press feedback;
- a working state only when the wait becomes perceptible;
- stable layout when loading starts and finishes;
- local progress for local work instead of freezing the entire screen.

The exact loader-onset delay is a product decision. The source explicitly treats common `200–400ms` delayed-spinner values as practitioner patterns, not universal research laws.

## Keep the next action available when it is genuinely ready

Animation should explain a state change, not become a toll gate.

A control that is visually present but ignores input until a decorative transition ends creates false availability.

If the system is not ready:

- show a real disabled / working state;
- preserve the reason or progress;
- do not let the interface pretend the action is available.

If the system is ready, do not make the user wait for choreography.

High-frequency actions deserve especially lightweight timing. A 300ms flourish repeated fifty times is cumulative interaction cost.

## Preserve spatial ownership after touch

Timing and geometry interact.

After a tap, avoid:

- removing the tapped control and sliding a dangerous action under the same finger;
- inserting a banner that shifts the target the user was about to press;
- moving the accepted / working state to a distant part of the screen;
- making the user search for whether the action registered.

Stable ownership often means the same region evolves:

`Save → Saving… → Saved`

rather than disappearing and reappearing elsewhere.

## Prevent duplicate actions without making the surface feel dead

For submissions or network actions:

- acknowledge immediately;
- prevent duplicate execution when duplicates are harmful;
- keep the specific control's working state visible;
- leave unrelated UI usable where safe;
- do not silently ignore repeated taps while leaving the control looking active.

Repeated taps after uncertainty are evidence that acknowledgement or state communication may be weak.

## Long press and double tap use platform recognition

Do not invent custom timing thresholds for familiar gestures without a strong product reason.

Use platform recognizers / configuration for:

- long press;
- double tap;
- touch slop;
- ambiguous gesture handling.

These gestures compete with scrolling and other recognizers. Overloading one surface with tap + double tap + long press + drag + swipe increases timing ambiguity.

Long press is hidden interaction. Keep required primary actions visibly available elsewhere unless the platform convention and task genuinely support hidden contextual access.

## Transient UI needs read + decide + reach + act time

A snackbar, banner, toast or contextual control does not need one universal duration.

Its fair lifetime depends on:

**READ TIME + DECISION TIME + MOTOR TIME**

A short redundant success message can disappear automatically. A transient surface with text plus an action needs more time and, where the platform supports it, should use accessibility-aware timeout mechanisms.

Important or consequential information should not exist only in a fleeting surface.

If missing the transient control causes meaningful loss, prefer one or more of:

- persistent presentation;
- accessibility-adjusted timeout;
- pause / extension;
- a durable recovery path such as history, trash or restore.

Do not misread WCAG's five-second moving-content rule as a recommended toast duration.

## Reversible actions and destructive actions have different timing needs

For low-risk reversible actions, immediate result + undo can preserve flow.

For high-consequence or irreversible actions, deliberate confirmation can be appropriate.

Do not confirm every harmless action. Confirmation itself adds time and can train users to dismiss warnings automatically.

A transient Undo control is only fair when the user has enough time to perceive, reach and activate it, and when the consequence is recoverable elsewhere if stakes are high.

## Learning interfaces should respond fast without rushing learning

For teaching / practice flows:

**SELECT → COMMIT → IMMEDIATE STATE → EXPLANATION → NEXT**

Fast input acknowledgement is good. Automatically removing the explanation or jumping to the next item before the learner can inspect feedback is not.

Do not accidentally test reaction speed unless reaction speed is the lesson.

## Timing evidence

Useful runtime timestamps:

- `T0` — input begins / touch lands;
- `T1` — visible / tactile acknowledgement;
- `T2` — accepted / working state;
- `T3` — result appears;
- `T4` — next action is available.

Derived measures:

- `T1 − T0` — input-feedback latency;
- `T3 − T0` — completion latency;
- `T4 − T3` — post-result blocking / choreography cost.

A screen can complete quickly and still feel slow if acknowledgement is delayed or if motion blocks the next action.

## Owner boundaries

| Question | Owner |
| --- | --- |
| Does touch acknowledge quickly enough to preserve cause and effect? | `komorebi-mobile-ux` + `komorebi-ui` |
| What press / motion treatment should express that acknowledgement? | `komorebi-ui` |
| Does timed UI satisfy accessibility requirements / preferences? | `komorebi-accessibility` |
| Does transient UI give enough read / decide / reach / act time? | `komorebi-mobile-ux` |
| Should the action be visually available yet? | `komorebi-layout` + `komorebi-mobile-ux` |
| Does async state copy explain what is happening? | `komorebi-writing` |
| Does the full flow remain coherent? | `komorebi-interface` |

## What not to overgeneralise

Do not turn these into laws:

- “all buttons must respond in exactly 100ms”;
- “all spinners wait exactly 300ms before appearing”;
- “all animations are 200ms / 300ms”;
- “all toasts last five seconds”;
- “all destructive actions need confirmation”;
- “all reversible actions should use transient Undo”;
- “long press means 350ms”.

The transferable principle is simpler:

**Respond quickly. Explain waiting. Preserve causality. Let the human finish reading and acting. Do not make animation or timers race the user.**
