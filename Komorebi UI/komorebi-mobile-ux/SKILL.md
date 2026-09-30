---
name: komorebi-mobile-ux
description: "Adds embodied mobile and tablet UX: visual attention, thumb and finger reach, grip, occlusion, interaction timing, transient UI, repeated motor cost, and iPad holding/input modes."
---

# Mobile embodied UX

A touch interface is not only a picture on a screen. Someone is holding the device, looking, deciding, moving a finger, changing grip and returning to the task.

This skill owns that **attention-to-action path across space and time**.

Its spatial model is:

**SEE → UNDERSTAND → REACH → ACT → RECOVER**

Its temporal model is:

**NOTICE → DECIDE → TOUCH → FEEDBACK → WORK → RESULT → NEXT**

A control can be visually obvious but physically expensive. It can be easy to reach but hard to notice. It can acknowledge instantly yet make the user wait on decorative motion, or complete quickly while giving no sign that the tap registered. Good mobile UX keeps both paths coherent.

This skill is a companion to the Komorebi UI skill set, not a replacement for its owners:

- visual hierarchy, reading order and spatial composition → `komorebi-layout`;
- target-size conformance, motor accessibility and alternatives → `komorebi-accessibility`;
- press-state styling, gesture presentation, motion and surface polish → `komorebi-ui`;
- wording and control labels → `komorebi-writing`;
- cross-domain synthesis and verdict → `komorebi-interface`;
- stress harnesses → `break`.

Do not turn the research into a universal thumb-zone diagram or a universal timing table. Reachability and timing bands are evidence, not placement or duration truth.

## 1. Start with the human/device configuration

Before judging placement, name the configuration that matters:

- phone or tablet;
- portrait or landscape;
- left hand, right hand, cradle or two-handed use;
- device supported in the hand, lap or desk;
- touch, pointer, hardware keyboard or Pencil;
- one-off action or the 50th repetition.

If the configuration is unknown, keep the ergonomics judgement conditional instead of pretending one grip represents everyone.

For iPad especially, ask **how the device is being supported** before asking where the thumb zone is.

## 2. Keep the attention map and motor map separate

Do not assume the place that attracts the eye is the place the hand can comfortably reach.

Ask two independent questions:

1. **Attention:** Does the user notice and understand the next meaningful thing?
2. **Motor:** Can the hand reach and operate it with reasonable effort in the relevant posture?

Only then ask whether those paths converge naturally.

Mobile attention research does not support one universal scan pattern. Top-leading bias, lower-screen attention and semantic expectation all appear in different studies and tasks. Treat them as observations to test, not layout laws.

See [attention-and-action-flow.md](attention-and-action-flow.md).

## 3. There is no universal thumb-safe zone

Thumb reach varies with:

- hand size;
- device size;
- grip;
- handedness;
- finger support behind the device;
- movement direction.

Distance alone is not enough. A target equally far away in two directions can carry different biomechanical cost.

Do not review a phone only with the designer's preferred hand. At minimum, check both left- and right-handed one-hand use where one-handed operation is part of the product.

See [phone-reach-and-grip.md](phone-reach-and-grip.md).

## 4. Optimize the path, not the isolated target

A target can be fine by itself while the flow is tiring.

Trace the actual sequence:

- where the eyes orient;
- where the decision is made;
- where the next control sits;
- how far the hand travels;
- whether the grip changes;
- where the eyes must return afterward.

Look for **motor ping-pong**: repeated top ↔ bottom travel, far-corner ↔ opposite-edge travel, or repeated regrip between steps.

A common reading flow can legitimately be:

**orient high → process through the middle → act lower**

but that is a useful pattern, not a law. Maps, cameras, games, drawing tools and dense workspaces can need different geometry.

## 5. Regrip is a signal

Watch for:

- phone sliding in the palm;
- thumb stretching to its limit;
- wrist rotation;
- device tilt;
- second hand entering;
- switching from thumb to index finger;
- repeated hand repositioning.

One regrip is not automatically bad. A repeated regrip for a high-frequency primary action is stronger evidence of motor friction.

Do not diagnose from reach alone. **Reachability ≠ comfort ≠ accuracy ≠ speed.** Name which dimension is actually failing.

## 6. Frequency changes the placement cost

High-frequency actions deserve the cheapest repeat path:

- next / continue;
- repeat / play-pause;
- mark done;
- like / save;
- logging and training controls;
- game actions;
- repeated data entry.

