---
name: komorebi-interface
description: Combines the `komorebi-*` skills into one evidence-based interface review across accessibility, layout, mobile embodied UX, writing, typography, color and UI polish, with cross-domain coherence and multilingual states kept intact.
---

# Interface review

This skill runs a cross-discipline interface review.

It routes the interface to the owning `komorebi-*` skills, gathers evidence, checks the seams between domains and consolidates one ranked verdict.

**Orchestration is all it owns.** Accessibility rules belong to `komorebi-accessibility`, structure and composition to `komorebi-layout`, touch ergonomics / grip / attention-to-action flow to `komorebi-mobile-ux`, copy to `komorebi-writing`, type to `komorebi-typography`, color to `komorebi-colors`, and visual polish / motion to `komorebi-ui`.

Never duplicate, weaken or override their rules here.

Change-scoped review of uncommitted work, branches and pull requests belongs to `interface-review`, which resolves version-control scope before handing the interface review back.

## Evidence, not taste

Press hard on confirmed failures and leave deliberate project choices alone.

A density, radius, asymmetry, typeface, color mood or writing voice you merely prefer differently is not a finding.

A visual choice becomes reviewable when there is evidence that it:

- breaks an owning domain rule;
- contradicts an established project source, approved reference or design token;
- harms comprehension, discoverability, accessibility or adaptability;
- behaves inconsistently across supported states or languages;
- visibly fails in the rendered interface.

The bar for reporting is evidence, not taste.

The bar for `Approve` is that you inspected what you claim to have inspected.

A short report from a real inspection beats a long report padded to look thorough. A clean review is a valid result.

## Do not average the interface

A holistic review is not a stack of disconnected domain reports.

The goal is to understand one user experience.

After the domain reviews, check the seams:

- writing × layout: does real copy still fit the intended composition?
- typography × layout: do line-height, wrapping and mixed-script density change grouping or hierarchy?
- color × accessibility: does the intended mood survive required contrast and state distinction?
- UI × accessibility: do hover, focus, press and motion remain perceivable without becoming noisy?
- imagery × layout: do crops, overlays and controls preserve the subject and focal point?
- layout × mobile ergonomics: does the visually expected action remain physically reasonable for the relevant grip, hand and device?
- UI × mobile ergonomics: do gestures, repeated actions and contextual controls avoid occlusion, regrip and motor ping-pong?
- UI × mobile timing: does touch acknowledge promptly, explain waiting and release the next action without decorative delay?
- accessibility × mobile timing: does transient or timed UI give enough perceive / decide / reach / act time and preserve a durable recovery path where needed?
- localization × everything: do EN / Traditional Chinese / Japanese remain the same interface rather than three unrelated compositions?

When one root cause crosses domains, assign it to the owner of the underlying rule and mention secondary effects in **Why**. Report it once.

## Core principles

### 1. Resolve the scope first

Infer the screen, flow, feature or workspace scope from the request and current project.

State the resolved scope in the output.

Also resolve the supported states relevant to that scope:

- normal / default;
- empty;
- loading / working;
- error;
- transient / timed feedback where the surface uses it;
- narrow width;
- larger text / zoom;
- light / dark where supported;
- hover / focus / pressed where relevant;
- EN / Traditional Chinese / Japanese where the surface supports them;
- RTL only where the product supports it;
- relevant phone / tablet holding or input modes where touch ergonomics materially affects the task.

Do not manufacture states the product does not have.

When the scope is too large to inspect credibly, narrow it to one complete flow: the one the request centers on, or failing that the entry path every user must pass through. State the boundary and what it excluded.

Never imply uninspected surfaces were reviewed.

### 2. Send a change to `interface-review`

A request naming a branch, pull request, commit range or uncommitted changes is a change review, not a screen review.

Route it to `interface-review`, which owns diff scope, changed-file expansion and finding status.

Do not guess a change scope here.

When `interface-review` hands a review back, this skill still owns consolidated severity, ranking, cap and verdict for the change-scoped findings.

### 3. Recon before judgment

Identify:

- framework;
- styling system;
- component library;
- design tokens;
- supported viewports;
- supported languages;
- light / dark or theme variants;
- preview, test or story command;
- approved visual references or design-system sources when they exist.

Then read the project interface guidance that actually applies: `CONTRIBUTING.md`, `CODING_STANDARDS.md`, `AGENTS.md`, `CLAUDE.md`, design-system docs, Storybook docs, interface ADRs or equivalent sources.

Name which you found, or that there are none.

A documented convention is not proof that the convention is good. It tells you **where** a systemic finding belongs.

When a shared token, component or guideline is the root cause, report it once against that owner and list affected surfaces as locations.

### 4. Use domain skills as sources of truth

Before reviewing, confirm that every owning skill below is available.

Review in this order so foundational failures are not hidden by polish:

1. `komorebi-accessibility`
2. `komorebi-layout`
3. `komorebi-mobile-ux` where phone / tablet reach, grip, occlusion, transient UI or interaction timing is relevant
4. `komorebi-writing`
5. `komorebi-typography`
6. `komorebi-colors`
7. `komorebi-ui`

Load and apply every available owner.

From a domain skill, take its principles, references and verification checks. Its standalone severity ladder and report format do not replace this consolidated skill's severity, cap or output format.

If an owner is unavailable, mark that domain `Not reviewed`, name the missing skill and continue. Do not recreate its rules from memory, borrow a neighboring skill or claim holistic coverage.

A domain can finish `Clear`. Do not invent a finding because the skill was loaded.

### 5. Inspect reality at the right surface

Use the evidence surface closest to the claim.

