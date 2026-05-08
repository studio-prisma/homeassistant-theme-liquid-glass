# Liquid Glass — Home Assistant Theme

[![HACS Custom](https://img.shields.io/badge/HACS-Custom-orange.svg)](https://hacs.xyz/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Maintained](https://img.shields.io/badge/Maintained-yes-green.svg)]()

A premium glass-morphism theme for Home Assistant — translucent surfaces, layered blur, soft accents, and a refined dark UI.

> Maintained by **studio-prisma**.

## Preview

<!-- Add screenshots to docs/screenshots/ and reference them here -->
<!-- ![Preview](docs/screenshots/preview.png) -->

*Screenshots coming soon.*

## Features

- Layered translucent surfaces with subtle blur
- Soft cyan accent (`#7ab8ff`) with warm amber state-glow (`#ffb454`)
- Optimized for dark dashboards
- Works with standard Lovelace cards out of the box
- Smooth color transitions across all UI elements

## Requirements

- Home Assistant `2024.1.0` or newer
- Frontend theme support enabled in `configuration.yaml`:

  ```yaml
  frontend:
    themes: !include_dir_merge_named themes/
  ```

## Installation

### Via HACS (Custom Repository)

1. Open **HACS** in Home Assistant.
2. Go to **Frontend** → top-right menu → **Custom repositories**.
3. Add this URL: `https://github.com/studio-prisma/homeassistant-theme-liquid-glass`
4. Category: **Theme**.
5. Click **Add**, then install **Liquid Glass Theme** from the list.
6. Restart Home Assistant.
7. Go to **Profile** → **Theme** → select **Liquid Glass**.

### Manual Installation

1. Copy `themes/liquid_glass.yaml` to `<config>/themes/`.
2. Ensure `configuration.yaml` includes:

   ```yaml
   frontend:
     themes: !include_dir_merge_named themes/
   ```

3. Restart Home Assistant.
4. Activate the theme in your profile or per-dashboard settings.

## Customization

All colors are exposed as theme variables. To override a value, create a custom theme that extends Liquid Glass or edit the YAML directly. The variables are grouped by purpose (surfaces, text, accent, states, sidebar, cards) — see comments inside `themes/liquid_glass.yaml`.

## Versioning

This project follows [Semantic Versioning](https://semver.org/). Changes are documented in [GitHub Releases](../../releases).

## Contributing

Issues and pull requests are welcome. For larger changes, please open an issue first to discuss.

## Credits

- Designed & maintained by **studio-prisma**
- Thanks to the Home Assistant and HACS communities

## License

MIT — see [LICENSE](LICENSE).
