# Palette generation

Producing values once the structure and roles are decided.

For which roles exist see [palette-structure.md](palette-structure.md).

## Start from the anchor, not necessarily “brand 500”

A product may begin with:

- a fixed brand color;
- a room / material reference;
- an illustration palette;
- an existing accent token;
- a set of approved light / dark surfaces.

Identify which value is contractually fixed and which values may move.

Do not silently darken or recolor a fixed brand value just to make it fit a preferred ramp position. If the brand swatch cannot serve as an accessible solid control, keep the brand value and choose a different role value for the control.

## Design lightness roles first

Before fine hue work, decide the perceptual hierarchy:

- page / environment;
- subtle surface;
- raised / sunken surfaces;
- borders;
- solid accent;
- muted text;
- primary text.

If adjacent steps have no distinct job or do not look distinct in their real use, one of them may not need to exist.

## Constant hue is a system option, not a law

A constant-hue ramp is clean, predictable and often ideal for semantic accent / status systems.

Material and neutral families may benefit from small intentional hue drift.

Examples:

- warm paper becoming slightly cooler in shadow;
- sage-gray losing green as it approaches ink;
- pale sky blue warming slightly toward a cream highlight.

Keep drift restrained. The family should still read as one family at a glance.

## Chroma trajectory

Large persistent areas usually need less chroma than small focal accents.

A common starting shape:

- low chroma at the light environmental end;
- more character around mid values;
- reduced chroma again toward dark ink / shadow.

But do not force every family into the same curve. A material family may intentionally stay muted throughout.

## Step density follows decisions

Light UI surfaces often need several subtle distinctions. Dark themes may need different spacing because dark surfaces collapse together easily.

Do not mechanically mirror numeric steps between appearances.

## Use perceptual tools, then look at the real composition

Use a color library or color-science tooling for:

- conversions;
- perceptual lightness;
- interpolation;
- gamut checks;
- contrast calculations.

Do not ask the library to make the aesthetic decision.

A mathematically even ramp can still feel sterile or wrong beside the actual paper, illustration or photography.

Workflow:

1. compute a coherent candidate;
2. place it in the real interface / artwork;
3. adjust intentional material or optical relationships;
4. remeasure required contrast and gamut;
5. document deliberate departures from the generated curve.

## Several semantic hues

When accent and status hues appear together, match **role weight**, not raw chroma numbers.

At the same semantic level, one hue should not look inexplicably twice as loud as another unless that difference is intentional.

Because different hues reach different maximum chroma, compare perceived result rather than copying a saturation value.

## Warm / cool neutrals

Choose neutral temperature deliberately.

- warm neutrals can feel paper-like, domestic or editorial;
- cool neutrals can feel misty, technical or quiet;
- green-gray can integrate foliage / natural environments;
- blue-gray can support ink / dusk atmospheres.

The choice should come from the world of the product, not from a generic “Japanese palette” recipe.

## Dark mode

Dark mode is not a reversed light ramp.

Re-evaluate:

- page temperature;
- separation between dark surfaces;
- accent chroma;
- text brightness;
- border visibility;
- image / illustration integration.

A subtle warm-light palette may need a less warm dark field to avoid looking muddy; a cool light palette may need a warmer accent at night. Preserve identity, not numeric symmetry.

## Pure extremes

Do not force ramps to reach pure black / white simply because the scale has endpoints.

Also do not ban pure extremes.

Use them when they serve:

- contrast;
- a deliberate graphic edge;
- photography / illustration;
- a material reference;
- platform convention.

For quiet UI fields, off-white and off-black are often more comfortable starting points.
