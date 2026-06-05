# GroundK Design System

> Reverse‑engineered from the **groundk.com** production site (all pages).
> GroundK is a luxury ground‑transportation / chauffeur & concierge brand — the
> system reads **premium, editorial, motion‑driven**: large display type, generous
> whitespace, a single confident brand color, and scroll‑reveal animation as a
> first‑class citizen.

| | |
|---|---|
| **Analyzed** | `variable.css`, `reset.css`, `common.css`, `main.css`, `sub.css`, `font.css` |
| **Pages covered** | Home + 22 sub‑page patterns (services, business, events, case‑studies list/view, destinations, about, fleet, sustainability, contact, policy, 404) |
| **Deliverables** | `design-system.md` (this file) · `tokens.json` (W3C DTCG) · `tokens.css` (CSS variables) · `raw-css/` (source) |
| **Tech stack** | Hand‑authored HTML/CSS · jQuery · GSAP + ScrollTrigger · Lenis smooth‑scroll · Slick carousel |

---

## 0. The one thing to understand first — the fluid `vw` model

GroundK does **not** use a fixed px grid or `rem`. **Every size — type, spacing,
radius, even shadows — is authored in `vw`** so the whole design scales linearly
with the viewport. There are two design references:

| Layout | Reference width | Conversion | Switch trigger |
|--------|----------------|-----------|----------------|
| **Desktop** | **1920 px** | `px = vw × 19.2` → `1vw = 19.2px` | default |
| **Mobile**  | **360 px**  | `px = vw × 3.6`  → `1vw = 3.6px`  | `@media (max-aspect-ratio: 10/9)` |

The root is `--font-size: 0.833vw` = **16px @1920**. Confirmed clean at both
references (e.g. section title `2.708vw` = 52px @1920; mobile body `3.889vw` =
14px @360).

> **Reading the tables below:** the `vw` column is the literal authored value;
> the **px** columns are what it resolves to at each reference. When you rebuild,
> keep the `vw` values — that *is* the responsive behavior.

**Layout breaks on aspect ratio, not width.** The only meaningful breakpoint is
`(max-aspect-ratio: 10/9)` ≈ portrait. Width queries (`1366`, `1024`, `640`) exist
but are nearly empty (only tweak nav pointer‑events). Treat **portrait = mobile**.

---

## 1. Color

### 1.1 Primitive palette

| Token | Value | Swatch use |
|-------|-------|-----------|
| `color.base.navy` | `#2E3192` | **Brand primary** — CTAs, links, active, map |
| `color.base.cyan` | `#2BD9FF` | **Brand secondary** — hover/active accent in nav |
| `color.base.black` | `#0F0F0F` | Text, dark backgrounds, footer |
| `color.base.white` | `#FFFFFF` | Background, inverted text |
| `color.base.gray-700` | `#5C5C5C` | Secondary / descriptive text |
| `color.base.gray-600` | `#636363` | Marquee “pass‑through” text |
| `color.base.gray-500` | `#B0B0B0` | Footer sub‑links, labels |
| `color.base.gray-400` | `#C4C4C4` | Borders, dividers |
| `color.base.gray-050` | `#F8F8F8` | Off‑white section background (pagination, content‑04) |

**Alpha overlays** (image scrims & effects): `rgba(0,0,0,.5 / .6 / .7)` for image
darkening, `rgba(0,0,0,.2)` shadows, `rgba(0,0,0,.35)` faded map dots,
`rgba(15,15,15,.1)` (light) / `rgba(255,255,255,.1)` (dark) for the `txt-mask`
under‑fill, `rgba(248,248,248,.9)` for the content‑04 wash.

> The palette is deliberately tiny: **two brand hues + a neutral ramp**. Navy
> carries 95% of the brand; cyan is a spark used only on interaction.

### 1.2 Semantic tokens & theming (light / dark)

