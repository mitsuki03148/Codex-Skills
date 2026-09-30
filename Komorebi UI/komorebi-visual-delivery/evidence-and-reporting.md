# Evidence and reporting

Visual QA needs the correct evidence surface and a small reporting vocabulary.

## Applicability first

Before reporting a check, classify it as:

- `Applicable` — the asset can genuinely fail this way;
- `N/A` — the check cannot apply to this asset / delivery;
- `Not verified` — the check applies, but evidence or execution was unavailable.

`N/A` is not a softer form of `Not verified`.

Examples:

- animation continuity on a static PNG → `N/A`;
- character consistency on a background texture with no recurring character → `N/A`;
- reference fidelity when a canonical reference exists but was not available to inspect → `Not verified`;
- export integrity when the export was not opened → `Not verified`.

## Reference claims

To claim style fidelity was checked:

- inspect the authoritative reference;
- inspect the actual output;
- compare the relevant style axes.

Memory is not a fidelity check.

## Character claims

To claim identity consistency:

- inspect the canonical anchor / model sheet;
- inspect the new work;
- compare stable identity anchors;
- account for pose and perspective.

A single “looks same” statement is weak evidence.

## Production claims

Source / layers can show:

- transforms;
- masks;
- layer order;
- asset references;
- timeline / export configuration.

But the rendered or exported artifact is stronger evidence for visible production defects. A rendered scene can show contact, support, depth and perspective cues; it does not certify engineering or simulation-grade physical correctness.

## Animation claims

Static frames cannot prove timing.

Normal-speed playback can reveal a problem but may not locate its cause.

Use playback plus neighboring-frame inspection when possible.

## Severity

Severity describes one issue.

### BLOCKER

Must be fixed before delivery because it materially affects correctness, identity or delivery integrity.

Examples:

- materially wrong reference language;
- character identity drift;
- obvious layer / mask / transform failure;
- broken animation continuity;
- wrong / missing export;
- corrupt transparency or missing required visual content.

### VISIBLE

Clearly visible at intended use and meaningfully lowers production quality, but does not invalidate the asset's identity or purpose.

Unresolved `VISIBLE` issues keep delivery `BLOCKED` unless the user explicitly accepts a named exception; if accepted, report `PASS WITH ACCEPTED EXCEPTION` and name the issue.

### MINOR

Small polish imperfection with limited visibility / impact at intended use.

A `MINOR` may remain only when repair cost or regression risk is disproportionate and the tolerance is named.

## Delivery status

### PASS

All applicable delivery-critical checks were performed and no unresolved material issue remains.

### PASS WITH MINOR TOLERANCE

Only named `MINOR` issues remain; they do not affect identity, required reference fidelity, continuity, correctness or intended use.

### PASS WITH ACCEPTED EXCEPTION

Use only when the user explicitly accepts every remaining `VISIBLE` issue for this delivery; name each accepted issue and its scope. No `BLOCKER` or applicable delivery-critical `Not verified` check may remain.

### BLOCKED

Use when:

- any `BLOCKER` remains;
- an unresolved `VISIBLE` issue remains without explicit accepted exception;
- an applicable delivery-critical check is `Not verified`;
- the actual final export has not been inspected when export is part of the delivery.

`N/A` does not block delivery.

## Reporting discipline

Report root causes, not every pixel.

Good:

`Hair mask retains a white matte fringe against the final dark background.`

Weak:

`Pixel at x=238 is white.`

When one cause affects many frames / assets, report it once and list the affected range.

Always state:

- what artifact / profile was checked;
- which checks were applicable;
- which were `N/A`;
- which were `Not verified`;
- what was fixed;
- what remains;
- final delivery status.

A short truthful report is better than a theatrical checklist.
