# Design System — Kushagra's GitHub Profile

A single source of truth for the tokens reused across every asset in this
project. Because each SVG is a standalone document (GitHub renders them as
independent `<img>` sources), tokens can't be shared via a real CSS file —
so this document is the contract. If you change a value here, apply it
everywhere the token is used.

## Color

| Token | Value | Usage |
|---|---|---|
| `--black` | `#0A0A0A` | Dark canvas / primary background |
| `--graphite` | `#171717` | Dark surfaces, cards, terminal body |
| `--charcoal` | `#262626` | Dark elevated surfaces, hover states |
| `--off-white` | `#F5F5F5` | Light canvas / primary text on dark |
| `--gray` | `#A3A3A3` | Secondary text on dark |
| `--gray-light` | `#525252` | Secondary text on light |
| `--surface-light` | `#FFFFFF` | Light surfaces, cards |
| `--border-dark` | `rgba(255,255,255,0.08)` | Hairline borders on dark |
| `--border-light` | `rgba(10,10,10,0.08)` | Hairline borders on light |
| `--accent` | `#3B82F6` | Electric blue — links, cursor, active states, progress |
| `--accent-dim` | `#3B82F6` @ 8–15% opacity | Ambient glow, background wash only |

Contrast check: `--off-white` on `--black` = 19.6:1 (AAA). `--gray` on
`--black` = 7.1:1 (AAA). `--accent` on `--graphite` = 4.6:1 (AA for large/UI
text — used only for headings, pills, and icons, never body copy at small
sizes).

## Typography (system stack — no external font loading)

```
--font-display: -apple-system, "SF Pro Display", "Segoe UI", Inter, ui-sans-serif, system-ui, sans-serif;
--font-body:    Inter, -apple-system, "Segoe UI", ui-sans-serif, system-ui, Helvetica, Arial, sans-serif;
--font-mono:    "JetBrains Mono", "Cascadia Code", Consolas, "SF Mono", ui-monospace, Menlo, monospace;
```

Hierarchy is built with weight + tracking + size, not with headings piled on
headings:

| Role | Size | Weight | Tracking |
|---|---|---|---|
| Display (name) | 56px | 700 | -0.02em |
| Heading | 22px | 600 | -0.01em |
| Body | 15px | 400 | 0 |
| Label / eyebrow | 11px | 600 | 0.08em, uppercase |
| Code | 14px | 500 | 0 |

## Spacing — strict 8px system

`8 · 16 · 24 · 32 · 40 · 48 · 64` — no arbitrary values. Safe margin on all
banner-class assets is **64px** on every edge.

## Radius

`--radius-sm: 10px` (pills' inner elements, tags)
`--radius-md: 16px` (cards, terminal window)
`--radius-lg: 22px` (banner outer frame, hero surfaces)
`--radius-pill: 999px` (pills, badges)

## Elevation (shadow, not blur-heavy glass)

```
--shadow-soft:  0 8px 24px rgba(0,0,0,0.35)
--shadow-tight: 0 2px 8px rgba(0,0,0,0.25)
--highlight-top: inset 0 1px 0 rgba(255,255,255,0.06)
```
Glass is used exactly once across the whole system: the terminal title bar,
as a restrained accent — everything else is matte with hairline borders and
shadow-based depth.

## Motion

- Ambient loops: 4–8s, `ease-in-out`, never below 3s.
- Entrance reveal: one-time, 900–1400ms, gentle translateY(6px)+opacity.
- Cursor blink: 1s step, standard terminal convention (only "fast" motion
  allowed, since it reads as a UI signal, not decoration).
- Every non-essential animation is wrapped so
  `@media (prefers-reduced-motion: reduce)` disables it, leaving only the
  static, fully-readable composition.

## Visual balance target

~70% typography / whitespace / layout hierarchy, ~30% illustration and
ambient effect, on every asset that includes the avatar or background
motion.

## Extending this system

- **New project card**: duplicate the `<use href="#card-frame">` block in
  `assets/projects-dark.svg` / `-light.svg`, increment its `y` offset by
  the card height + `24px` gutter, and update the four text fields. No
  other file needs to change.
- **New tech pill**: add one `<use href="#pill">` + `<text>` pair in the
  pill row of the banner; width auto-adjusts by re-running the pill-width
  helper comment left inline in the SVG.
- **New section in README**: follow the existing narrative voice — a short
  connective sentence, not a bare heading — and reuse the horizontal-rule
  style (`<sub>` divider) already established.