The site is fully themable via `:root[data-theme="dark"]`. Only **8 semantic
tokens** flip; everything else is built on them, so theme switching is free.

| Semantic token | Light | Dark |
|----------------|-------|------|
| `--color-primary` | `#2E3192` navy | `#FFFFFF` white |
| `--color-primary-invert` | `#FFFFFF` | `#2E3192` navy |
| `--color-secondary` | `#2BD9FF` | `#2BD9FF` |
| `--color-text` | `#0F0F0F` | `#FFFFFF` |
| `--color-text-sub` | `#5C5C5C` | `#FFFFFF` |
| `--color-text-fill` | `rgba(15,15,15,.1)` | `rgba(255,255,255,.1)` |
| `--color-border` | `#C4C4C4` | `#C4C4C4` |
| `--color-background` | `#FFFFFF` | `#0F0F0F` |

**Rules of use**
- Body/section background & text transition on theme change: `background-color .3s ease-out, color .3s ease-out`.
- `primary` is the “ink” for interactive accents; `primary-invert` is what sits *on top* of a primary fill (e.g. button text on hover, active tab label).
- On image scrims and dark banners, text is hard‑coded `--color-white` (not `--color-text`) because it must stay light regardless of theme.

---

## 2. Typography

### 2.1 Families

| Family | Token | Role |
|--------|-------|------|
| **Pretendard Variable** | `--font-family` | Body, Korean + Latin, all paragraph & UI text. Loaded via jsDelivr (dynamic‑subset variable). |
| **Termina** | `--font-family-sub` | Display: English headlines, numerals (steps, “NEXT”), the GroundK wordmark, and all `txt-stroke` outline text. Loaded via Adobe Typekit (`use.typekit.net/csa5igw.css`). |

Weights in use: **400 Regular · 500 Medium · 700 Bold** (no others).
Default `line-height` is `normal`; headings tighten to `1.06–1.2`, body opens to `1.3`.

### 2.2 Type scale (semantic styles)

Sizes are `vw`; px resolved at each reference. Family **P** = Pretendard, **T** = Termina.

| Style | Family / Weight | Size (vw) | px @1920 | px @360 (mobile) | LH | Used by |
|-------|-----------------|-----------|---------|------------------|----|---------|
| **Display / Hero** | T 700 | `9.896vw` | **190** | 36 | 0.95 | Home hero `WEMOVEYOU` title |
| **Display / Stroke‑XL** | T 700 outline | `7.292vw` | **140** | 26 | 1 | Case‑studies stroke headline |
| **Display / Stroke** | T 700 outline | `5.208vw` | **100** | 36 (`10vw`) | 1.2 | `.txt-stroke` (welcome, contact, 404) |
| **Heading / Page** | T 700 | `2.5vw` | **48** | 24 (`6.667vw`) | 1.08 | `.sct-visual .title` (page hero) |
| **Heading / Section** | P 700 | `2.708vw` | **52** | 24 (`6.667vw`) | 1.06 | `.comm-title`, banner title, contact title |
| **Heading / Item** | P 700 | `2.188vw` | **42** | 20 (`5.556vw`) | 1.3 | Service & trusted card `.tit` |
| **Heading / Block** | P 500 | `1.667vw` | **32** | 20 (`5.556vw`) | 1.3 | Content `.tit`, character `.tit`, accordion, fleet, contact detail |
| **Eyebrow** | P 500 | `1.458vw` | **28** | 14 (`3.889vw`) | 1.3 | `.sub-title` (color = primary) |
| **Body / Lead** | P 400 | `1.458vw` | **28** | 16 (`4.444vw`) | 1.3 | Visual hero description |
| **Body / Default** | P 400 | `1.042vw` | **20** | 14 (`3.889vw`) | 1.3 | `.desc` everywhere (color = text‑sub) |
| **Body / Small** | P 400 | `0.938vw` | **18** | 14 (`3.889vw`) | 1.3 | Service/trusted `.desc`, copyright |
| **Label / Action** | P 500 | `1.25vw` | **24** | 14 (`3.889vw`) | — | Button, footer L1, tabs, cities, contact label |
| **Nav** | P 500 | `0.938vw` | **18** | 28 (`7.778vw`) | — | GNB top‑level links |
| **Nav‑sub / Caption** | P 500 | `0.833vw` | **16** | 16 (`4.444vw`) | — | Dropdown links, fleet capacity |

