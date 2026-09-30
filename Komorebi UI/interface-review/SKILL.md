---
name: interface-review
disable-model-invocation: true
description: Reviews a branch, pull request, range or working-tree change across interface domains, resolving scope, affected surfaces and regressions before handing evidence to komorebi-interface.
---

# Change review

This skill reviews a **change**, not a screen and not the whole codebase.

It owns four things:

1. resolving exactly what changed;
2. expanding changed files to the user-facing surfaces they can affect;
3. reading both added and removed behavior;
4. classifying findings by causality: `Introduced`, `Regression`, or `Pre-existing`.

Domain rules belong to the `komorebi-*` skills. Severity, consolidation, coverage, the cap and the verdict belong to `komorebi-interface`.

Correctness, tests, security and general performance belong to the project's normal code review. Name such a concern once and route it there rather than absorbing it into the interface review.

## Review the change, not the codebase

The useful question is not “what is wrong in these files?” It is:

**What did this change make newly true, newly false, newly visible, newly hidden or newly fragile?**

Read the complete change before judging it. Stated intent matters because an interface can regress by omission: a new variant added without its loading state, a new string added without one locale, a token changed without checking the surfaces that consume it.

Stay mostly quiet about legacy problems the change merely passed through. A few high-value pre-existing observations can be useful; turning a change review into a repository audit is not.

## 1. Resolve the change scope first

The invocation is the target. Accepted targets and the exact resolution rules live in [scope-resolution.md](scope-resolution.md).

With no explicit target, resolve in this order:

1. branch work ahead of the merge base **plus** uncommitted work;
2. otherwise uncommitted work;
3. otherwise no change — ask rather than invent one.

Always state committed and uncommitted counts separately.

Exclude generated / vendored / machine-authored material from the reviewed file list, but keep user-facing asset changes represented through the code or manifest that places them in the interface.

## 2. A diff is evidence, not the surface

Changed files tell you where to start. They do not tell you where the user experiences the change.

Expand to affected surfaces.

### Direct components

For a changed leaf component, inspect its direct rendered consumers.

### Shared primitives, tokens and themes

For a shared primitive, token, typography rule, color semantic, icon primitive or theme value, expand farther because one line can affect many screens.

### Choose representative consumers, not five near-duplicates

A bounded review still needs diversity.

When there are more consumers than can be inspected credibly, choose a small representative set by **different failure surfaces**, not importer count alone. Prefer consumers that differ in ways that can expose different behavior:

- narrow vs wide container;
- dense utility UI vs spacious / image-led composition;
- EN vs Traditional Chinese vs Japanese where the product supports them;
- light vs dark appearance;
- normal vs loading / error / selected / disabled state;
- text-only vs media / illustration composition;
- local feature use vs shared global chrome;
- phone vs tablet, and held-touch vs desk/pointer mode, when a change alters frequent touch placement, gesture paths or persistent controls.

Reach still matters. A global route or heavily reused component is valuable evidence, but five consumers with the same geometry are weaker than three that expose genuinely different seams.

State what you inspected and what you did not.

## 3. Preserve source truth across refs

For a pull request or named ref, read files from the reviewed ref. Do not silently read the working-tree copy when it can differ.

Cite line numbers against the head ref declared in the scope block.

For uncommitted work, distinguish staged, unstaged and untracked material where that distinction matters.

Never claim a surface was inspected from source when runtime behavior is what determines the result.

## 4. Read the removed side as carefully as the added side

Regressions often live in what disappeared.

Use [removed-signals.md](removed-signals.md) as a **lead list**, never as a verdict list.

For each suspicious removal:

1. inspect the surrounding hunk;
2. look for an equivalent replacement in the same change;
3. route the remaining signal to the owning `komorebi-*` skill;
4. report it only if that owner confirms the interface got worse.

A deletion can be an improvement. Removing a border, animation, wrapper, token or helper label is not a regression merely because something vanished.

## 5. Classify causality, not proximity

Every confirmed finding gets one status:

- `Introduced` — the change created the problem;
- `Regression` — the change removed or weakened behavior that was previously sound;
- `Pre-existing` — the issue already existed and the change did not cause it.

A line three rows from a hunk is not automatically introduced.

Likewise, a token or primitive changed in one file can create a regression far away from the hunk. Causality follows dependency and rendered behavior, not physical distance in the diff.

Confirm ambiguous cases against the base ref.

## 6. Hold the change to its stated intent

Read PR title/body, linked issue where available and commit subjects.

Look for incomplete interface promises:

- a new state or variant implemented only on the happy path;
- a new component without the states it actually supports;
- a new visible string missing from a maintained translation catalogue;
- one of EN / zh-Hant / ja updated while the product claims support for all three;
- a new media treatment that only works at one crop or viewport;
- a theme/token change validated in one appearance only;
- a motion or transition change whose final state is correct but whose continuity is broken;
- a shared primitive updated without checking representative consumers.

Do not turn unrelated scope creep into an interface finding.

## 7. Treat cross-domain seams as first-class evidence

A change can look correct inside one owner and fail at the seam between owners.

Examples:

- typography × layout — a new CJK line-height breaks card height;
- colors × accessibility — a softer semantic token loses required contrast;
- UI × layout — a new shadow / surface layer obscures spatial grouping;
- UI × continuity — a new animation resets a component before moving it;
- writing × localization — a translated label changes the geometry of a peer action row;
- imagery × layout — a new crop removes the quiet region that held overlay text;
- layout / UI × mobile ergonomics — a relocated repeated action is visually coherent but now forces repeated regrip or finger travel in a supported phone / tablet posture;
- UI × mobile timing — the final state is correct but the change delays acknowledgement, flashes loading UI, blocks the next action or destabilizes the tapped region;
- accessibility × mobile timing — a new transient timeout leaves too little time to perceive, decide, reach or recover.

The finding still belongs to one owning domain rule. The seam explains the blast radius and the user impact; it does not create another domain.

When a change moves a bottom bar, toolbar, gesture target, floating action, row action or other repeated touch control, include `komorebi-mobile-ux` in the affected-domain routing and expand to representative mobile / tablet configurations where that placement actually matters.

Also include `komorebi-mobile-ux` when a change alters tap acknowledgement, async working state, loader onset, transient timeout, long-press / double-tap recognition, duplicate-submit prevention or whether animation delays the next action. Route accessibility requirements and motion styling to their own owners rather than duplicating them here.

## 8. Removed visual signals need context

Some visual removals are healthy simplification.

Do not flag the removal of:

- a border when space or a surface already carries the grouping;
- a shadow when depth no longer needs it;
- an entrance animation when content is already present;
- a filled icon when another persistent state cue remains;
- a decorative color when it carried no semantic responsibility.

Only route it as a regression lead when the removal may have taken away meaning, discoverability, state, hierarchy, readability, continuity or accessibility.

## 9. Hand the review to `komorebi-interface`

Hand off:

- the resolved scope block;
- affected surfaces inspected;
- representative consumers and skipped coverage;
- every confirmed finding with `Introduced` / `Regression` / `Pre-existing` status;
- verification performed and `Not verified` claims;
- any cross-domain seam relevant to the finding.

`komorebi-interface` applies domain routing, severity, consolidation, cap and verdict.

If `komorebi-interface` is unavailable, report the resolved scope and inventory, name the missing owner and stop. Do not invent a replacement severity system.

## 10. Never mutate the working tree

A change review is read-only, including checkout state.

Fetching refs is allowed because it does not rewrite the author's working files. Do not checkout, switch, stash or otherwise disturb the tree.

Rendered verification must also preserve the author's workspace. Use an isolated worktree when runtime verification is requested or naturally available.

## 11. Verify only what the evidence surface can prove

Source can prove declarations and ownership.

Rendered output can prove visual composition, wrapping, crop and visible state.

Interaction can prove keyboard flow, interruption and transitions.

Real localized strings can prove localization geometry.

A passing build does not prove a visual experience. A screenshot does not prove an interaction. A diff does not prove runtime behavior.

Mark what you could not verify as `Not verified` rather than inflating the claim.

## Before you finish

| Mistake | Fix |
| --- | --- |
| One stray edit reviewed instead of branch work | Resolve merge-base branch scope before falling back to the dirty tree |
| Last commit reviewed because there was no change | State repository facts and ask what target to review |
| Hunks reviewed without their surfaces | Expand to rendered consumers |
| Five nearly identical consumers inspected | Prefer representative failure contexts over redundant coverage |
| Only added lines read | Inspect removals for lost behavior and equivalent replacements |
| Removal itself treated as regression | Route it as a lead; deletion can be simplification |
| Finding status inferred from line proximity | Follow causality against the base ref |
| Token change treated as local | Expand to representative consumers across themes / locales / compositions |
| Visual claim inferred from source only | Render it or mark it `Not verified` |
| EN fixture treated as localization coverage | Inspect supported locales where geometry or meaning can change |
| PR checked out into the author's tree | Fetch the ref and read it in place or use an isolated worktree |
| Severity / cap restated here | Defer to `komorebi-interface` |

## Review output format

Open with the scope block:

| Field | Value |
| --- | --- |
| Target | `branch`, `working`, `staged`, `pr 482`, or the entered range |
| Base ref | `origin/main` at `a1b2c3d` |
| Head ref | `refs/remotes/pr/482` at `e4f5g6h` |
| Commits | 7 committed, 2 files uncommitted |
| Files in scope | 12 after exclusions |
| Excluded | named generated / vendored / machine-authored paths |
| Surfaces expanded | inspected representative rendered consumers; state what was skipped |

Then use `komorebi-interface`'s consolidated coverage, evidence, findings, synthesis, verification and verdict format, adding a `Status` column to findings:

| Severity | Domain | Status | Location | Evidence | Before | After | Why |
| --- | --- | --- | --- | --- | --- | --- | --- |
| HIGH | Accessibility | Regression | `src/Dialog.tsx:42` | Base had an accessible name; head does not | `aria-label="Close"` existed | Restore an accessible name | The change removed the only programmatic name |

With no `Introduced` or `Regression` findings, state **“No actionable interface findings in this change.”**

Pre-existing findings are optional, at most three, and explicitly outside the change verdict.

The final `Block` / `Approve` decision comes from `komorebi-interface` and covers `Introduced` and `Regression` findings only.
