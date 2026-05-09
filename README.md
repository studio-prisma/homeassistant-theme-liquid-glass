# Liquid Glass — Home Assistant Theme

[![HACS Custom](https://img.shields.io/badge/HACS-Custom-orange.svg)](https://hacs.xyz/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![HA](https://img.shields.io/badge/HA-2024.1.0%2B-blue.svg)]()
[![DE](https://img.shields.io/badge/Lang-DE-lightgrey.svg)](README.de.md)

A premium glass-morphism theme for Home Assistant — translucent surfaces, layered blur, soft accents, refined dark UI. Six variants in one file.

> Maintained by **studio-prisma**.

![Liquid Glass Dashboard Preview](docs/assets/screenshots/preview-main.svg)

## Variants

| Theme name (HA dropdown) | Behavior |
|---|---|
| **Liquid Glass** ⭐ | **Default — always dark** with `aurora.png` background. Recommended. |
| **Liquid Glass Auto (experimental)** | OS-driven light/dark — known HA limitations (see note) |
| **Liquid Glass Light only** | Always light, ignores OS — `dawn.png` background |
| **Liquid Glass Compact** | Always dark + tighter spacing for wall-tablets |
| **Liquid Glass Sunset** | Always dark + warm rose/amber palette |
| **Liquid Glass Floorplan** | Always dark + heatmap glow for picture-element cards |

> ⚠️ **Why "Auto" is experimental:** HA's `modes:` block does not reliably override the `lovelace-background` CSS variable, and certain form/dropdown components (search fields, language picker) may render with mismatched colors. The auto variant is best-effort. For consistent results, pick a fixed variant. To switch automatically by sun position, use a `frontend.set_theme` automation between **Liquid Glass** and **Liquid Glass Light only** — see Auto-Switch Strategy below.

Pick in **Profile → Theme** or per dashboard via `theme: Liquid Glass Compact`.

## Card Anatomy

![Card states](docs/assets/screenshots/preview-cards.svg)

## Mushroom Cards

![Mushroom integration](docs/assets/screenshots/preview-mushroom.svg)

## Features

- Glass-morphism with layered translucent surfaces and blur
- Per-domain status colors: light, switch, climate, cover, fan, media_player, person, lock, vacuum
- **Per-room accent tokens** (`room-living-rgb`, ...) — color cards differently per area
- **Energy Dashboard integration** — grid, solar, battery, gas, water harmonized
- **Notification toast styling** — system pop-ups match the theme
- **Form field & dropdown styling** — language picker, search fields, selects, alarm-code input, time pickers, tooltips, dialog popovers all render correctly in dark mode via HA's dark token system (`modes:` block triggers `darkSemanticColorStyles` + `<meta color-scheme=dark>` injection — see [Architecture](#architecture--token-layers))
- Sidebar refinement, Mushroom & Bubble card tokens
- Card-mod global variables
- **Background Pack** — four PNGs (Aurora, Dawn, Night, Calm)

## Tested With

- Home Assistant Core 2026.5.0
- Frontend 20260509.x (WebAwesome + Material Web 3 components)
- Supervisor 2026.05.0 / OS 17.3
- Browser: Chrome/Firefox/Safari/Edge desktop, iOS Companion App

Minimum supported: **Core 2024.1.0**. WCAG AA contrast verified for all dark variants (audit in v1.2.8).

## Installation

### Step 1 — Theme via HACS

1. **HACS** → **Frontend** → top-right menu → **Custom repositories**
2. URL: `https://github.com/studio-prisma/homeassistant-theme-liquid-glass`
3. Category: **Theme** → **Add** → install
4. Restart HA

`configuration.yaml`:

```yaml
frontend:
  themes: !include_dir_merge_named themes/
```

### Step 2 — Background images (one-time setup)

1. Create folder: `/config/www/liquid_glass/`
2. Download all four PNGs from [`docs/assets/backgrounds/`](docs/assets/backgrounds/) into the new folder:
   - `aurora.png` (default for Liquid Glass, Compact, Floorplan, Auto)
   - `dawn.png` (Light only, Sunset)
   - `night.png` (alternative)
   - `calm.png` (alternative)
3. Reload themes: Developer Tools → YAML → **Reload Themes**

Missing files → fallback to solid background color.

### Step 3 — Activate

**Profile → Theme** → **Liquid Glass** (recommended default).

## Background Pack

| File | Style | Default for |
|---|---|---|
| `aurora.png` | Deep blue ambient | Liquid Glass, Compact, Floorplan, Auto |
| `dawn.png` | Pastel sunrise | Light only, Sunset |
| `night.png` | Indigo + moon + stars | alternative |
| `calm.png` | Minimal teal waves | alternative |

### Switch backgrounds per dashboard

```yaml
title: Home
theme: Liquid Glass
background: 'center / cover no-repeat url("/local/liquid_glass/night.png") fixed'
views:
  - title: Overview
```

### Bring your own image

Any 1920×1200+ PNG/JPG. Drop into `/config/www/liquid_glass/` and reference via dashboard background.

**Free sources:**
- [Unsplash](https://unsplash.com/), [Pexels](https://pexels.com/), [Pixabay](https://pixabay.com/)
- AI generators: Midjourney / DALL-E / Stable Diffusion. Prompt: *"premium dashboard background, deep blue ambient, soft gradient, minimal, 16:10"*

Aim dark, low-contrast, ≤ 500 KB.

## Auto-Switch Strategy (recommended)

Skip the experimental built-in auto and use a HA automation — fully reliable:

```yaml
alias: Theme — Sunset to Dark
trigger:
  - platform: sun
    event: sunset
    offset: "-00:30:00"
action:
  - service: frontend.set_theme
    data:
      name: Liquid Glass

alias: Theme — Sunrise to Light
trigger:
  - platform: sun
    event: sunrise
action:
  - service: frontend.set_theme
    data:
      name: Liquid Glass Light only
```

Full light/dark transitions including backgrounds, no surprises.

## Demo Dashboard

[`docs/demo-dashboard.yaml`](docs/demo-dashboard.yaml) — generic showcase. Adjust entity IDs.

## Card-mod Snippets

For users with [card-mod](https://github.com/thomasloven/lovelace-card-mod):

- [`docs/card-mod-snippets.yaml`](docs/card-mod-snippets.yaml) — nine drop-in mods
- [`docs/floorplan-snippets.yaml`](docs/floorplan-snippets.yaml) — picture-element snippets

## Customization

### Override base colors

```yaml
Liquid Glass:
  primary-color: "#ff7a8a"
  accent-color: "#7af5b8"
```

### Per-room accent tokens

Each variant ships eight room tokens as RGB triplets, ready to use with `rgb()` / `rgba()` for area-specific tinting. Defaults live inside `themes/liquid_glass.yaml`; override per dashboard via card-mod or globally via theme-mixin.

| Token | Default (Liquid Glass) | Suggested area |
|---|---|---|
| `--room-living-rgb` | `255, 180, 84` (amber) | Living room |
| `--room-bedroom-rgb` | `157, 130, 230` (lavender) | Bedroom |
| `--room-office-rgb` | `122, 184, 255` (sky blue) | Office / Workspace |
| `--room-kitchen-rgb` | `255, 139, 74` (coral) | Kitchen |
| `--room-bathroom-rgb` | `100, 220, 220` (teal) | Bathroom |
| `--room-garden-rgb` | `74, 210, 149` (mint) | Garden / Outdoor |
| `--room-garage-rgb` | `120, 120, 130` (graphite) | Garage / Utility |
| `--room-workshop-rgb` | `255, 200, 100` (warm gold) | Workshop / Hobby |

**Use in a card via card-mod:**

```yaml
type: tile
entity: light.living_room_main
card_mod:
  style: |
    ha-card {
      background: rgba(var(--room-living-rgb), 0.18);
      border-left: 3px solid rgb(var(--room-living-rgb));
    }
```

**Override globally (per theme):**

```yaml
Liquid Glass:
  room-living-rgb: "210, 90, 130"   # custom rose for living
  room-office-rgb: "90, 200, 170"   # custom teal for office
```

> Tokens are RGB triplets (no `rgb(...)` wrapper) so you can use them with both `rgb()` for solid colors and `rgba()` for transparency.

## Architecture — Token Layers

HA's frontend has accumulated several CSS-token generations as the codebase evolved. A theme that wants to render correctly on a modern HA install needs to cover all of them — that's why this file is large.

| Layer | Used by | Generation |
|---|---|---|
| `--mdc-*` | Legacy Material Design Components | HA ≤ 2023 |
| `--paper-*` | Polymer-era inputs | HA ≤ 2022 |
| `--input-*`, `--mwc-*` | HA aliases for the above | bridge layer |
| `--wa-color-*`, `--wa-form-control-*` | WebAwesome (Shoelace fork) — modern form controls | HA 2025+ |
| `--ha-color-*`, `--ha-color-fill-*-*-*`, `--ha-color-surface-*` | HA's own semantic token system | HA 2025+ |
| `--md-sys-color-*`, `--md-list-item-*` | Material Web 3 — combo-boxes, dialogs, list items | HA 2025+ |

### How `modes:` unlocks dark mode

HA's resolver (`src/state/themes-mixin.ts`) requires a theme to declare a `modes:` block before it loads `darkSemanticColorStyles` + `darkColorStyles`. Every dark variant in this theme declares an empty `modes: dark: {}` to trigger the load — that's what gives tooltips, dropdown popovers, dialog backgrounds, and active-filter pills their dark backgrounds without us having to enumerate every single token by hand.

Side 