> **Pattern:** a *style* is the triple **(family, weight, size‑role)**. Color is
> applied separately from the theme tokens — headings use `--color-text`,
> descriptions use `--color-text-sub`, eyebrows use `--color-primary`.

### 2.3 Signature text treatments

These three reusable classes give the brand its identity — treat them as
**typographic components**:

| Class | Effect | Mechanics |
|-------|--------|-----------|
| `.txt-stroke` | Outlined (hollow) display text | `-webkit-text-stroke: 1px var(--color-text); color: transparent;` + Termina. Stroke color overridable (e.g. white on banners, primary @30% opacity behind section titles). |
| `.txt-mask` | Scroll‑reveal text “fills in” | Foreground `--color-text-fill` (10% ink) with a `background-image` gradient clipped to text (`background-clip: text`) animated `background-size: 0% → 100%` by GSAP on scroll. |
| `.img-mask` | Theme‑able icon / logo | SVG via `mask-image`; the shape is painted with `background-color` (a token), so every icon recolors with the theme automatically. This is how all icons, the logo, and the world map are rendered. |

### 2.4 Korean (국문) type rules — `/kr`, `<html lang="ko">`

The display family **Termina is Latin‑only** — it has no Hangul glyphs. Korean text placed in a Termina slot (hero, page title, stroke text, case‑study headline, fleet title, 404) would fall back to an arbitrary system font and, worse, **clip** under the ultra‑tight line‑heights (0.72–1.08) and negative tracking those slots were tuned for. The Korean build fixes this in two layers:

**1) Font fallback (automatic, per glyph).** `--font-family-sub` carries a Pretendard fallback:
`"termina", "Pretendard Variable", Pretendard, sans-serif`. So a mixed string like **"APEC 정상회의"** routes `APEC` to Termina and `정상회의` to Pretendard automatically — no manual splitting. A fully‑Korean title simply renders in Pretendard 700 at the slot's size/weight. (English build is unaffected — Termina covers Latin so the fallback never triggers.)

**2) Line‑height & tracking relax (`[lang="ko"]`).** Token line‑heights bump for ko (`--lh-hero` 0.95→1.1, `--lh-tight` 1.06→1.15, `--lh-snug` 1.08→1.2, `--lh-none` 1→1.15), and `overrides-ko.css` relaxes the specific clip‑prone slots, resets negative `letter-spacing` to `normal`, and adds `word-break: keep-all` so Korean words don't split mid‑syllable.

**Keep Termina (do NOT substitute)** for English/numeric ornaments — step numbers (`01, 02`), `NEXT`/`PREVIOUS`, the pass‑through marquee, and the GroundK wordmark (an SVG mask, not text).

| Display slot | EN line‑height | KO line‑height | Note |
|--------------|----------------|----------------|------|
| Hero `.sct-design .title` | 0.95 | 1.1 | `keep-all`, tracking → normal |
| Stroke `.txt-stroke` | 1.0 | 1.15 | tracking → normal |
| Page hero `.sct-visual .title` | 1.08 | 1.2 | `keep-all` |
| Case‑study headline / title | 1.0 / 1.2 | 1.15 / 1.3 | — |
| Fleet title `.atc-type .tit` | 1.0 (`-0.052vw`) | 1.15 (normal) | tracking reset |
| 404 title | 0.72 | 1.05 | hardest clip |

