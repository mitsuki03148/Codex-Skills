---
name: break
description: Renders one real component across plausible worst-case states, locales, containers and high-risk combinations on a temporary page, then reports only what visibly breaks.
disable-model-invocation: true
---

# Break

This skill takes one real component and gives it bad weather.

It renders the component on a temporary page across the states and scenarios that can actually reach it, then marks only what visibly breaks. The page is the primary artifact: a scrollable visual report with the normal case, stress cases and observed failures side by side.

A component built against one happy path can look finished until real content, localization, constrained space, media, state changes, accessibility settings, real touch posture or async / transient timing arrive.

This skill observes rather than judges. A finding is a visible or interactively reproducible break, named in the vocabulary of the domain skill that owns the fix. Reviewing code against a standard belongs to `interface-review` / `komorebi-interface`; embodied phone / tablet comfort belongs to `komorebi-mobile-ux`; exploring alternative designs belongs to `variant`.

Isolation is intentional, but isolation must not erase the environment the component genuinely depends on.

## Principles

### Stress reality, not imagination

A scenario earns a slot only when production can plausibly create it or the component contract explicitly allows it.

Do not invent absurd hostile input merely because it can make CSS fail. Use realistic extremes, real locale strings, actual data shapes and supported states first.

If a pathological value is still valid input — for example an unbreakable user-supplied URL — it is fair game.

### Keep one normal case visible

Every harness starts with one representative normal case. It gives the eye a baseline and makes stress-induced changes obvious.

Do not judge the stress cases against an imaginary ideal; compare them with the real component behaving normally in the same environment.

### Isolate the component, not its dependencies

Import the real production component.

Keep the smallest real shell it needs:

- the app's global styles and fonts;
- its real theme / token providers;
- required context providers;
- safe-area or platform wrapper where the component genuinely depends on one;
- the real parent sizing behavior when that behavior is part of the contract.

Do not rebuild a lookalike, re-theme it, copy styles into the harness or replace real tokens with test colors.

A harness that removes a required owner context is testing a different component.

## 1. Scope one component

One component per run.

"The settings page" is not one component. A reusable profile text field, result card, practice tile or message row is.

When several candidates are present, choose the one the request clearly centers on. If no candidate is clearly primary, list the candidates rather than pretending a page is one component.

Restate the component in one sentence: what it accepts, what it renders and the environment it belongs to.

## 2. Infer scenario axes from the contract

Read the component before generating fixtures:

- props;
- slots;
- supported states;
- data shape;
- media inputs;
- localization surface;
- parent sizing assumptions;
- interaction / lifecycle states that can be entered without rewriting the component;
- async / timer / transient behavior the real component owns;
- supported phone / tablet posture or input assumptions when the component is touch-first and repeated reach matters.

[scenarios.md](scenarios.md) contains the scenario axes and the cue for each one.

Keep only axes whose cue matches. Record the kept axes and the dropped axes with one short reason each.

Do not run every axis against every component.

## 3. Add a few seam scenarios

Single-axis cases catch many failures. Some important failures only appear when two reasonable conditions meet.

After selecting the axes, add a small number of **high-risk seam scenarios** where the component contract makes the combination plausible, for example:

- narrow container × Japanese long label;
- error state × long localized message;
- large text × two peer actions;
- image crop × wide English overlay;
- many tags × narrow width;
- dark appearance × translucent surface over media.

Do not build the Cartesian product. Two to four seams is usually enough.

A seam exists to test a suspected interaction between axes, not to inflate coverage.

## 4. Build the harness page

Create one throwaway route inside the app and render the real component once per scenario in a single readable column or simple grid.

Each case gets:

- a short scenario label;
- the real component;
- only the minimum fixture / container wrapper needed to create that scenario;
- a one-line observed note only when something breaks.

The harness adds no visual design of its own beyond labels, spacing between cases and scenario containers.

### Widths

Width cases are fixed containers on the page, not repeated viewport resizing. One load should show the width variants together.

### Themes and environment

Use the product's real theme mechanism when it can be activated without redefining tokens.

Do not simulate dark mode by creating a fake `.dark` token set in the harness.

