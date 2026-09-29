# Scope resolution

Turning a review target into a trustworthy file list and then into representative affected surfaces.

The scope block is part of the evidence. If it names the wrong base, wrong ref, wrong file count or an unspoken cutoff, every later conclusion inherits that error.

## Default branch

Prefer the repository's actual default branch metadata. Try the remote HEAD, then the hosting provider's repository metadata, then local configuration. Do not guess `main` merely because it is common.

If no remote exists, a local `main` / `master` fallback can be used only when named explicitly in the scope block.

## Targets

Accepted targets:

- `working`;
- `staged`;
- `branch`;
- `pr <n>`;
- a bare ref;
- explicit `<a>..<b>` or `<a>...<b>`.

For a branch review, compare against the merge base.

For an explicit range, preserve the dots the user wrote. Two-dot and three-dot ranges answer different questions.

Any target containing uncommitted work must include untracked files as well as tracked diffs.

## Pull requests

Fetch the PR head into a non-working-tree ref and review that ref in place.

Read unchanged context from the same reviewed ref. Do not mix a PR diff with working-tree source.

Use the PR title/body as stated intent; use commit subjects when that material is absent.

Line citations must resolve against the head ref declared in the scope block.

## Awkward repository states

Stop rather than guess when the base cannot be resolved.

Detect and name states such as:

- detached HEAD;
- shallow history with no merge base;
- mid-rebase;
- mid-merge;
- mid-cherry-pick;
- unrelated histories;
- repository with no commits.

A scope that cannot be named precisely cannot support a trustworthy change review.

## Nothing to review

When the tree is clean and HEAD is not ahead of the merge base, gather enough facts to make the next choice legible:

- current branch;
- clean / dirty state;
- ahead count;
- last commit SHA and subject;
- open PR for the current branch where available.

Then offer:

1. the open PR, when one exists;
2. a target the user names;
3. the last commit, shown by SHA and subject;
4. a whole-repository audit routed directly to `komorebi-interface`.

Never turn “nothing changed” into an implicit `HEAD~1..HEAD` review.

## Renames

Treat a rename as continuity unless the content changed.

Use rename detection strong enough to catch moved-and-edited files. Do not report unchanged content as delete + add merely because the path changed.

## Excluded paths

Exclude machine-authored / vendored material from the direct code-review inventory and name the exclusions.

Typical categories:

| Category | Examples |
| --- | --- |
| Lockfiles | package / pnpm / yarn / bun / Cargo / composer / Gem / poetry / uv locks |
| Snapshots and generated test output | `__snapshots__/`, `*.snap`, reports, test artifacts |
| Build output | `dist/`, `build/`, `.next/`, coverage, source maps |
| Generated source | generated clients, emitted declarations, codegen output |
| Vendored code | `vendor/`, `third_party/`, `node_modules/` |
| Binary asset bytes | images, fonts, video, PDFs |

### Asset exception

An asset file's bytes may not be source-reviewable, but introducing or swapping that asset can still be an interface change.

Review the code / manifest / content record that places the asset and inspect the rendered surface when the visual claim depends on it.

Examples:

- new font → `komorebi-typography` through actual rendering and fallback behavior;
- new image / crop → `komorebi-ui`, `komorebi-layout` and accessibility through placement, composition and alt / semantic treatment;
- new icon asset → `komorebi-ui` through state, optical weight and direction;
- new color token source → `komorebi-colors` through semantic consumers.

Do not treat “binary excluded” as “visual effect excluded”.

## Expanding to consumers

A diff is not a surface.

### One hop by default

For a leaf component, inspect direct rendered consumers.

### Two or more hops for shared primitives

Tokens, themes, typography primitives, color semantics, icon primitives, layout primitives and shared interaction components can have much larger blast radii.

Expand far enough to find representative rendered contexts, then stop when additional consumers are materially redundant.

### Representative consumer selection

Order candidate consumers by a combination of reach and **context diversity**.

Prioritize:

1. route / layout entry points and global chrome;
2. consumers with high reuse;
3. consumers that expose a different composition or failure seam;
4. same feature / package proximity when the above tie.

Useful diversity dimensions include:

- narrow / wide container;
- EN / zh-Hant / ja;
- light / dark;
- normal / loading / error / selected / disabled;
- dense utility surface / spacious editorial or image-led surface;
- text-only / media composition;
- local component / persistent chrome.

A bounded review should usually inspect a small representative set rather than every consumer. Do not use a hard number as a substitute for judgement; state the inspected set, the skipped count and why the inspected contexts were representative.

### Search the reviewed ref

Consumer discovery must search the reviewed ref, not the working tree, when those differ.

For tokens and semantic names, search the token itself rather than only files importing its definition.

## Localization as blast radius

When the change affects typography, visible copy, layout width, icons tied to reading direction or text-over-image composition, supported locales are part of the blast radius.

Do not require all locales for every change. Expand locale coverage only where language can materially change geometry, glyphs, punctuation, meaning or direction.

For this project's adapted visual stack, EN / Traditional Chinese / Japanese are the key multilingual seams when those locales are supported by the product under review.

## Scope completion check

Before handing the review upward, be able to answer:

- What exact change did I review?
- What did I exclude?
- Which surfaces can this change reach?
- Which representative consumers did I inspect?
- Which materially different contexts did those consumers cover?
- What did I not inspect?
- Are my citations and source reads from the same ref I claim to review?

If any answer is unclear, scope resolution is not finished.