> **Build:** load `overrides-ko.css` **after** `style.css` on `/kr` pages, and set `<html lang="ko">`. Files: `tokens.css` (fallback + ko line‑height tokens), `overrides-ko.css` (slot fixes).

---

## 3. Spacing

A **4px base unit**, expressed in `vw`. Values cluster on multiples of 4/8.

| Token | vw | px @1920 | Typical use |
|-------|----|---------|-------------|
| `space-4` | `0.208vw` | 4 | icon↔label, fine gaps |
| `space-8` | `0.417vw` | 8 | inline gaps, small radius |
| `space-10` | `0.521vw` | 10 | button icon gap, dots |
| `space-12` | `0.625vw` | 12 | card row gaps |
| `space-16` | `0.833vw` | 16 | tit↔desc |
| `space-20` | `1.042vw` | 20 | list gaps |
| `space-24` | `1.25vw` | 24 | — |
| `space-28` | `1.458vw` | 28 | nav‑sub padding |
| `space-32` | `1.667vw` | 32 | character row gap |
| `space-36` | `1.875vw` | 36 | banner inner gap |
| `space-40` | `2.083vw` | 40 | card column gap, footer rows |
| `space-44` | `2.292vw` | 44 | service text row gap |
| `space-48` | `2.5vw` | 48 | — |
| `space-52` | `2.708vw` | 52 | — |
| `space-56` | `2.917vw` | 56 | **title → content** (`.comm-title margin-bottom`) |
| `space-60` | `3.125vw` | 60 | header bar height |
| `space-64` | `3.333vw` | 64 | nav column gap |
| `space-80` | `4.167vw` | 80 | **container side padding** |
| `space-100` | `5.208vw` | 100 | large vertical |
| `space-120` | `6.25vw` | 120 | **standard section padding (top/bottom)** |

**Rhythm conventions**
- **Section vertical padding:** `6.25vw` (120px) is the default; content‑heavy sections use `8.333vw` (160px); mobile jumps to `16.667vw` (60px @360).
- **Title → body:** `2.917vw` (56px).
- **`.tit` → `.desc`:** `0.833vw` (16px).
- **Inter‑column gap:** `6.25vw` (120px) for 2‑up text/image; `2.083vw` (40px) for card grids.

---

## 4. Layout & grid

### 4.1 Container

```css
.inner { width: 100%; box-sizing: border-box; padding: 0 4.167vw; } /* 80px @1920 */
@media (max-aspect-ratio: 10/9) { .inner { padding: 0 4.444vw; } }   /* 16px  @360 */
```
There is **no max‑width** — the design is full‑bleed and scales with the viewport.
All content is gutter‑bounded by `.inner`’s side padding only.

### 4.2 Structural pattern

Every page is a stack of **sections** following one consistent nesting:

```
section.sct-{name}
└─ .atc-{content|text|image|map|tab|type}   ← the “article” block, owns vertical padding
   └─ .inner                                ← gutter container
      └─ .comm-title / .descript / .list…   ← content
```

- `sct-` = **section** (full‑width band, vertical rhythm).
- `atc-` = **article** (content group inside a section; carries the padding).
- `.inner` = **gutter** (horizontal padding).
- Lists are `flex: 1 1 0` equal columns, or CSS Grid `repeat(2|3|4, 1fr)`.

### 4.3 Columns / grids seen across pages

| Layout | Where |
|--------|-------|
| 2‑up text ↔ image, alternating (`row-reverse` on even) | `sct-content` 01/02/05, `sct-trusted` |
| 3‑up equal cards | `sct-character` (icon cards), `descript-bg`, step `col-3` |
| 4‑up | step `col-4`, fleet tabs (`flex 1 1 20%`) |
| 2‑col grid, every 3rd item full‑width | `case-studies` gallery (editorial masonry) |
| 2‑col country grid | `cities-worldwide` |
| Sticky‑stacking cards | `sct-services` (cards pin & overlap on scroll via `position: sticky` + per‑child `translateY`) |