For these, prefer:

- stable placement;
- short travel;
- low regrip cost;
- sufficiently large hit regions;
- immediate feedback.

Rare or destructive actions do not automatically belong in the easiest reach region. A little deliberate motor friction can protect against accidental activation when the product still keeps the action discoverable.

## 7. Phone: lower reach is useful, not sovereign

Current platform guidance and thumb-reach research support treating the middle/lower phone region as a useful place for repeated primary actions.

But do not move everything down.

Top/leading regions can remain good for:

- orientation;
- titles and context;
- status;
- low-frequency or secondary navigation.

The lower region often suits:

- repeated primary actions;
- persistent top-level navigation;
- next / continue;
- common toggles.

Far corners deserve caution for repeated one-handed actions, especially on tall phones, but familiar platform placement and task meaning can outweigh pure reach.

## 8. iPad is not a large phone

Large tablets change the motor map.

In two-hand held mode:

- each thumb naturally owns a side-edge region;
- repeated reaches toward the center can increase thumb extension and wrist load;
- the physical center can be a high-cost motor zone even when it is visually central.

In other modes the map changes again:

- **one-hand support + other-hand input:** index finger has wider access;
- **lap:** grip constraints reduce;
- **desk + pointer/keyboard:** touch reach matters less and density can increase;
- **Pencil:** precision and occlusion patterns change.

Design iPad ergonomics by **holding/input mode**, not screen width alone.

See [ipad-holding-and-input.md](ipad-holding-and-input.md).

## 9. Account for finger occlusion

Touch is not a perfect point. The finger can hide the target or the result of the action.

Be especially careful with:

- sliders;
- scrubbing;
- drag handles;
- maps;
- drawing surfaces;
- tiny adjacent controls;
- controls placed directly under the finger during repeated scrolling.

Possible responses include larger hit regions, more spacing, offset feedback, magnification, contextual controls or moving the result away from the finger.

Do not invent a custom gesture when a familiar platform gesture already solves the task.

## 10. Preserve hand continuity through a flow

When a flow begins in an easy one-handed region, avoid sending the next routine step to a far corner without a reason.

When the user is already acting on an object, consider bringing the next action closer to that object rather than forcing travel to global chrome.

The goal is not minimum movement at every step. It is a path that feels predictable and physically coherent.

## 11. The 50th repetition matters

A reach that feels acceptable once can become the defining friction of a repetitive product.

For learning, music practice, games, reading, coaching/logging and data entry, inspect cumulative cost:

- repeated thumb travel;
- repeated wrist posture;
- grip shifts;
- mis-taps;
- fatigue;
- reorientation after each action.

This extends `komorebi-layout` and `komorebi-ui`'s existing principle that the fiftieth use matters, without taking over their visual rules.

## 12. Timing is part of the embodied path

A tap has two different clocks:

1. **Acknowledgement** — when the interface makes it clear the input was received.
2. **Completion** — when the requested work actually finishes.

Do not wait for final completion before acknowledging the action. Prompt local feedback preserves cause and effect even when network or processing work takes longer.

Look for timing friction:

- silence after touch that causes repeat taps;
- inconsistent feedback latency / jitter;
- loading UI that flashes so briefly it creates instability;
- animation that blocks the next action after the system is already ready;
- a tapped control disappearing and another action moving underneath the finger;
- transient UI disappearing before the user can read, decide, reach and act;
- hidden gesture timing invented instead of using platform recognition;
- high-frequency controls carrying ceremonial motion on every repetition.

Classic response-time bands and study-specific latency thresholds are useful evidence, not universal product constants. Do not turn `100ms`, `300ms`, `1s`, `5s` or `10s` into magic numbers without the owning platform / accessibility context.

For transient UI, think in human time:

**READ + DECIDE + REACH + ACT**

Short redundant status can disappear automatically. A snackbar or banner containing an action needs enough time — or persistence / recoverability — for the user who actually has to use it. Important information should not exist only in a fleeting surface.

Prefer platform recognizers for long press / double tap and platform accessibility timeout mechanisms where available. Do not hide a required primary action behind long press.

See [interaction-timing-and-transient-ui.md](interaction-timing-and-transient-ui.md).

## 13. Test with real postures and real timing

Static screenshots cannot verify ergonomics.

Where the experience matters, test the relevant configurations with the real device or a realistic hardware setup.

Useful quick checks:

