# Review output format

This is the consolidated format for a review orchestrated by `komorebi-interface`.

A domain skill reporting on its own keeps the smaller format in its own `## Reporting` section.

## Scope and coverage

State:

- the exact screen / flow / feature reviewed;
- stack and styling conventions;
- project interface / design sources found in recon;
- supported states included;
- supported languages actually inspected;
- any review boundary or excluded surface.

Then show coverage:

| Domain | Evidence inspected | States / locales | Result |
| --- | --- | --- | --- |
| Accessibility | Files, components, runtime states or checks | e.g. default + keyboard + 200% zoom | Findings count or `Clear` |

Include every domain listed by `komorebi-interface`.

`Clear` means genuinely inspected with no actionable finding.

`Not reviewed` must explain why.

## Cross-domain synthesis

Before the findings table, write up to three short root-level observations when they materially help the user understand the interface as one system.

Examples:

- one shared component causes both wrapping and hierarchy problems;
- a visual treatment is fine in English but breaks layout in Japanese;
- controls are individually accessible but the composition makes their order unclear;
- the interface is structurally sound and the remaining issues are isolated polish.

Do not use this section for vibes, praise or a second findings list. Omit it when the table already tells the story.

## Findings

One table, ordered by severity and then reach:

| Severity | Domain | Location | Evidence | Before | After | Why |
| --- | --- | --- | --- | --- | --- | --- |
| HIGH | Accessibility | `src/Dialog.tsx:42` | Keyboard + source | `<button><XIcon /></button>` | Add `aria-label="Close"` and hide the icon from the accessibility tree | Icon-only control has no accessible name |

Rules:

- **Severity** comes from `komorebi-interface`.
- **Domain** is the owning skill without the `better-` prefix.
- **Location** cites `path/to/file:line`. When there is no source file, cite the exact screen / state / artifact.
- **Evidence** says what proves the finding: source, rendered state, browser interaction, localized fixture, test, screenshot or another concrete surface.
- **Before / After** show the current implementation and the smallest actionable replacement.
- **Why** names the principle and user impact, including secondary cross-domain effects where useful.

Each row is one root cause.

Consolidate repeated symptoms into one row and list every affected location.

Respect the finding cap.

With no findings, omit the table and state:

`No actionable interface findings.`

Do not invent low-severity polish to avoid an empty table.

## Verification

Separate:

### Passed

List each check or interaction, exact command / steps, and observed result.

### Not verified

List checks that matter but could not be run.

Examples include:

- physical keyboard;
- real device;
- production font loading;
- one supported locale;
- reduced-motion state;
- dark mode;
- a server-driven error state.

`Not verified` is a coverage boundary, not a finding.

## Verdict

End with one of two:

- `Block`: one or more `HIGH` findings remain.
- `Approve`: no `HIGH` findings remain within the coverage actually reported.

`MEDIUM` and `LOW` findings remain in the table as work to do.

Do not issue `Approve` if a required domain was not reviewed and the user asked for a holistic review. Narrow the stated scope instead, or mark the review incomplete.

## Change-scoped reviews

When `interface-review` resolves scope from version control, it supplies the change-scope block, finding status and change-scoped format.

Severity, ranking, cap and verdict still come from `komorebi-interface`, and apply to `Introduced` and `Regression` findings as defined by the change-review owner.

Do not silently mix pre-existing findings into the change verdict.
