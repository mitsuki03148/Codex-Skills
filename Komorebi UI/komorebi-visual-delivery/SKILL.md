---
name: komorebi-visual-delivery
description: Pre-work reference and character locking plus pre-delivery QA for visual assets, compositing, animation and exported media.
---

# Komorebi Visual Delivery

This skill is the **visual production quality owner** inside the Komorebi Codex UI Skills suite.

It does not decide how an interface should be designed. It protects visual work from drifting before production and from leaving the workshop with visible production defects.

Its two gates are:

**LOCK BEFORE WORK → VERIFY BEFORE DELIVERY**

Use it for illustration, recurring characters, layered composites, cutout / transparent assets, sprites, animation, image-led UI assets and exported visual media.

Do not run the full skill against a text-only or ordinary layout-only UI task.

## Ownership

This skill owns:

- approved-reference fidelity;
- recurring character / visual identity consistency;
- series consistency;
- cutout, alpha and compositing hygiene;
- layer / mask / transform integrity;
- frame-to-frame animation continuity;
- visual export integrity;
- spatial / physical plausibility of depicted objects and their relationships in a rendered scene.

This checks whether a depicted scene reads coherently; it does not own interface composition, hierarchy, spacing, control design or usability.

Route other questions to their owners:

- interface composition / hierarchy → `komorebi-layout`; this skill checks fidelity to an approved composition reference but does not redesign it;
- interface visual polish / motion language → `komorebi-ui`;
- touch ergonomics / human interaction timing → `komorebi-mobile-ux`;
- typography → `komorebi-typography`;
- approved reference-palette fidelity → this skill; palette design / semantic color roles → `komorebi-colors`; contrast requirements → `komorebi-accessibility`, with color-pair measurement by `komorebi-colors`;
- copy → `komorebi-writing`;
- accessibility and contrast requirements → `komorebi-accessibility`;
- change scope / causality → `interface-review`;
- whole-interface review / verdict → `komorebi-interface`;
- hostile valid component-state stress → `break`.

If preflight exposes a problem outside this owner, route it. Do not redesign the interface from inside this skill.

---

## 1. Choose the applicable asset profile

Do not run one giant checklist against every asset.

| Asset type | Usually applicable |
| --- | --- |
| One-off illustration | reference fidelity when authoritative; export integrity |
| Recurring character / series | reference lock; character lock; series continuity; export |
| Transparent / cutout asset | reference fidelity when relevant; edge / alpha; export |
| Layered composite | reference fidelity when relevant; masks / layers / transforms; spatial / physical plausibility when scene relationships matter; export |
| Room / environment / furniture / prop render | reference fidelity when relevant; spatial / physical plausibility; export; compositing when layered |
| Character × prop / furniture scene | character continuity; spatial / physical plausibility; compositing when relevant; export |
| Sprite / animation | reference / character lock when relevant; frame continuity; compositing; spatial / physical plausibility when orientation/contact/depth changes; loop / timing export |
| UI visual asset / icon set | approved visual language; set consistency; crop / alpha / export variants |
| Text-only / ordinary UI | usually `N/A`; use the other UI owners |

`N/A` = the check genuinely cannot apply.

`Not verified` = it applies, but evidence was unavailable or the check was not run.

Never use `N/A` to hide an unperformed applicable check.

---

# Gate A — LOCK BEFORE WORK

## 2. Resolve the visual contract

Before final production, identify only what matters for this asset:

- intended use and delivery size;
- authoritative reference(s), if any;
- whether recurring identity must remain stable;
- output format, transparency, animation or series requirements.

Reference authority, when present:

1. explicitly approved canonical reference;
2. approved model / style sheet;
3. latest approved output the user identified as correct;
4. multiple references with explicit roles.

Do not average conflicting references silently.

If no reference-fidelity requirement exists, mark it `N/A` rather than inventing one.

See [reference-lock-and-style-fidelity.md](reference-lock-and-style-fidelity.md).

## 3. Style Lock

When reference fidelity matters, extract the visible style through six axes:

1. line / edge language;
2. shape language;
3. proportion language;
4. color / value language;
5. rendering / material language;
6. composition / spacing mood.

For the relevant axes, record:

- **Must Match**
- **Can Vary**
- **Must Avoid**

Do not stop at labels such as “cute”, “soft”, “Japanese” or “cartoon”. Translate them into observable traits.

The composition / spacing axis records what an approved visual reference looks like; it does not decide whether a new interface hierarchy or layout is effective. Route that design judgement to `komorebi-layout`.

## 4. Character Lock

When identity must persist, lock stable anchors visible in the approved reference:

- head-to-body proportion;
- silhouette;
- face shape;
- eye / brow character and spacing;
- hair silhouette / fringe / volume;
- shoulder / torso / limb proportion;
- recurring clothing / accessory landmarks;
- age impression, posture and expression energy.

