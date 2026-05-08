# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.1.0] - 2026-05-08

### Added
- **Liquid Glass Light** — standalone light variant (separate top-level theme key)
- **Liquid Glass Compact** — tighter spacing variant for wall-tablets and small displays
- **Background image support** — `lovelace-background` variable (commented out by default), preset asset shipped at `docs/assets/liquid_glass_bg.png`
- **Sidebar refinement** — `sidebar-icon-color`, `sidebar-text-color`, `sidebar-selected-icon-color`, `sidebar-selected-text-color`, `sidebar-selected-background-color`
- **Per-domain status colors** extended: `state-cover-active-color`, `state-fan-active-color`, `state-media_player-active-color`, `state-person-active-color`, `state-lock-active-color`, `state-vacuum-active-color`
- **Animation variables** — `transition-duration`, `transition-timing-function`
- **Extended Mushroom tokens** — `mush-control-border-radius`, `mush-control-height`, `mush-icon-border-radius`, `mush-card-primary-font-size`, `mush-card-secondary-font-size`
- **Demo dashboard** at `docs/demo-dashboard.yaml` (Overview / Mushroom / Compact views)
- **Card-mod snippets** at `docs/card-mod-snippets.yaml` (6 drop-in mods)
- **Visual previews** — three SVG mockups in `docs/assets/screenshots/` (main / cards / mushroom)

### Changed
- README rewritten with hero preview, variant overview, tested-versions block, background-image guide, demo-dashboard guide, card-mod section
- `info.md` updated with hint about variants and tested versions

### Tested
- Home Assistant Core 2026.5.0
- Supervisor 2026.04.2
- Operating System 17.3
- Frontend 20260429.3

## [1.0.0] - 2026-05-08

### Added
- Initial public release of Liquid Glass Theme
- Glass-morphism aesthetic with layered translucent surfaces
- Soft cyan accent (`#7ab8ff`) with warm amber state-glow (`#ffb454`)
- Optimized color variables for dark dashboards
- Full coverage of Home Assistant 2024.1.0+ theme variables

[Unreleased]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.1.0...HEAD
[1.1.0]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/releases/tag/v1.0.0
