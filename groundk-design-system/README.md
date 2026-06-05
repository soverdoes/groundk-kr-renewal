# GroundK Design System

Reverse‑engineered design system for **groundk.com** — built by analyzing the
full production CSS of every page (home + 22 sub‑page patterns).

## Contents

- **[design-system.md](design-system.md)** — the spec. Foundations (color,
  typography, spacing, layout, radius/elevation/motion) + full component
  specifications (22 components).
- **[tokens.json](tokens.json)** — design tokens in W3C DTCG format
  (Style Dictionary / Tokens Studio compatible), with semantic aliases & dark theme.
- **[tokens.css](tokens.css)** — drop‑in CSS custom properties (light + dark + mobile re‑scale).
- **[raw-css/](raw-css/)** — original source stylesheets pulled from the live site.

## Key facts (TL;DR)

| Aspect | Value |
|--------|-------|
| **Sizing model** | Fluid `vw`. Desktop ref **1920px** (`1vw=19.2px`), mobile ref **360px** (`1vw=3.6px`). Anchor: `0.833vw = 16px`. |
| **Breakpoint** | `@media (max-aspect-ratio: 10/9)` (portrait = mobile). No width‑based layout. |
| **Brand colors** | Primary navy `#2E3192`, secondary cyan `#2BD9FF` (interaction only). |
| **Theming** | 8 semantic tokens flip on `:root[data-theme="dark"]`. |
| **Fonts** | Pretendard Variable (body/KR), Termina (display/EN). Weights 400/500/700. |
| **Spacing** | 4px base unit, scale in `vw`. Section padding `6.25vw` (120px). |
| **Motion** | Single `0.3s ease-out`. GSAP ScrollTrigger + Lenis + Slick. |
| **Signatures** | `txt-stroke` (outline), `txt-mask` (scroll‑fill), `img-mask` (themable icons). |

## Using the tokens

**CSS** — link/import `tokens.css`, then reference variables:
```css
@import "tokens.css";
.cta { color: var(--color-primary); font-size: var(--fs-24); padding: 0 var(--space-24); }
```

**Style Dictionary / Tokens Studio** — import `tokens.json` (DTCG `$value`/`$type`,
references like `{color.base.navy}` resolve automatically). Generate platform
outputs (iOS/Android/CSS/SCSS) from there.

_Provenance: read from live groundk.com stylesheets on 2026‑06‑02._