---

## 5. Radius, borders, elevation, motion

### 5.1 Radius
| Token | vw | px | Use |
|-------|----|----|-----|
| `radius-none` | `0` | 0 | **buttons, tabs (default — sharp)** |
| `radius-sm` | `0.417vw` | 8 | header glass pills |
| `radius-md` | `1.042vw` | 20 | cards, screen slides (mobile → `2.222vw`/8px) |
| `radius-full` | `100%` | — | avatars, slider dots, map dots |

### 5.2 Borders
- **Hairline `1px`** — the workhorse: button outlines, dividers, table grid, card rules, accordion separators.
- **Thick `0.156vw` (3px)** — framed screenshots (`screen-slide`), nav underline.
- Divider color = `--color-text` (full strength) or `--color-border` (`#C4C4C4`) for softer rules.

### 5.3 Elevation (shadows)
| Token | Value (≈ px @1920) | Use |
|-------|--------------------|-----|
| `shadow-card` | `-0.104vw 0.313vw 1.302vw rgba(0,0,0,.16)` ≈ `-2 6 25` | review cards |
| `shadow-screen` | `-0.417vw 0.26vw 1.042vw rgba(0,0,0,.16)` ≈ `-8 5 20` | device/screen slides |
| `shadow-drop` | `0 0.26vw 1.042vw rgba(0,0,0,.16)` ≈ `0 5 20` | featured images (`drop-shadow`) |

Shadows are **subtle and directional** (slight left offset), at 16% black — premium, not heavy.
**Glass:** `backdrop-filter: blur(15px)` over `rgba(0,0,0,.7)` on the header & nav dropdowns.

### 5.4 Motion
- **Single duration/easing:** `0.3s ease-out` for *all* hover, state, and theme transitions. Keep it.
- **Scroll engine:** Lenis (smooth scroll) + GSAP ScrollTrigger drive the reveals — `txt-mask` fills, map line‑draws, sticky service cards, the section title fades.
- **Reveal grammar:** content animates *in* once on scroll (lines draw, dots scale `0→1`, text fills `0%→100%`), staggered with small delays (`.3s / .6s / .9s / 1.2s` on the map).

---

## 6. Components (full spec)

Notation: sizes given as **px @1920 (`vw`)**; mobile value in parentheses where it diverges.

### 6.1 Button — `.comm-button`
Primary action. Outlined, square, with a **slide‑fill hover**.

- **Rest:** text `--color-primary`, `1px` primary border, height **45px (`2.813vw`)**, padding `0 24px (1.25vw)`, font **24px (`1.25vw`)**, `radius 0`. Trailing arrow icon **30px (`1.563vw`)** via `img-mask`, gap `10px (.521vw)`.
- **Hover:** a `::before` panel wipes `width: 0 → 100%` in primary color; text & icon flip to `--color-primary-invert`. (`.3s ease-out`.)
- **On‑dark variant** (banners): border/text/icon = white, hover fills white and text → navy.
- **Mobile:** font **14px (`3.889vw`)**, height **32px (`8.889vw`)**, padding `0 16px (4.444vw)`.
- **`.btn-more`** variant swaps the arrow for a “more” glyph (case‑studies).

### 6.2 Header / Global Nav — `header > .header-wrap`
Fixed, centered, **glassmorphic**.

- **GNB bar:** centered pill, height **60px (`3.125vw`)**, `radius 8px`, background `rgba(0,0,0,.7)` + `blur(15px)`. Logo **76px (`3.958vw`)** wide. Nav links **18px (`.938vw`)** medium white, `column-gap 60px (3.125vw)`; animated underline (`::before`, `2px`, slides up on hover).
- **Dropdown `.nav-sub`:** absolute glass panel, padding `28px 20px`, links **16px (`.833vw`)** white → `--color-secondary` (cyan) on hover with a sliding circle‑arrow `::after`. Fades + lifts in (`opacity 0→1`, `translateY`).
- **Hide on scroll‑down:** bar translates up `-5.208vw` (`header.hide`).
- **Mobile:** logo pinned top‑left; hamburger top‑right; tapping opens a **full‑screen panel** (`translateX(100%) → 0`) with nav links at **28px (`7.778vw`)** and an accordion for sub‑items; includes a login button row.

