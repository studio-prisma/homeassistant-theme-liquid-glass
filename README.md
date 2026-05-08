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
- **Form field & dropdown styling** — language picker, search fields, selects render correctly in dark mode (no white-on-white text)
- Sidebar refinement, Mushroom & Bubble card tokens
- Card-mod global variables
- **Background Pack** — four PNGs (Aurora, Dawn, Night, Calm)

## Tested With

- Home Assistant Core 2026.5.0
- Frontend 20260429.3
- Supervisor 2026.04.2 / OS 17.3

Minimum supported: **Core 2024.1.0**.

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

```yaml
Liquid Glass:
  primary-color: "#ff7a8a"
  accent-color: "#7af5b8"
```

## Versioning

[Semantic Versioning](https://semver.org/). See [`CHANGELOG.md`](CHANGELOG.md).

## Contributing

See [`CONTRIBUTING.md`](CONTRIBUTING.md).

## Credits

- Designed & maintained by **studio-prisma**
- Mushroom & Bubble card token compatibility ensured

## License

MIT — see [LICENSE](LICENSE).
