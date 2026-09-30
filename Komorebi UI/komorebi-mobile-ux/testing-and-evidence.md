# Testing and evidence

Primary research syntheses for this skill:

- `10_Admin_Documents/Search Results/Mobile_iPad_Attention_Thumb_Finger_Flow_UX_Research_20260929`
  - Google Drive File ID: `1tmsnIoqTo5pfbxLc6-16YfnCA21P1zWJlO6Ab-Ku4EI`
- `10_Admin_Documents/Search Results/Mobile_UI_Interaction_Timing_Button_Response_and_Transient_UI_Research_20260929`
  - Google Drive File ID: `13K7_GWpEeQcDIIvm0pWVNMlMy_2kp-gd1CgAf6xAHsI`

The research source distinguishes peer-reviewed HCI / ergonomics, current platform guidance and practitioner observation. Preserve those evidence boundaries when extending this skill.

This skill is intentionally cautious about what can be claimed from source code or screenshots.

## Evidence tiers

### Source-derived

You can inspect:

- control position;
- hit-region declarations;
- gesture handlers;
- responsive layout;
- fixed / sticky placement;
- ordering and state changes.

Source does **not** prove physical comfort.

### Render-derived

A browser or simulator can verify:

- actual geometry;
- occlusion risk on screen;
- scrolling behavior;
- keyboard overlap;
- orientation variants;
- placement changes across breakpoints.

A simulator still does not reproduce the weight and grip of a physical device.

### Embodied / real-device

Strongest evidence for:

- regrip;
- thumb stretch;
- wrist posture;
- hand switching;
- subjective comfort;
- fatigue;
- accidental activation during repeated use.

## Timing evidence tiers

Timing claims need their own evidence surface.

### Source-derived

You can inspect:

- transition / animation durations;
- gesture recognizers and timeout APIs;
- loading / working / success state wiring;
- debounce / duplicate-submit guards;
- transient-UI timeout values;
- whether the next action is programmatically disabled.

Source does not prove when pixels actually update or whether the delay feels connected to the user's touch.

### Runtime-measured

Instrument or observe:

- `T0` — input / touch;
- `T1` — first visual / tactile acknowledgement;
- `T2` — accepted / working state;
- `T3` — result;
- `T4` — next action available.

Useful differences:

- `T1 − T0` — acknowledgement latency;
- `T3 − T0` — completion latency;
- `T4 − T3` — choreography / blocking cost after completion.

Do not claim perceived quality from code constants alone.

### Human-observed

Watch for:

- repeated taps after uncertainty;
- verbal “did it work?”;
- re-aiming or pressing harder;
- giving up / navigating away;
- failing to reach a transient action before it disappears;
- frustration on the 50th repetition;
- slower readers or motor users being forced to race the UI.

When important, test accessibility timeout behavior and Reduce Motion as actual modes rather than inferring them from declarations.

## Practical phone matrix

Use only the rows relevant to the product:

- right one-hand;
- left one-hand;
- cradle;
- two-thumb;
- seated / standing;
- walking or commuting when the real use case includes it.

## Practical iPad matrix

- portrait two-hand held;
- landscape two-hand held;
- one-hand support + finger;
- lap;
- desk + pointer / keyboard;
- Pencil when supported.

## Regrip log

Watch rather than only ask “was it easy?”

Record:

- phone sliding in palm;
- thumb stretch;
- second hand entering;
- finger substitution;
- wrist rotation;
- device tilt;
- repeated repositioning.

One regrip can be normal. Repeated regrip on the primary loop is a stronger signal.

## Quick attention tests

### First-glance test

Show the screen briefly and ask what was noticed first.

### Action-expectation test

Ask where the person would tap next before telling them.

### Structure test

Ask:

- What screen is this?
- What is the main thing here?
- What can you do next?

If the action is noticed but physically awkward, the problem is primarily motor.
If it is easy to reach but not noticed, the problem is primarily attention/hierarchy.
If neither works, inspect the structure before polishing the control.

## Repetition test

For a repetitive product, do not stop at the first successful tap.

Repeat the core loop enough times to expose:

- cumulative travel;
- repeated wrist posture;
- grip changes;
- fatigue;
- mis-taps;
- reorientation cost.

The exact repetition count depends on the product; “50th use” is a design reminder, not a compliance threshold.

## Source quality boundaries

The research basis combines:

- current Apple / Android / WCAG platform guidance;
- peer-reviewed HCI and ergonomics studies;
- practitioner field observation for grip diversity.

Do not flatten them into one authority level.

In particular:

- practitioner grip percentages are useful field evidence, not universal population constants;
- older small-device target studies are historical evidence, not modern platform specifications;
- conflicting attention studies are evidence against a single universal scan path;
- platform target sizes belong to `komorebi-accessibility` when judging conformance/usability thresholds.