Separate identity anchors from pose-, perspective- and allowed-variant changes.

The target is **identity continuity, not tracing**.

See [character-model-and-series-consistency.md](character-model-and-series-consistency.md).

## 5. Keep one approved anchor

Use an approved image / model sheet as the canonical anchor when the toolchain permits.

Do not restart a series from prose alone when image-reference continuity is available.

A newer generation does not automatically become the new authority.

## 6. Pre-work gate

State only applicable rows:

| Gate item | Status |
| --- | --- |
| Authoritative reference | `LOCKED` / `N/A` / `BLOCKED` |
| Style Lock | `LOCKED` / `N/A` / `BLOCKED` |
| Character Lock | `LOCKED` / `N/A` / `BLOCKED` |
| Output / format contract | `LOCKED` / `N/A` / `BLOCKED` |

A material unknown that can change the asset remains unknown or gets clarified. Do not silently invent the contract.

---

# Gate B — VERIFY BEFORE DELIVERY

## 7. Check fidelity by axis

Do not conclude with “looks close” or “same vibe”.

For applicable reference / character checks:

- compare the actual reference and actual output;
- name the style axis or identity anchor that drifted;
- distinguish permitted variation from real drift;
- judge at intended use size before zooming for diagnosis.

Overlays, ratios and silhouette comparisons are diagnostics, not truth. Respect pose, perspective, lens and foreshortening.

For a series, compare a contact sheet / montage rather than relying on memory.

## 8. Check production integrity

Use only the checks that apply to the asset.

### Compositing / edge hygiene

Inspect cutout edges, alpha, masks, depth order, blend / opacity state and temporary residue. For important transparent assets, check against light, dark and representative destination backgrounds.

See [compositing-and-edge-hygiene.md](compositing-and-edge-hygiene.md).

### Transform / layer integrity

Check for accidental stretch, mirror, pivot / perspective mismatch, wrong mask owner, duplicate / ghost layers and one-frame layer-order mistakes.

### Spatial / physical plausibility

For rooms, environments, furniture, props, layered scenes, character-object interaction and relevant animation, verify that the rendered world is visibly coherent.

Check only what applies: object orientation, contact/support, gravity cues, depth/occlusion, perspective/ground plane, relative scale, obvious functional orientation, grounding cues, character × prop relationship, and continuity of these relationships across frames.

This is not simulation-grade physics or industrial-design certification.

**Stylization may bend physics; accidental impossibility is the defect.**

See [spatial-and-physical-plausibility.md](spatial-and-physical-plausibility.md).

### Animation / series continuity

For time-based output, inspect:

1. normal-speed playback;
2. slow / frame diagnosis;
3. neighboring frames / contact sheet.

Look for pop, flicker, transform jump, mask / layer swap, missing / duplicate frame, character-model drift and broken loop boundaries.

Intentional squash, stretch or smear is not a defect when it belongs to the approved animation language.

See [animation-and-series-continuity.md](animation-and-series-continuity.md).

## 9. Verify the actual export

The editor state is not the delivered artifact.

Inspect the final file for the checks relevant to its format: correct variant, dimensions, crop, transparency, color / matte, compression, frame order / duration, playback speed, loop and missing states / assets.

See [export-and-delivery-preflight.md](export-and-delivery-preflight.md).

## 10. Re-check after repair

A technical cleanup can damage the approved visual language.

If a fix changes edge, shape, color, proportion, transform or interpolation, re-check the relevant reference / identity seam and re-open the final export.

## 11. Pre-delivery pass

Run one calm pass with only applicable checks:

1. whole artifact at intended size;
2. reference fidelity — or `N/A`;
3. character / series consistency — or `N/A`;
4. edge / alpha / compositing — or `N/A`;
5. transform / layer integrity — or `N/A`;
6. spatial / physical plausibility — or `N/A`;
7. animation continuity — or `N/A`;
8. actual export integrity;
9. regression after repair, when relevant.

Finish the applicable pass after fixes; do not stop at the first repaired issue.

---

# Severity and status

## Issue severity

### BLOCKER

Materially wrong and must be fixed before delivery: identity / reference failure, obvious mask / layer / transform break, broken animation continuity, wrong / missing export, corrupted transparency or missing key visual content.

### VISIBLE

Clearly visible at intended use and meaningfully lowers production quality without invalidating the asset's identity or purpose.

Unresolved `VISIBLE` issues keep delivery `BLOCKED` unless the user explicitly accepts a named exception; if accepted, report `PASS WITH ACCEPTED EXCEPTION` and name the issue.

### MINOR

Small imperfection with limited visibility / impact. It may remain only when repair cost or regression risk is disproportionate and the tolerance is named.