Environment settings such as reduced motion, contrast preference, browser zoom or an OS theme may remain user-toggled when the production environment owns them.

### Data

Use fixture props. Never wire the harness to live production state.

Production must never import from the harness.

## 5. Include EN / Traditional Chinese / Japanese when language can vary

When the component renders localized, API, CMS or user-authored text, include representative EN / zh-Hant / ja fixtures.

Do not translate one English string mechanically just to make three rows. Use realistic shapes for each language:

- English can become horizontally long;
- Traditional Chinese can be compact in character count but dense and punctuation-sensitive;
- Japanese can mix kanji / kana, and long katakana names can become unexpectedly wide;
- mixed Latin + CJK strings can expose line-height, spacing and truncation seams.

The owner skills decide whether the behavior is correct. `break` only exposes what happened.

## 6. Observe the rendered result

Actually render before reporting a visible failure.

A predicted break is not a finding.

Prefer one calm pass over the full harness rather than screenshotting or debugging every case independently. The point is that the page itself makes comparison cheap.

If the harness itself is broken — missing fixture data, missing provider, wrong client/server boundary — fix the harness and reload. A harness repair does not count as a second design review.

If runtime inspection is unavailable, provide the harness route and scenario list and mark visual observation `Not verified`. Do not convert a source-code prediction into an observed finding.

## 7. Observe transitions only when the component owns them

Side-by-side states do not prove transitions.

If the component contract itself contains a meaningful transition that can break — loading → content, collapsed → expanded, validation → error, image placeholder → image, tap → working → result, or transient feedback → dismissal — add one small sequence case or an interaction note.

Do not invent instrumentation or a state machine the component does not own.

A layout shift observed only during transition should not be claimed from two static snapshots.

## 8. Mark breaks on the page

The page is half the report.

For each observed break, place one concise note below the affected scenario. Example:

`Break — Japanese label clips before the trailing icon.`

Do not decorate the report with severity colors, redesign suggestions or screenshots unless the task asks for them.

## 9. Report what broke and stop

Report broken scenarios first:

| Scenario | Observed | Owner |
| --- | --- | --- |
| Narrow container × long Japanese label | Label clips before the trailing icon | `komorebi-layout` / `komorebi-typography` |
| Error state × long zh-Hant copy | Action row is pushed outside the card | `komorebi-layout` |

Assign one primary owner. Add a secondary owner only when the break genuinely crosses a seam.

This skill owns no domain rules and issues no verdict.

"Everything survived" is a complete report. State the scenarios rendered and the route where the page remains available.

Do not pad a clean run with preferences.

## 10. Fix only when asked

A normal `break` run is observational.

If the user asks to fix a break, follow the owning skill's rules, then re-render only the failing scenario plus the normal baseline and any seam that depends on it.

Do not rerun the whole matrix unless the fix changed a shared primitive that could affect everything.

## 11. Leave the page available

The temporary page is part of the report. Leave it available until the user is finished with it.

Remove it and its fixtures when the user asks, or when the surrounding workflow explicitly owns cleanup.

## Before you finish

| Mistake | Fix |
| --- | --- |
| Every axis run against every component | Keep only axes whose cue matches |
| Only single-axis cases tested | Add a few plausible high-risk seams |
| Cartesian product of every axis | Keep seams sparse and evidence-driven |
| English fixture treated as localization coverage | Use realistic EN / zh-Hant / ja shapes when language can vary |
| One unbreakable monster string used against a field that can never receive one | Stress only contract-valid or plausible production input |
| A predicted failure reported as observed | Render it, or mark observation `Not verified` |
| Harness missing real provider / tokens / parent sizing | Restore the minimum real environment |
| A rebuilt lookalike component in the harness | Import the real component |
| Fake theme tokens declared in the harness | Use the production theme mechanism or leave the mode to the viewer |
| Static snapshots claimed to prove transition behavior | Add a real sequence only when the component owns the transition |
| Break in the table but not on the page | Mark the affected scenario on the harness page |
| Clean run padded with polish suggestions | "Everything survived" is enough |
| Whole matrix rerun after a local fix | Recheck the failing case, baseline and dependent seams |
