# Spatial and physical plausibility

A rendered object can be beautifully drawn and still fail because it does not physically belong in the scene.

This check owns **visible spatial and physical plausibility**, not simulation-grade physics. It judges object-to-scene relationships, not interface composition, hierarchy or usability. For interface layout, route to `komorebi-layout`; for control styling and interaction, route to `komorebi-ui`.

The question is:

**Does the object appear to face, sit, touch, overlap, scale and move in a way that makes sense inside the intended visual world?**

Stylization may bend physics. Accidental impossibility is the defect.

## When this check applies

Use it for:

- rooms and environments;
- furniture and props;
- layered scenes;
- characters holding / touching / sitting on objects;
- composited objects;
- product / object renders;
- animation where orientation, contact, gravity or depth changes.

Mark it `N/A` for assets where no meaningful spatial or physical relationship exists.

## Orientation

Check whether the object faces the intended direction.

Look for front / back reversal, accidental mirroring, inverted top / bottom, screen or label facing the wrong way, or a handle / hinge / opening / functional side oriented implausibly.

Mirroring can be intentional. Report it only when it contradicts the scene, reference or object function.

## Contact and support

Objects should visibly connect to the surfaces or bodies supporting them.

Check that feet and furniture meet the floor, props rest on surfaces, seated characters meet the seat, hands visibly grip rather than merely overlap props, wall-mounted objects meet the wall, and stacked objects have believable support.

A tiny stylized gap can be acceptable. A visible unexplained float is a defect.

## Gravity and weight

Ask whether the scene suggests a coherent direction of gravity and weight.

Look for unsupported centres of mass, hanging objects behaving against gravity without cause, loose fabric or hair contradicting the scene, or shadows implying a different ground plane.

Do not demand realistic deformation from a stylized illustration.

## Depth and occlusion

Check whether front / back relationships remain coherent.

Look for limbs passing through furniture, props intersecting bodies, objects cutting through walls or floors, background leaking through foreground assets, impossible overlap order, or depth order changing without a spatial cause.

This overlaps with compositing hygiene, but this check asks whether the **scene relationship** is plausible, not merely whether the layer stack is technically clean.

## Perspective and ground plane

Related objects should appear to inhabit compatible space.

Check horizon / vanishing direction, floor plane, furniture footprint, object orientation relative to walls, camera angle and scale with depth.

Do not require mathematically perfect perspective in deliberately flattened, isometric, chibi, storybook or other stylized worlds. Ask whether the chosen spatial language is internally coherent.

## Relative scale

Check object sizes against characters, doors, chairs, tables, beds, handheld props and repeated copies of the same object.

Use known project dimensions or approved references when available.

Do not invent real-world measurements when the visual world intentionally exaggerates scale.

## Functional plausibility

Where an object has an obvious use, check that its visible construction supports that use.

Examples include chair facing, door hinge / opening direction, drawer access, phone screen orientation, book spine, cup handle, lamp connections, wheels, legs and handles.

This is not industrial-design certification. Report visible contradictions that make the rendered object or interaction read incorrectly.

## Light and contact cues

Lighting does not need simulation accuracy, but it should not accidentally break spatial reading.

Check that contact shadows support contact, cast shadows do not obviously contradict the scene, grounding cues do not disappear, and a composited object does not carry such incompatible lighting that it stops belonging to the scene.

Art-directed or surreal lighting is allowed when intentional.

## Character × prop

When a character uses an object, inspect the relationship as one unit.

Check hand position, grip relationship at the level the art style supports, arm path, body balance, sitting / leaning contact, task-relevant facing direction, prop orientation and occlusion.

Do not over-police anatomy in simplified art. Look for visible interaction failure.

## Animation continuity

Across frames, spatial truth should not randomly change.

Watch for object orientation flips, props changing hand, contact points sliding without motion, stable furniture shifting, scale changing without depth movement, shadows detaching, depth order flipping or held objects teleporting relative to the hand.

Intentional motion, squash/stretch and perspective change remain valid.

## Diagnostic methods

Useful checks include silhouette view, contact-point zoom, ground-plane or perspective guides, neighboring-frame overlays, side-by-side reference comparison and simple scale ratios.

Guides are diagnostic only. Remove them from delivery.

## Before delivery

For applicable assets, ask:

1. Is every important object facing the intended direction?
2. Is it visibly supported?
3. Are contact points believable?
4. Do depth / occlusion relationships make sense?
5. Do perspective and scale belong to the same visual world?
6. Does the object visibly function the way the scene implies?
7. Do light / shadow cues accidentally make anything float?
8. For animation, does this remain true through time?

Report only meaningful visible failures.

**Stylization may bend physics; accidental impossibility is the defect.**