See [evidence-and-reporting.md](evidence-and-reporting.md).

## Delivery status

### PASS

All applicable delivery-critical checks were performed and no unresolved material issue remains.

### PASS WITH MINOR TOLERANCE

Only documented `MINOR` issues remain; identity, required fidelity, continuity, correctness and intended use are unaffected.

### PASS WITH ACCEPTED EXCEPTION

Use only when the user explicitly accepts every remaining `VISIBLE` issue for this delivery; name each accepted issue and its scope. No `BLOCKER` or applicable delivery-critical `Not verified` check may remain.

### BLOCKED

Use when:

- a `BLOCKER` remains;
- a `VISIBLE` issue remains without explicit accepted exception;
- an applicable delivery-critical check is `Not verified`;
- the actual final export has not been inspected when export is part of delivery.

`N/A` does not prevent `PASS`. `Not verified` is not `N/A`.

---

## Evidence discipline

- reference + output side by side → style / character fidelity;
- source / layers → declared masks, transforms, order, timeline and asset references;
- rendered artifact → visible edge / compositing / transform defects and scene contact / support / depth relationships;
- playback + neighbors → animation continuity;
- actual export → delivery-file correctness.

Do not claim a fidelity check without inspecting the authoritative reference.
Do not claim animation timing from static frames.
Do not convert absence of evidence into `PASS`.

---

## Cross-skill routing

| Question | Owner |
| --- | --- |
| Interface composition / hierarchy | `komorebi-layout` |
| Interface visual polish / motion language | `komorebi-ui` |
| Touch placement / human timing | `komorebi-mobile-ux` |
| Reference fidelity / recurring character consistency | `komorebi-visual-delivery` |
| Masks / layers / transforms / frame integrity | `komorebi-visual-delivery` |
| Final exported visual asset | `komorebi-visual-delivery` |
| Contrast requirements / accessibility | `komorebi-accessibility` |
| Contrast measurement | `komorebi-colors` |
| Change scope / affected surfaces | `interface-review` |
| Whole-interface review / verdict | `komorebi-interface` |
| Hostile valid component scenarios | `break` |

Within the Komorebi Codex UI Skills suite, invoke this skill when visual assets, illustration, recurring characters, compositing, animation or exported-media fidelity materially affect the work.

---

## Before you finish

| Mistake | Better move |
| --- | --- |
| Full checklist on every asset | Choose the asset profile; mark true non-applicable checks `N/A` |
| `N/A` used because a check was inconvenient | Use `Not verified` |
| “Looks similar enough” | Name the style axis / identity anchor |
| Reference remembered from earlier | Re-open the authoritative reference |
| References averaged together | Choose authority and permitted variation |
| Pixel overlay treated as truth | Use it only as diagnostic evidence |
| Character checked one image at a time | Compare the series / contact sheet |
| Correct source assumed to mean correct export | Inspect the exported artifact |
| One good frame assumed to mean good animation | Check temporal continuity |
| Edge cleanup removes intentional texture | Re-check fidelity after cleanup |
| Microscopic 800% artifact blocks delivery | Judge at intended use, then zoom to diagnose |

---

## Reporting

Keep the report short and asset-specific.

### Visual Delivery Preflight

**Artifact** — name / path / type / intended use

**Applicable profile** — e.g. `Character series + transparent PNG`, `Layered composite`, `Animation`, `Static illustration`

**Pre-work locks**
- Reference: `LOCKED` / `N/A` / `BLOCKED`
- Style: `LOCKED` / `N/A` / `BLOCKED`
- Character: `LOCKED` / `N/A` / `BLOCKED`
- Output contract: `LOCKED` / `N/A` / `BLOCKED`

**Pre-delivery checks**

| Check | Result | Evidence |
| --- | --- | --- |
| Reference fidelity | `PASS` / `N/A` / `Not verified` | ... |
| Character / series consistency | `PASS` / `N/A` / `Not verified` | ... |
| Edge / alpha / compositing | `PASS` / `N/A` / `Not verified` | ... |
| Transform / layer integrity | `PASS` / `N/A` / `Not verified` | ... |
| Spatial / physical plausibility | `PASS` / `N/A` / `Not verified` | ... |
| Animation continuity | `PASS` / `N/A` / `Not verified` | ... |
| Actual export integrity | `PASS` / `N/A` / `Not verified` | ... |

**Issues**

| Severity | Area | Evidence | Issue | Fix / disposition |
| --- | --- | --- | --- | --- |

**Delivery status** — `PASS` / `PASS WITH MINOR TOLERANCE` / `PASS WITH ACCEPTED EXCEPTION` / `BLOCKED`

Never write `PASS` for an applicable check that was not actually performed.
