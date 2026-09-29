# Token naming

Naming makes a palette usable by people who did not build it.

For palette composition see [palette-structure.md](palette-structure.md).

## Two core tiers

### Primitives

Primitives name a value or family step:

```css
--sage-500: #6f897d;
--paper-100: #f5efe4;
--ink-900: #2e2b27;
```

They describe what a color *is* in the system.

### Semantics

Semantic tokens name a job:

```css
--color-bg-page: var(--paper-100);
--color-text-primary: var(--ink-900);
--color-accent-solid: var(--sage-500);
```

Components should normally reference the semantic tier.

A component-level tier is appropriate only when a component genuinely owns a local visual decision that should not become a global semantic role.

## Do not force every world color into semantic UI tokens

Illustration, character palettes and environment art can use their own asset / scene naming system.

For example:

```css
--room-wall-morning
--clara-cardigan-sage
--leaf-shadow-cool
```

Those names are legitimate when they belong to authored visual assets or scene composition rather than reusable UI semantics.

The important boundary is: **components should not borrow world / illustration colors to fake semantic UI roles.**

## Role inventory

A system is complete when the product's real roles have names, not when a generic checklist is fully populated.

Common groups:

| Group | Examples |
| --- | --- |
| Surfaces | `bg-page`, `bg-surface`, `bg-raised`, `bg-sunken`, `scrim` |
| Text | `text-primary`, `text-secondary`, `text-disabled`, `text-inverse`, `text-on-accent` |
| Borders | `border-subtle`, `border-default`, `border-strong`, `focus-ring`, `separator` |
| Accent | `accent-subtle`, `accent-border`, `accent-solid`, `accent-solid-hover`, `accent-text` |
| Status | `danger-*`, `warning-*`, `success-*`, `info-*` only where shipped |

Do not create unused status families or every possible state in advance.

## Naming grammar

Use one grammar consistently, such as:

`--color-{role}-{variant}-{state}`

```css
--color-bg-surface
--color-text-secondary
--color-border-strong
--color-accent-solid-hover
```

Consistency matters more than the exact vocabulary.

## Material names are allowed when material is the role

A semantic token should not be named for accidental appearance.

But if the product intentionally models a material layer, a material-oriented role can be honest:

```css
--color-paper-surface
--color-paper-edge
--color-room-shadow
```

Use this only when “paper” or “room” is a stable product concept, not just how one mockup happens to look.

## Avoid ambiguous `primary`

Do not let `primary` mean both “brand color” and “main body text”.

Use `accent` or another explicit brand-role term for the brand family. Reserve `primary` for prominence within a clear group, such as `text-primary`.

## Anti-patterns

| Name / usage | Problem | Better direction |
| --- | --- | --- |
| `--color-blue-button` | Appearance and component mixed together | `--color-accent-solid` |
| `--color-sidebar-gray` | First location becomes the name | Name the surface role |
| `--color-light-gray` | Lies in dark mode | Primitive step or material name |
| `--color-text-2` | Number has no semantic meaning | `--color-text-secondary` |
| Raw primitive used in component UI | Skips the theming seam | Reference semantic role |
| Illustration swatch used for focus ring | World color impersonates UI semantics | Use a real focus token |
| Twenty component tokens for the same missing role | Component tier compensates for a weak semantic tier | Add / refine the global role |

## Tailwind projects

Tailwind can expose both primitive and semantic color names. The fact that a primitive utility exists does not mean templates should use it directly.

Keep the same ownership boundary:

- primitive utilities are implementation detail / exceptional use;
- semantic utilities are the normal component API.

Opacity modifiers create composited colors. Anything important for text or state must be checked against its actual rendered background.