### 6.3 Footer — `.footer-wrap`
Dark band (`--color-black`, white text), pulled up under the page (`translateY(-10.417vw)`), padding `120px 0 40px`.

- **`fnb`:** GroundK logo (`img-mask` **273px (`14.219vw`)**), then a `space-between` nav row — column headers **24px (`1.25vw`) bold**, sub‑links **20px (`1.042vw`)** in `--color-gray` (active item highlighted white via `<b>`).
- **`etc`:** top hairline (white), copyright **18px (`.938vw`)**, legal links (Terms / Privacy) right‑aligned.
- **Mobile:** stacks vertically, nav headers drop to medium **18px (`5vw`)**.

### 6.4 Section title — `.comm-title` (+ eyebrow + stroke)
- **`.comm-title`:** **52px (`2.708vw`) / 700 / LH 1.06**, color `--color-text`; often `text-align: center`; `margin-bottom 56px (2.917vw)`.
- **`.sub-title` (eyebrow):** **28px (`1.458vw`) / 500**, `--color-primary`, sits above the title (`margin-bottom 8px`).
- **Decorative stroke:** a `.txt-stroke` set **80px (`4.167vw`)** in primary @ **30% opacity**, absolutely positioned *behind* the title (uppercase) — the signature “ghost word” backdrop.

### 6.5 Page hero — `.sct-visual`
Full‑width image banner, height **62.5vh**.
- Background image + `rgba(0,0,0,.6)` scrim.
- Centered white text: title **48px (`2.5vw`)** Termina 700 (LH 1.08), description **28px (`1.458vw`)** constrained to `53.333vw`, `text-wrap: balance`. Top padding `23.75vh`.
- Some pages add a bottom `linear-gradient(transparent → #0F0F0F)` to blend into content (case‑studies, contact).

### 6.6 Icon feature cards — `.sct-character`
3‑up equal columns. Each: centered icon **72px (`3.75vw`)** (`img-mask`, primary), title **32px (`1.667vw`)**, description **20px (`1.042vw`)** text‑sub, `text-wrap: balance`. Per‑page icon sets are swapped by `#wrap.{page} .img-01/02/03`. Mobile → single column, icon **48px (`13.333vw`)**.

### 6.7 Promo banner — `.sct-banner` (variants 01/02/03)
Full‑width image (`rgba(0,0,0,.5)` scrim), height **360px (`18.75vw`)**, centered content. Title **52px (`2.708vw`)** white, description **20px**, white `comm-button`, and a giant `.txt-stroke` watermark **84px (`4.375vw`)** bottom‑right. Variants change alignment: `01` centered Termina title, `02` left detail, `03` centered with CTA. Mobile → tall portrait (`133vw`), watermark hidden.

### 6.8 Content block — `.sct-content` (content‑01 … 05)
The core editorial workhorse: alternating **image ↔ text** rows.
- Section padding `120px (6.25vw)`; `.descript > ul` is a `space-between` flex with `column-gap 120px (6.25vw)`.
- Block title `.tit` **32px (`1.667vw`)/500**, body `.desc` **20px** text‑sub.
- Variants set image aspect ratios & order: `01` reversed row + stacked image, `02` side‑by‑side, `04` centered with drop‑shadow hero image on a washed bg, `05` full‑width alternating rows (image `59.9vw × 26vw`).
- Optional sub‑grids: `.character` (mini 3‑up icon row), `.descript-bg` (image‑background cards with white text), `.stroke` (centered `txt-stroke` **100px**).

