# Export and delivery preflight

The final file is the delivered artifact.

Run only the section matching the actual delivery format; mark unrelated formats `N/A`.

Inspect it after export.

## Static image

Verify as applicable:

- correct file;
- correct variant;
- dimensions;
- aspect ratio;
- resolution / pixel density;
- transparent background;
- alpha edge;
- color appearance;
- no unexpected crop;
- no stale draft;
- no hidden layer rendered;
- no guide / overlay residue.

## SVG

Verify:

- viewport / viewBox;
- crop;
- transparent regions;
- strokes;
- masks / clip paths;
- unsupported filters where relevant;
- text converted / preserved according to project need;
- external dependencies not accidentally missing.

## GIF / animated image

Verify:

- frame count;
- frame order;
- frame duration;
- loop;
- transparency;
- matte contamination;
- disposal / ghosting;
- final-to-first continuity.

## Video

Verify:

- dimensions;
- aspect ratio;
- frame rate;
- duration;
- audio only when expected;
- color appearance;
- first / final frames;
- compression;
- playback at normal speed.

## Delivery package

Verify:

- filename;
- version;
- requested formats;
- variant completeness;
- final vs draft;
- source / export distinction when both are delivered.

## Intended-size pass

Inspect the output at the size the user will actually see.

Then zoom only to investigate suspicious seams.

Avoid wasting time polishing invisible microscopic defects unless the asset is intended for reuse at larger scale.

## Regression after fix

After any meaningful repair:

- re-open the final export;
- re-check the repaired defect;
- re-check neighboring seams;
- re-check reference / character fidelity if the repair changed shape, edge, color or proportion.

A fix is not complete until the new export is inspected.
