# Color usage

Deploying color once the system exists: meaning, emphasis, atmosphere, gradients and appearance variants.

For values see [palette-generation.md](palette-generation.md), for naming [token-naming.md](token-naming.md), for required contrast [contrast.md](contrast.md).

## Separate semantic color from world color

Semantic UI color communicates jobs: interaction, state, text hierarchy, borders, focus and feedback.

World color belongs to illustration, environment, material and atmosphere.

The same hue can appear in both worlds, but the **treatment** should keep the semantic signal clear.

Example: a sage accent button can coexist with sage leaves in a background. The leaves do not become “clickable” simply because the hue matches, provided their shape, position and interaction treatment clearly belong to the scene.

## Use tokens in their role

Do not borrow a semantic token because its current value looks convenient.

A separator token used for text may look fine today and become unreadable the moment borders are tuned lighter.

If a real semantic role is missing, add or refine the role rather than borrowing by value.

## Primary emphasis should reflect real hierarchy

When one action is truly primary, filled accent can communicate that.

When several choices are peers, let them remain peers. Do not recolor one merely to satisfy a “single primary” recipe.

Selected / active state is not the same thing as primary emphasis.

## Ambient color can stay quiet

Persistent environment colors should usually tolerate being ignored.

A room, paper background or illustration can have warmth, coolness or slow variation without becoming a notification surface.

Avoid repeated high-chroma pulses, color cycling or decorative accent flashes in always-on spaces unless attention is the intended effect.

## Color density matters

A small saturated mark can be calmer than a large muted block.

Judge:

- area;
- repetition;
- contrast against surroundings;
- persistence;
- motion;
- semantic role.

Do not decide “this color is too strong” from swatch chroma alone.

## Gradients

Interpolation space is a look, not a correctness setting.

- **sRGB** may darken / mute the midpoint;
- **Oklab** often gives smoother lightness transitions;
- **OKLCH** follows hue around a polar space and can stay more vivid, sometimes producing intermediate hues that were not intended.

Choose by the visual result the composition needs.

For quiet interfaces, prefer a gradient that behaves like light or material rather than one that announces itself as a gradient.

Useful restrained cases:

- paper warming toward one edge;
- daylight cooling toward shadow;
- a shallow surface depth cue;
- a temporary state glow that fades away.

### Text on gradients

Measure the worst relevant region behind the text.

If the background varies too much, first try composition: move text into a naturally quiet region. Add a scrim or surface only when needed.

## Cultural / locale meaning

Color meaning varies by region, domain and existing product convention.

Finance is the classic example: gain / loss conventions differ across markets.

Do not map colors from language alone. `zh-Hant` does not by itself tell you the financial market, and `ja` does not define every Japanese product convention.

For critical semantics:

- verify the target locale / market;
- keep text / icon support;
- localize semantic tokens when the domain convention genuinely differs.

## Japanese-influenced restraint without costume

Do not reach for a fixed “Japanese palette”.

Sakura pink, indigo, gold, vermilion, washi beige and matcha green can all be beautiful — and all can become cliché when used as identity shortcuts.

A more reliable direction is:

- low-chroma field colors;
- natural temperature shifts;
- off-white / ink rather than automatic pure extremes;
- one or two deliberate accents;
- enough quiet area for color to matter;
- material consistency across paper, wood, foliage, fabric and light.

Use saturated traditional colors when the subject genuinely calls for them, not because the interface needs proof of “Japan”.

## Light, dark and increased contrast

Every appearance should preserve role, not necessarily the same numeric distance from black / white.

Design dark mode rather than mirroring it.

A user-requested increased-contrast appearance should make required distinctions more visible. Follow `komorebi-accessibility` and [contrast.md](contrast.md) for the actual gate.

Do not invent one universal lightness delta as proof of increased contrast. Measure the required pairs.