- Code / source proves declared structure, tokens, semantics and implementation.
- The rendered interface proves visual hierarchy, crop, wrapping, overlap, motion and actual affordance.
- Browser / device interaction proves focus, keyboard, scroll, hover, zoom, responsive behavior and observable state timing.
- Instrumented runtime timing can prove touch-to-feedback / result / next-action intervals; source constants alone do not prove perceived responsiveness.
- Real-device / realistic-posture testing is the strongest evidence for grip, regrip, reach comfort and repeated motor cost; a simulator can show geometry but not muscle effort.
- Real localized strings prove multilingual layout.
- Tests prove only what they actually assert.

Do not infer a visual failure from code when runtime behavior decides it.

Do not infer implementation correctness from a screenshot when source ownership decides it.

A green test, successful route or loaded screen is evidence; it is not automatically the completion condition for the experience being reviewed.

### 6. Review the rendered interface, not only the implementation

When visual or interaction judgment matters, inspect the real rendered state whenever available.

For EN / Traditional Chinese / Japanese surfaces, prefer real representative strings over a universal expansion percentage.

Check whether the same semantic hierarchy survives even when each language changes line breaks, optical density and geometry.

Do not force all languages to occupy identical shapes merely for screenshot symmetry.

### 7. Rank by user impact

Use one shared severity scale:

- `HIGH`: blocks a task, misleads the user, hides content or controls, causes data-loss risk, or creates a repeated systemic failure.
- `MEDIUM`: meaningfully harms comprehension, efficiency, adaptability, localization, discoverability or consistency.
- `LOW`: isolated polish with limited task impact.

Within a severity, rank by reach and leverage. A token or shared-component fix outranks the same symptom in one leaf.

**Escalation triggers.** Once the owning skill confirms one of these, it is `HIGH` on sight:

- interactive control with no accessible name;
- keyboard-reachable control with no visible focus indicator;
- pointer-only path with no keyboard equivalent where keyboard access is required;
- motion / autoplay ignoring `prefers-reduced-motion`;
- content or control clipped, overlapped or unreachable at supported narrow width or 200% zoom;
- body or control text failing the required contrast ratio;
- state or meaning carried by color alone;
- destructive action with no confirmation, undo or distinct treatment;
- important truncated content with no way to recover the full value;
- required content or control hidden behind an edge / disclosure with no discoverable cue;
- error with no recovery path;
- semantic color used against its meaning;
- state change carried by motion alone with no persistent non-motion cue.

These set severity, not ownership. The owning domain decides whether the symptom is actually present.

When more `HIGH` findings exist than the cap allows, list them first and state how many additional blockers were excluded by the cap.

### 8. Prefer the cheaper fix

Severity says how bad the problem is. This principle chooses the least expensive fix that actually resolves it.

Prefer, in order:

1. **Delete.** Remove the redundant separator, wrapper, cue, animation, badge or state.
2. **Recompose.** Move, regroup, reflow or reuse space before adding new chrome.
3. **Use the platform.** Native element, control, focus behavior or semantic primitive.
4. **Reuse the project.** Existing token, component, spacing step or motion curve.
5. **Correct the value.** Fix the wrong gap, radius, contrast pair, crop or timing.
6. **Add.** New wrapper, token, media query, affordance or ARIA only when the simpler options cannot solve it.

A step-6 fix when deletion or recomposition would solve the root cause is a weaker fix.

### 9. Preserve deliberate quietness

Do not mistake restraint for absence.

A quiet interface can be correct when:

- hierarchy is clear without oversized headings;
- controls are discoverable without every control becoming a filled button;
- empty space carries grouping or focus;
- asymmetric composition remains balanced;
- ambient content is alive without demanding attention;
- secondary guidance recedes once the user can proceed.

But quietness never excuses hidden controls, low contrast, tiny text, missing focus, ambiguous state or undiscoverable content.

### 10. Consolidate systemic findings

One root cause is one finding.

List every confirmed location in the same row rather than one row per occurrence.

Never pad to reach the cap. No findings is a valid review result.

### 11. Verify what can be verified

Run the safe relevant checks the project offers.

Verification can include:

- build / lint / tests;
- viewport resize;
- 200% zoom / larger text;
- keyboard navigation;
- reduced-motion behavior;
- light / dark themes;
- EN / zh-Hant / ja rendering;
- representative image crops;
- empty / loading / error states;
- scroll and progressive disclosure;
- interaction states.

A check you cannot run is **Not verified**, never a finding.

### 12. Review without mutating by default

Treat a review request as read-only.

Do not edit source unless the user also asks you to implement findings.

When implementation is requested, keep the consolidated findings as the change scope and re-run the relevant verification afterward.

## Before you finish

| Mistake | Fix |
| --- | --- |
| Six disconnected domain reports | One ranked findings table with one cross-domain synthesis |
| Visual claim inferred only from source | Inspect the rendered state or mark it `Not verified` |
| Screenshot treated as proof of implementation ownership | Read the source that owns the behavior |
| Green tests treated as proof the experience is complete | Verify the actual experience goal |
| Silent gaps in state / language coverage | List the states and locales actually inspected |
| Missing owning skill treated as covered | Mark the domain `Not reviewed` |
| Style preference promoted into a defect | Require user impact, project contradiction or owner-skill evidence |
| Every quiet surface treated as under-designed | Preserve restraint when discoverability and comprehension remain intact |
| Same root cause reported by multiple domains | Assign one owner and note secondary effects |
| Domain marked `Clear` without real evidence | Mark what was actually inspected |

## Review output format

The format lives in [review-format.md](review-format.md): scope and coverage, cross-domain synthesis, findings, verification and verdict.

A review is not finished until its findings are reported there.
