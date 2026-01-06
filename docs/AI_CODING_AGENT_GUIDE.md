# AI Coding Agent Guide: Tabler vs. Vanilla Bootstrap (Standalone)

This document embeds the key Tabler CSS/markup details (with concrete values) so AI coding agents can work without repository context. Focus is on structural and stylistic differences from vanilla Bootstrap; JavaScript component differences are intentionally omitted.

## Core CSS Differences (with concrete values)
- **Variable prefixing:** Tabler uses `$prefix: 'tblr-'` (while keeping `$variable-prefix: bs-` for legacy). Custom properties and generated utilities therefore emit `--tblr-*` names instead of `--bs-*`.
- **Feature flags enabled by default:** Tabler flips on several Bootstrap options: `$enable-cssgrid: true`, `$enable-navbar-vertical: true`, `$enable-smooth-scroll: true`, `$enable-negative-margins: true`, `$enable-important-utilities: true`, plus `$enable-social-colors`, `$enable-extra-colors`, `$enable-shadows`, `$enable-dark-mode`, `$enable-button-pointers`, `$enable-validation-icons`, and others shown below. Agents can assume these utilities/classes exist without extra configuration.
- **Expanded color system:** Neutral scale and brand palette are defined explicitly (all values are hex). Grays: `50 #f9fafb`, `100 #f3f4f6`, `200 #e5e7eb`, `300 #d1d5db`, `400 #9ca3af`, `500 #6b7280`, `600 #4b5563`, `700 #374151`, `800 #1f2937`, `900 #111827`, `950 #030712`. Core hues: `blue #066fd1`, `azure #4299e1`, `indigo #4263eb`, `purple #ae3ec9`, `pink #d6336c`, `red #d63939`, `orange #f76707`, `yellow #f59f00`, `lime #74b816`, `green #2fb344`, `teal #0ca678`, `cyan #17a2b8`, plus black/white. These feed `$colors` and utility generation, so use the names directly when choosing theme colors.

## Layout Markup Conventions (structural CSS inlined)
Tabler adds wrappers that supply sizing, spacing, and cover effects beyond vanilla Bootstrap:
- **`.page`:** `display: flex; flex-direction: column; position: relative; min-height: 100%;` to fill the viewport and stack children vertically.
- **`.page-wrapper`:** `flex: 1; display: flex; flex-direction: column;` with print margin reset, ensuring the main area consumes available height.
- **`.page-body`:** Vertical padding via `margin-top`/`margin-bottom: var(--tblr-page-padding-y);` plus `display: flex; flex-direction: column; flex: 1;` so content stretches within the wrapper.
- **`.page-body-card`:** Card-like container with `background: var(--tblr-bg-surface); border-top` using theme border tokens, `padding: var(--tblr-page-padding) 0; flex: 1;` and margin adjustments when stacked.
- **Cover helpers:** `.page-cover` sets `min-height` breakpoints (9/12/15rem) with background-cover styling; the later redefinition adds blur tokens (`--tblr-page-cover-blur: 20px`), padding, `position: relative; overflow: hidden;`. `.page-cover-img` positions a blurred, full-bleed backdrop behind content (absolute positioning with inset offsets and `filter: blur(var(--tblr-page-cover-blur));`).
- **Headers:** `.page-header` is a flex column wrapper (`min-height: 2.25rem;` etc.) that gains top margin inside `.page-wrapper`. `.page-title`/`.page-title-lg` set typography (font sizes/weights from theme variables) and align embedded icons; `.page-subtitle` uses `color: var(--tblr-secondary);`. `.page-header-border` adds a bottom border and background for separated headers.
- **Page tabs:** `.page-tabs` adds `margin-top: .5rem; position: relative;`, while `.page-header-tabs .nav-bordered` removes borders and zeroes the adjacent `.page-body-card` top margin for tight tab/content alignment.

## Grid and Spacing Utilities (behavior spelled out)
Tabler layers grid helpers on top of Bootstrap with explicit values:
- **Custom gutters:** `.row-0`, `.row-sm`, `.row-md`, `.row-lg` set horizontal padding/margins using gaps `0`, `0.375rem`, `1.5rem`, `3rem`, also pushing `.card` bottoms to `2 * gap`. This extends beyond Bootstrap’s single gutter scale.
- **Card-friendly rows:** `.row-deck` forces immediate children to `display: flex; align-items: stretch;` so nested `.card` elements grow to equal heights.
- **Card grid guttering:** `.row-cards` defines CSS vars `--tblr-gutter-x`/`--tblr-gutter-y` to `$cards-grid-gap` and ensures nested `.row-cards` flex, standardizing card spacing without manual margins.
- **Spacing helpers:** `.space-x*` and `.space-y*` map spacer scale to `gap` on a flex container (default `$spacer` when un-suffixed). `.divide-x*`/`.divide-y*` add translucent borders between siblings and symmetric padding equal to the chosen spacer value, with important flags to enforce the separation. `.divide-y-fill` stacks flex children and stretches them to equal height while centering their content.

## Navigation and Sidebar Patterns
Tabler’s markup patterns assume the layout wrappers above:
- **Top-nav pages:** Wrap content in `.page` and `.page-wrapper`, then use `.page-header` plus `.page-body`/`.page-body-card` to align card grids (`.row-deck`, `.row-cards`) with the layout rhythm; `.navbar` commonly pairs with `container-xl` and grid helpers for consistent spacing.
- **Vertical sidebar layouts:** Combine `<aside class="navbar navbar-vertical">` with `.page-wrapper` to position side navigation alongside the main content; header spacing relies on `.page-header` margins provided by the wrapper.

## Usage Tips for Agents
- Prefer Tabler utilities (`row-deck`, `row-cards`, `space-x*`, `divide-x*`, etc.) to keep gutters, separators, and card heights aligned with the theme defaults described above.
- Use the explicit color names/hexes listed in this guide when selecting utilities or SCSS variables; they are registered in `$colors` and drive generated classes.
- Keep the `.page`/`.page-wrapper`/`.page-body` scaffold for new pages to inherit built-in spacing, printing tweaks, and cover/header behaviors; only omit when intentionally deviating from Tabler norms.
