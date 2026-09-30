# Compositing and edge hygiene

Visual delivery often fails at seams.

Inspect the produced artifact, not only the layer names.

## Cutout / alpha checks

Look for:

- white fringe;
- black fringe;
- color matte contamination;
- jagged cutout;
- erased hair / thin stroke;
- accidental semi-transparent edge;
- holes;
- over-feathering;
- clipped soft shadow;
- opaque pixels in an intended transparent region.

## Three-background check

For important transparent assets, inspect against:

1. light background;
2. dark background;
3. representative destination background.

A halo that disappears on white may be obvious on dark green.

## Layer order

Check meaningful overlaps:

- hand in front of / behind object;
- hair against face / shoulder;
- foreground foliage;
- UI chrome over illustration;
- shadow under owner;
- particle behind / in front of subject.

One wrong z-order can make a correct drawing feel broken.

## Mask ownership

Check:

- correct layer is clipped;
- mask is not offset;
- transform did not detach mask;
- mask softness matches the intended edge language;
- one frame did not lose the mask.

## Blend and opacity

Look for:

- forgotten Multiply / Screen / Overlay;
- opacity left at diagnostic value;
- doubled shadow;
- hidden layer unexpectedly enabled;
- temporary adjustment layer leaking into final.

## Transform hygiene

Check:

- aspect ratio;
- uniform scale when required;
- pivot;
- rotation;
- mirroring;
- skew;
- perspective;
- registration to scene.

A visually plausible transform can still be wrong if it breaks character/model consistency.

## Residue

Before export, inspect for:

- guides;
- grids;
- crop marks;
- selection edges;
- transform handles;
- debug labels;
- temporary rectangles;
- checkerboard baked into raster;
- test watermark;
- placeholder art;
- hidden notes accidentally rendered.

## Intended texture vs defect

Do not clean intentional imperfection merely because it is irregular.

Preserve:

- pencil wobble;
- watercolor bleed;
- rough paper edge;
- hand-painted color variation;

when they are part of the approved style.

Clean accidental production residue, not life.
