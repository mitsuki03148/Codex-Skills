# Animation and series continuity

Animation is continuity over time.

Use the animation-specific checks only for actual time-based or frame-sequence output. For a static asset, animation continuity is `N/A`.

A sequence can contain individually attractive frames and still fail as motion.

## Three-pass inspection

### Pass 1 — normal speed

Watch without stopping.

Ask:

- did anything pop?
- did the character suddenly feel different?
- did depth flip?
- did the motion hesitate?
- did the loop bump?

### Pass 2 — slow diagnosis

Inspect the suspicious region.

Look for:

- one-frame transform jump;
- duplicated / missing frame;
- layer swap;
- mask pop;
- scale pulse;
- unexpected rotation;
- alpha flash;
- shadow discontinuity;
- expression / face-model drift.

### Pass 3 — contact sheet / neighbors

Compare nearby frames side by side.

This is especially useful for:

- face shape;
- head size;
- eye spacing;
- hair volume;
- limb thickness;
- layer order;
- overlay residue.

## Transform continuity

Track changes through time.

A property can change, but it should change because the motion calls for it.

Unexpected one-frame spikes are suspicious.

Examples:

- x/y jump;
- rotation flip;
- scale spike;
- skew;
- anchor/pivot change;
- crop offset.

## Layer-order continuity

Objects should not cross depth layers without a visual cause.

Check hands, hair, props, UI overlays, particles and foreground scenery.

## Character continuity

Animation deformation can be intentional.

Do not ban:

- squash and stretch;
- smear frames;
- exaggerated anticipation;
- perspective deformation.

Instead ask whether the deformation belongs to the intended animation language and returns cleanly to the stable model.

## Loop integrity

Compare:

- final frame;
- first frame;
- timing across the boundary.

Look for:

- position jump;
- scale pop;
- color pop;
- alpha reset;
- particle discontinuity;
- character-model discontinuity.

## Temporary overlays

Transient guides, flashes, hit areas or instructional overlays should leave exactly when intended.

One leftover frame is still a visible defect.

## Export timing

Verify the actual exported sequence:

- frame count;
- order;
- frame duration;
- variable-delay frames;
- loop setting;
- playback speed.

Do not assume the editor timeline and exported playback are identical.