### 6.9 Image‑background cards — `.descript-bg li`
Aspect `43/32`, full‑bleed image + `rgba(0,0,0,.5)`, bottom‑aligned white text: title **32px** bold, desc **20px**. 3‑up, `column-gap 40px (2.083vw)`.

### 6.10 Testimonial slider — `.sct-review` (Slick)
Centered carousel of quote cards. Card: white bg, `shadow-card`, padding **120px (`6.25vw`)**, quote `.tit` **28px (`1.458vw`)** text‑sub, `.desc` **20px**. A circular **170px (`8.854vw`)** avatar overlaps the top; a primary‑color bar runs behind the row; quotation‑mark glyphs at the corners. Custom **dots** = `20px` circles, outlined, filled when active. Mobile hides dots, enlarges padding.

### 6.11 Interactive world map — `.sct-worldwide`
Signature home section. An SVG world (`img-mask`, text‑sub) with absolutely‑positioned **city labels** (Termina **48px (`2.5vw`)** primary, scroll‑filled like `txt-mask`), animated **connector lines** (`width`/`height` grow from 0), and **dots** (`scale 0→1`). “Expect” (future) cities render as faded dots (`opacity .35`). Staggered reveal delays `.3s→1.2s`. Mobile widens the map to `158vw` and overflows horizontally.

### 6.12 Destination list — `.cities-worldwide .world`
2‑col grid (`column-gap 15.625vw`, `row-gap 3.75vw`). Each country: flag **48px (`2.5vw`, 3:2)** + name **32px (`1.667vw`)/500**, then a wrapping list of city links **24px (`1.25vw`)** at `50%` basis. Faint world map sits behind. Mobile → single column.

### 6.13 Tabs — `.atc-tab` (fleet filter)
Top hairline, then a bordered row of equal tab buttons (`flex 1 1 20%`, height **80px (`4.167vw`)**, **24px (`1.25vw`)/500**). Active = `--color-primary` fill, `--color-primary-invert` text. Below: centered helper `.desc` **20px**. Tab panels (`.sct-fleet`) toggle `display` via `.active`. Mobile → 3‑per‑row, height `13.889vw`.

### 6.14 Fleet vehicle row — `.sct-fleet .atc-type`
Per‑class header image (height **370px (`19.271vw`)**) with title overlay (Termina **48px (`2.5vw`)**, `letter-spacing -0.052vw`). Each vehicle: text column (title **32px**, bulleted `.desc` with `•` via `::before`, capacity `.max` = man/bag icons **20px (`1.042vw`)** + count **18px**) beside a contain‑fit car image **612px (`31.875vw`, 306:133)**. Mobile stacks; capacity row pins to the bottom center.

### 6.15 Gallery grid — `.case-studies .sct-gallery`
Editorial masonry: 2‑col grid where **every 3rd item spans both columns**; heights alternate `31.25vw / 46.875vw / 31.25vw`. Hover → `rgba(0,0,0,.7)` veil + centered **“See More”** (`32px`). Caption: Termina title **32px (`1.667vw`)/700** + date **32px**. A `btn-more` button (custom arrow) loads more. Above the grid: title **67px (`3.49vw`)** + right‑aligned stroke headline **140px (`7.292vw`)**. Mobile → single column.

### 6.16 Numbered steps — `.sct-step`
Auto‑numbered via CSS counter `counter(step, decimal-leading-zero)` → “01, 02…” in Termina **32px (`1.667vw`)/700**, with `.desc` **20px/500** below. Layouts: flex‑wrap, or grid `col-3` / `col-4`. Mobile → single column.

### 6.17 Pagination cards — `.sct-pagination`
Prev/Next as two large image cards (**590×500px**, `30.729vw × 26.042vw`) on `#F8F8F8`, `rgba(0,0,0,.7)` veil, centered white title **28px (`1.458vw`)/500**, with a corner **“NEXT/PREVIOUS”** (Termina **32px/700**) + arrow. First card flips to “PREVIOUS”.

