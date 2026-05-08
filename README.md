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
| **Liquid Glass** | Auto-switch via OS prefers-color-scheme |
| **Liquid Glass Light only** | Always light, ignores OS |
| **Liquid Glass Dark only** | Always dark, ignores OS |
| **Liquid Glass Compact** | Always dark + tighter spacing for wall-tablets |
| **Liquid Glass Sunset** | Always dark + warm rose/amber palette |
| **Liquid Glass Floorplan** | Always dark + heatmap glow for picture-element cards |

Pick in **Profile → Theme** or per dashboard via `theme: Liquid Glass Compact`.

## Card Anatomy

![Card states](docs/assets/screenshots/preview-cards.svg)

## Mushroom Cards

![Mushroom integration](docs/assets/screenshots/preview-mushroom.svg)

All ten `mush-rgb-*` tokens are predefined and used by the [Mushroom card library](https://github.com/piitaya/lovelace-mushroom).

## Features

- Glass-morphism with layered translucent surfaces and blur
- Per-domain status colors: light, switch, climate, cover, fan, media_player, person, lock, vacuum
- **Per-room accent tokens** (`room-living-rgb`, `room-bedroom-rgb`, ...) — color cards differently per area
- **Energy Dashboard integration** — grid, solar, battery, gas, water all harmonized
- **Notification toast styling** — system pop-ups match the theme
- Sidebar refinement, Mushroom & Bubble card tokens
- Card-mod global variables for inline mods
- Three background options: default PNG + Dawn / Night / Calm SVGs

## Tested With

- Home Assistant Core 2026.5.0
- Frontend 20260429.3
- Supervisor 2026.04.2 / OS 17.3

Minimum supported: **Core 2024.1.0**.

## Installation

### Via HACS (Custom Repository)

1. Open **HACS** → **Frontend** → top-right menu → **Custom repositories**
2. URL: `https://github.com/studio-prisma/homeassistant-theme-liquid-glass`
3. Category: **Theme** → **Add**
4. Install **Liquid Glass Theme** from the list
5. Restart Home Assistant
6. **Profile → Theme** → select your variant

`configuration.yaml`:

```yaml
frontend:
  themes: !include_dir_merge_named themes/
```

## Background Image

Default `liquid_glass_bg.png` — copy to `/config/www/` once, active immediately.

### Background Pack

Three vector alternatives in [`docs/assets/backgrounds/`](docs/assets/backgrounds/):

| File | Style |
|---|---|
| `dawn.svg` | Pastel sunrise |
| `night.svg` | Deep indigo + stars |
| `calm.svg` | Minimal teal waves |

**Switch per dashboard (recommended — survives HACS updates):**

```yaml
title: Home
theme: Liquid Glass
background: 'center / cover no-repeat url("/local/dawn.svg") fixed'
views:
  - title: Overview
```

## Auto-Switch (OS-driven)

Pick **Liquid Glass** — follows the system Light/Dark setting on iOS, macOS, Windows. Background image, sidebar, modal dialogs, cards, glass tokens all switch consistently.

For **manual control** (e.g. by sun position), pick `Liquid Glass Light only` or `Liquid Glass Dark only` and run an automation:

```yaml
alias: Theme — Sunset to Dark
trigger:
  - platform: sun
    event: sunset
    offset: "-00:30:00"
action:
  - service: frontend.set_theme
    data:
      name: Liquid Glass Dark only
```

## Demo Dashboard

[`docs/demo-dashboard.yaml`](docs/demo-dashboard.yaml) — generic showcase with Overview / Mushroom / Compact views. Adjust entity IDs to your setup.

## Card-mod Snippets

Two snippet files for users with [card-mod](https://github.com/thomasloven/lovelace-card-mod):

- [`docs/card-mod-snippets.yaml`](docs/card-mod-snippets.yaml) — nine drop-in mods: glass base, status-glow, pulse-on-active, toast styling, per-room tokens, sidebar slim, header hide
- [`docs/floorplan-snippets.yaml`](docs/floorplan-snippets.yaml) — picture-element snippets for the Floorplan variant: room marker, heatmap, warning-pulse

## Customization

All colors and tokens are exposed as theme variables. Quick brand swap:

```yaml
Liquid Glass:
  primary-color: "#ff7a8a"
  accent-color: "#7af5b8"
```

The Sunset variant ships as a pre-baked example of what's possible.

## Versioning

This project follows [Semantic Versioning](https://semver.org/). Changes documented in [`CHANGELOG.md`](CHANGELOG.md) and [GitHub Releases](../../releases).

## Contributing

Issues and PRs welcome — see [`CONTRIBUTING.md`](CONTRIBUTING.md).

## Credits

- Designed & maintained by **studio-prisma**
- Mushroom & Bubble card token compatibility ensured against their respective documentation

## License

MIT — see [LICENSE](LICENSE).