- **First glance:** what did you notice first?
- **Action expectation:** where would you tap next?
- **One-hand pass:** can the flow finish without a grip change?
- **Left/right pass:** does either hand become materially worse?
- **50th repetition:** does the routine stay comfortable?
- **Occlusion pass:** does the finger hide what needs to be seen?
- **iPad posture pass:** does the result change when held, on lap, or on desk?
- **Tap acknowledgement pass:** does the first feedback arrive before uncertainty causes a second tap?
- **Working-state pass:** does a noticeable wait stay local, legible and spatially stable?
- **Next-action pass:** can the user continue as soon as the system is ready, or does motion block them?
- **Transient-action pass:** can the user read, decide, reach and act before temporary UI disappears?

See [testing-and-evidence.md](testing-and-evidence.md).

## Cross-skill routing

Use this skill together with the suite rather than duplicating their rules.

| Question | Owner |
| --- | --- |
| Is the action visually where the user expects it? | `komorebi-layout` + this skill |
| Is the target large enough under WCAG/platform guidance? | `komorebi-accessibility` |
| Does pressing/dragging feel and look right? | `komorebi-ui` |
| Does touch acknowledge promptly while completion / waiting stays understandable? | this skill + `komorebi-ui` |
| Does timed / transient UI satisfy accessibility requirements? | `komorebi-accessibility` |
| Is the label clear? | `komorebi-writing` |
| Is the finger path physically cheap and coherent? | this skill |
| Can transient UI be read, reached and acted on fairly? | this skill |
| Does the whole experience still make sense? | `komorebi-interface` |
| Does it survive hostile mobile/tablet scenarios? | `break` |

## Before you finish

| Mistake | Better question |
| --- | --- |
| “Put every primary action in the thumb zone” | Which grip, hand, device and task frequency? |
| “Bottom is always best” | Where do attention and motor paths meet for this task? |
| “Center is easiest” | On phone, tablet, held how, using which finger? |
| “Reachable means good” | Is it comfortable, accurate, fast and repeatable? |
| “One regrip means failure” | Is the regrip repeated or costly for the task? |
| “iPad is the phone layout scaled up” | Which support/input mode is active? |
| “Bright and large means noticed” | Does placement and expectation support attention? |
| “44pt means the artwork must be 44pt” | Is the hit region large while the visual can stay quiet? |
| “Destructive actions should be easiest to reach” | Would a little deliberate friction reduce accidental activation? |
| “The screenshot proves ergonomics” | Which real posture or interaction was actually tested? |
| “All taps must finish in 100ms” | How fast is acknowledgement, and how long does completion actually take? |
| “Spinner after exactly 300ms” | Does heavier loading UI avoid flashing while still explaining a real wait? |
| “Toast for five seconds” | Does this content need read, decide, reach and act time — and is it recoverable? |
| “Long press = 350ms” | Can the platform recognizer own the gesture timing? |
| “Animation is only 300ms” | Does it block the next action or become costly on the 50th repetition? |

## Reporting

**Severity.** `HIGH` blocks or repeatedly degrades a core task, makes an important touch action effectively unreachable in a supported configuration, creates serious accidental-activation / duplicate-execution risk, or makes consequential timed UI unfairly unusable. `MEDIUM` adds repeated regrip, excessive travel, occlusion, hand asymmetry, reorientation cost, uncertain tap acknowledgement, timing jitter or repeated waiting friction to a meaningful flow. `LOW` is isolated ergonomic / timing polish.

When `komorebi-interface` orchestrates the review, its shared severity and verdict replace this standalone scale.

**Verification.** Distinguish source inspection, runtime timing and embodied verification. Source can show placement, gesture wiring, timers and state transitions; it cannot prove comfort or perceived responsiveness. Runtime instrumentation can measure touch-to-feedback / result / next-action timing; a simulator can show geometry but not muscle effort or grip. Real-device/posture testing is the strongest evidence for ergonomics. Mark untested hand/posture or timing assumptions `Not verified`.

**Format.** One row per root cause:

| Severity | Configuration | Location | Observed path | Change | Why |
| --- | --- | --- | --- | --- | --- |

`Configuration` names the relevant posture, e.g. `Phone · right one-hand`, `Phone · left one-hand`, `iPad · two-hand held landscape`, `iPad · desk + pointer`.

With nothing actionable, state **“No actionable mobile embodied-UX findings in the checked configurations.”**