### 6.18 References slider — `.sct-references` (Slick + arrows)
Carousel of image tiles (height **500px (`26.042vw`)**) with `rgba(0,0,0,.7)` veil, centered white title **28px (`1.458vw`)/500** + bottom “See More”. Square outline **prev/next arrows** (**56px (`2.917vw`)**, `img-mask` icon, dim when disabled), edge fade masks on both sides.

### 6.19 Accordion — `.sct-accordion`
FAQ / legal. Each row: top hairline (`--color-border`), `acc-title` (**32px (`1.667vw`)/500**, padding `40px 16px`) with a **plus icon** (`2.188vw`, `img-mask`) that **rotates 45° → ×** when `.active`; `acc-sub` body **20px** text‑sub, `display: none` until open. Mobile enlarges to **18px (`5vw`)** titles.

### 6.20 Contact block — `.sct-contact`
Title **52px (`2.708vw`)/700** + right stroke headline **100px (`5.208vw`)**, over a dark `--color-black` panel with a contact image. Info list: `label` **24px (`1.25vw`)** gray, `detail.title` **32px (`1.667vw`)/700**, `detail.desc` **24px (`1.25vw`)** text‑sub. Mobile → stacked, column‑reverse.

### 6.21 404 — `.sct-404`
Full‑height centered: logo (`img-mask` **157px (`8.177vw`)**), big Termina title **72px (`3.75vw`)/700** (LH 0.72), sub `.tit` **28px (`1.458vw`)/700**, `.desc` **20px/500**, and a square outline link button. A `.txt-stroke` watermark **100px (`5.208vw`)** sits bottom‑right.

### 6.22 Forms (base) — `reset.css`
Inputs/selects/textareas inherit Pretendard at `--font-size` (16px), `box-sizing: border-box`, focus outlines reset. No heavy form components exist beyond contact display — build inputs as **hairline‑bordered, square (`radius 0`), 16px** to match buttons.

---

## 7. Usage cheatsheet

**Do**
- Author every size in `vw` against 1920 (desktop) / 360 (mobile); keep `0.833vw = 16px` as the anchor.
- Drive *all* color from the 8 semantic tokens so light/dark “just works”.
- Use `0.3s ease-out` for every transition. One duration, one curve.
- Reach for the three signature treatments (`txt-stroke`, `txt-mask`, `img-mask`) — they *are* the brand.
- Keep buttons & tabs square (`radius 0`); reserve rounding for cards (`20px`) and pills (`8px`).

**Don’t**
- Don’t introduce new hues — extend the neutral ramp instead. Cyan stays interaction‑only.
- Don’t add `max-width`; the system is full‑bleed and fluid.
- Don’t branch layout on `min-width`; branch on `(max-aspect-ratio: 10/9)` (portrait).
- Don’t bake brand color into icons — paint `img-mask` shapes with a token so they recolor.

---

## 8. Files

| File | What |
|------|------|
| `design-system.md` | This document — foundations + component specs. |
| `tokens.json` | W3C DTCG tokens (color/theme/type/space/radius/shadow/motion/breakpoints) with aliases. |
| `tokens.css` | Ready‑to‑use CSS custom properties incl. dark theme + mobile re‑scale + ko line‑height tokens. |
| `overrides-ko.css` | Korean (`/kr`) display‑slot fixes — load after `style.css`. See §2.4. |
| `i18n-url-hreflang-spec.md` | EN(root)/KO(`/kr`) URL map, hreflang pairing, language‑switch fallback, per‑page build plan. |
| `raw-css/` | Original production CSS pulled from groundk.com (source of truth). |

> **Provenance:** every value here was read from the live `groundk.com`
> stylesheets on 2026‑06‑02. Where the site authored a value in `vw`, the `vw`
> is preserved as the source of truth and px equivalents are derived at the two
> design references (1920 / 360).
