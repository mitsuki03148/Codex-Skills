# Surfaces

Radius, edge treatment, optical alignment, depth and image boundaries.

## A surface must have a job

Before styling a region as a surface, identify why it exists.

Useful jobs include:

- containing an interactive unit;
- establishing material identity;
- separating elevation layers;
- creating a drag object;
- protecting readable content from a changing background;
- expressing a state boundary.

If spacing and placement already explain the group, another rounded rectangle may only add visual furniture.

## Concentric border radius

For closely nested rounded layers with an even visible inset, concentric geometry is a useful construction:

`outer radius = inner radius + inset`

Example:

```css
.card {
  border-radius: 20px;
  padding: 8px;
}

.card-inner {
  border-radius: 12px;
}
```

Use the formula when the eye actually reads one surface nested inside another.

Do not force it onto:

- independent surfaces;
- asymmetric padding;
- organic or illustrated shapes;
- paper-like material;
- layers separated by generous space.

Optical balance wins when the geometry is not truly concentric.

## Radius is character, not decoration

Do not increase radius simply to make an interface friendlier.

A project's radius language can be:

- nearly square;
- softly rounded;
- mixed by role;
- irregular where the asset itself is handmade.

Keep the number of radius roles small enough to feel intentional.

## Optical alignment

When geometric centering looks wrong, align optically.

### Icons beside text

Start from the component's real icon set and font. Adjust only if the rendered pair looks unbalanced.

A fixed “icon side = text side - 2px” recipe is not universal. CJK labels, asymmetric icons and different icon grids can shift the optical centre differently.

### Play triangles and asymmetric symbols

Small physical nudges are legitimate when they correct visual weight.

Prefer fixing the SVG / viewBox if the correction belongs to the glyph itself. Use component-level translation only when the same icon genuinely needs a different relationship in that context.

## Borders, shadows and material

Borders and shadows do different jobs.

**Borders** can express:
- structure;
- containment;
- focus;
- selection;
- input boundaries;
- dense data separation.

**Shadows** can express:
- elevation;
- overlap;
- floating state;
- local depth.

Do not replace a legitimate border with a shadow merely because “shadows feel softer”.

Likewise, do not add a shadow when value contrast, material, spacing or overlap already establishes the depth.

## Quiet depth

For calm interfaces, depth often works best when it is shallow.

Prefer:
- low-opacity edge separation;
- small local value differences;
- short shadows with low spread;
- occasional overlap;
- material texture where appropriate.

Avoid stacking border + ring + multiple shadows + gradient unless each layer has a separate job.

## Dark mode depth

Dark surfaces often need different depth logic rather than a literal inversion of light mode.

Shadows may become less informative. Edge light, value separation or a subtle outline can do more.

Tune against the real background rather than applying one white-ring recipe everywhere.

## Image edges

Images do not universally need a `1px` outline.

Add an edge treatment when it solves a real boundary problem:
- pale image against pale surface;
- dark image against dark surface;
- an interactive thumbnail needs object identity;
- neighboring media need a consistent frame.

Possible treatments:
- no edge at all;
- subtle neutral outline;
- inset edge;
- quiet shadow;
- material frame;
- crop / spacing adjustment.

Use the lightest treatment that makes the boundary clear.

Do not tint an outline accidentally with the accent color, but a warm or cool neutral may be correct when the material system intentionally calls for it.

## Images with transparent or irregular silhouettes

A rectangular outline is wrong for transparent PNGs, cutout illustrations and irregular objects.

Let the object's own silhouette define the boundary, or use a shadow / mask that follows the alpha edge.

The visual object matters more than the file's bounding box.

## Surface review

Ask:
- Does this region need to be a surface at all?
- Is the radius part of one coherent language?
- Is the depth relationship legible without excessive shadow?
- Is the edge structural, material or decorative?
- Does a transparent object still look like an object rather than a rectangle?
- Would removing one visual layer make the interface calmer without losing meaning?
