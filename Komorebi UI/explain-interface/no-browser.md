# Reading a site without a browser

Fetch raw HTML and stylesheets when a scriptable browser is unavailable or unnecessary.

This route reads authored source. It does not tell you which declaration won at runtime.

## Fetch source, not a reader view

Use a raw HTTP fetch. Reader/markdown conversions often remove class names, style attributes, scripts and linked assets — exactly the evidence this skill needs.

Resolve relative stylesheet URLs against the document origin before fetching them.

## First decide whether the HTML contains the interface

Many client-rendered sites return a shell with little useful markup.

Check whether the visible page content, useful class names and style links are actually present before drawing conclusions.

If the interface is injected at runtime, say the fetch route is insufficient rather than treating the shell as the page.

## Utility classes can expose authored intent

When class names are intact, they may reveal responsive/state variants and unusual values directly.

That is useful evidence, but do not assume every utility-looking class proves a specific framework. Projects can generate or imitate similar names.

## Inline styles can carry one-off values

Inspect inline gradients, transforms, masks and CSS custom properties where present.

A value in markup is measured source evidence. Whether it wins in the cascade remains unknown without runtime resolution.

## Stylesheets reveal systems well

Useful targets include:

- `:root`, `html` and theme blocks for custom properties;
- `@font-face` for families, formats and weights;
- media/container queries for breakpoints and adaptation;
- keyframes for named animations;
- utility layers or component selectors;
- language selectors such as `:lang(ja)` or `:lang(zh-Hant)`;
- writing-mode and CJK-specific typography rules.

Cross-origin or protected stylesheets may be unreachable. Name the gap.

## Fingerprints are confidence, not facts

Asset paths and runtime markers can strongly suggest frameworks or libraries.

Examples:

- `/_next/static` strongly suggests Next.js output;
- `/_nuxt/` suggests Nuxt;
- `astro-island` suggests Astro;
- known data attributes can suggest component primitives.

Report:

> “The HTML contains `/_next/static` assets, a strong Next.js fingerprint.”

not:

> “This was definitely authored with Next.js and this exact setup.”

unless supporting source confirms it.

## Do not infer intent from defaults

If the stylesheet contains common framework breakpoints, spacing values or radius values, report the match.

Do not infer that:

- nobody chose them;
- the team forgot to customize them;
- they are good or bad;
- the design system is generic.

Those are review or intent claims, not source facts.

## What this route cannot tell you

Without runtime inspection, do not claim:

- which matching rule won;
- computed values after inheritance/cascade;
- runtime-injected styles;
- actual paint order;
- whether a declaration is visually occluded;
- current animation state;
- geometry after layout;
- which responsive branch the user actually saw.

A source-level answer can still be complete for a source-level question. Do not simulate certainty to compensate for missing browser evidence.
