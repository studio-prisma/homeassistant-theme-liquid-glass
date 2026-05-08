# Liquid Glass — Home Assistant Theme

[![HACS Custom](https://img.shields.io/badge/HACS-Custom-orange.svg)](https://hacs.xyz/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Maintained](https://img.shields.io/badge/Maintained-yes-green.svg)]()
[![HA Version](https://img.shields.io/badge/HA-2024.1.0%2B-blue.svg)]()

A premium glass-morphism theme for Home Assistant — translucent surfaces, layered blur, soft accents, and a refined dark UI. Three variants in one file: **Dark** · **Light** · **Compact**.

> Maintained by **studio-prisma**.

![Liquid Glass Dashboard Preview](docs/assets/screenshots/preview-main.svg)

---

## Variants

| Variant | When to use |
|---|---|
| **Liquid Glass** (default) | Standard dark glass dashboard |
| **Liquid Glass Light** | Daytime / bright-room dashboards |
| **Liquid Glass Compact** | Wall-tablets, small displays, dense grids |

All three are bundled in `themes/liquid_glass.yaml`. Switch them in **Profile → Theme** or per-dashboard via `theme: Liquid Glass Compact`.

---

## Card Anatomy

![Card states](docs/assets/screenshots/preview-cards.svg)

Three states are styled by the theme: **idle** (passive surface), **active warm** (light, climate-heating), **active cool** (switch, climate-cooling). Color tokens are exposed as theme variables — override them per-dashboard if you want a different palette.

---

## Mushroom Cards

![Mushroom integration](docs/assets/screenshots/preview-mushroom.svg)

All ten `mush-rgb-*` tokens are predefined and used directly by the [Mushroom card library](https://github.com/piitaya/lovelace-mushroom). No extra setup — installing both works out of the box.

---

## Features

- Glass-morphism aesthetic with layered translucent surfaces
- Soft cyan accent (`#7ab8ff`) with warm amber state-glow (`#ffb454`)
- Per-domain status colors for **light, switch, climate, cover, fan, media_player, person, lock, vacuum**
- Refined sidebar (icon, text, selected state, hover background)
- Mushroom card tokens (10 RGB tokens, control radius, icon radius, font sizes)
- Bubble Card tokens
- Card-mod global variables (`--glass-bg`, `--glass-blur`, `--glass-radius` etc.) for inline mods
- Optional background image support via `lovelace-background`
- Three variants: Dark · Light · Compact

---

## Tested With

[Schlussfolgerung] Verified working on:

- **Home Assistant Core** 2026.5.0
- **Supervisor** 2026.04.2
- **Operating System** 17.3
- **Frontend** 20260429.3

Minimum supported: **Core 2024.1.0** — earlier versions are missing some required theme variables.

---

## Requirements

- Home Assistant `2024.1.0` or newer
- Frontend theme support enabled in `configuration.yaml`:

  ```yaml
  frontend:
    themes: !include_dir_merge_named themes/
  ```

---

## Installation

### Via HACS (Custom Repository)

1. Open **HACS** in Home Assistant.
2. Go to **Frontend** → top-right menu → **Custom repositories**.
3. Add this URL: `https://github.com/studio-prisma/homeassistant-theme-liquid-glass`
4. Category: **Theme**.
5. Click **Add**, then install **Liquid Glass Theme** from the list.
6. Restart Home Assistant.
7. Go to **Profile** → **Theme** → select **Liquid Glass** (or Light / Compact).

### Manual Installation

1. Copy `themes/liquid_glass.yaml` to `<config>/themes/`.
2. Ensure `configuration.yaml` includes the frontend block above.
3. Restart Home Assistant.
4. Activate the theme in your profile or per-dashboard settings.

---

## Optional: Background Image

The theme ships with a preset background image. To use it:

1. Download [`docs/assets/liquid_glass_bg.png`](docs/assets/liquid_glass_bg.png) from this repo.
2. Copy it into your HA `/config/www/` folder.
3. In `themes/liquid_glass.yaml` (your installed copy), uncomment this line:

   ```yaml
   lovelace-background: 'center / cover no-repeat url("/local/liquid_glass_bg.png") fixed, var(--primary-background-color)'
   ```

4. Reload themes (Developer Tools → YAML → Reload Themes).

The comma-fallback ensures that if the image fails to load, the dashboard falls back to the regular background color.

**Bring your own image:** any 1920×1200+ PNG/JPG works. Lower opacity if it competes with cards — `opacity: 0.6` via card-mod or via a darkened version of the file.

---

## Demo Dashboard

A ready-to-use showcase dashboard is included at [`docs/demo-dashboard.yaml`](docs/demo-dashboard.yaml). It contains three views (Overview, Mushroom, Compact) and demonstrates the theme's strengths.

Import:

1. Settings → Dashboards → Add Dashboard → name it "Liquid Glass Demo"
2. Open the new dashboard → top-right menu → **Edit dashboard** → top-right menu → **Raw configuration editor**
3. Paste the contents of `docs/demo-dashboard.yaml`
4. Adjust entity references to your setup (`light.living_room`, `climate.thermostat`, etc.)

---

## Card-mod Snippets

For users with [card-mod](https://github.com/thomasloven/lovelace-card-mod) installed, drop-in CSS snippets are included at [`docs/card-mod-snippets.yaml`](docs/card-mod-snippets.yaml). Six snippets cover:

1. Universal glass card base
2. Status-glow overlays (warm / cool / violet / mint)
3. Pill-shape toggle
4. Mushroom card glass skin
5. Sidebar slim mode
6. Header hide (for wall-tablets)

All snippets reference theme variables, so they adapt automatically when you switch between Dark / Light / Compact.

---

## Customization

All colors are exposed as theme variables. To override a value, create a custom theme that extends Liquid Glass or edit the YAML directly. Variables are grouped by purpose (surfaces, text, accent, sidebar, states, ha-card, mushroom, bubble, card-mod) — see comments inside `themes/liquid_glass.yaml`.

Quick brand-color swap:

```yaml
Liquid Glass:
  primary-color: "#ff7a8a"      # your brand pink
  accent-color: "#7af5b8"       # your brand mint
  # rest stays the same
```

---

## Versioning

This project follows [Semantic Versioning](https://semver.org/). Changes are documented in [`CHANGELOG.md`](CHANGELOG.md) and [GitHub Releases](../../releases).

---

## Contributing

Issues and pull requests are welcome — see [`CONTRIBUTING.md`](CONTRIBUTING.md). For larger changes, please open an issue first to discuss.

---

## Credits

- Designed & maintained by **studio-prisma**
- Thanks to the Home Assistant and HACS communities
- Mushroom & Bubble card token compatibility ensured against their respective documentation

---

## License

MIT — see [LICENSE](LICENSE).
