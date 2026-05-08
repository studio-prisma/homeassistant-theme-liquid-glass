# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.2.0] - 2026-05-08

### Added
- **Six theme variants** with clear semantic naming:
  - `Liquid Glass` — auto-switch via OS prefers-color-scheme (full coverage: background image, sidebar, modal, cards, glass tokens)
  - `Liquid Glass Light only` — always light, ignores OS
  - `Liquid Glass Dark only` — always dark, ignores OS
  - `Liquid Glass Compact` — always dark + tighter spacing
  - `Liquid Glass Sunset` — always dark + warm rose/amber palette (NEW)
  - `Liquid Glass Floorplan` — always dark + heatmap-glow tokens for picture-element cards (NEW)
- **Per-room accent tokens** — `room-living-rgb`, `room-bedroom-rgb`, `room-office-rgb`, `room-kitchen-rgb`, `room-bathroom-rgb`, `room-garden-rgb`, `room-garage-rgb`, `room-workshop-rgb`. Use via card-mod or as state colors.
- **Energy Dashboard variables** — `energy-grid-consumption-color`, `energy-grid-return-color`, `energy-solar-color`, `energy-battery-in-color`, `energy-battery-out-color`, `energy-non-fossil-color`, `energy-gas-color`, `energy-water-color`. Built-in HA Energy view now matches the theme.
- **Notification toast variables** — `mdc-snackbar-fill-color`, `mdc-snackbar-action-color`, `ha-toast-background-color`, `ha-toast-text-color`. System pop-ups stay on-brand.
- **Floorplan-specific tokens** — `floorplan-room-default-glow`, `floorplan-room-active-glow`, `floorplan-room-warning-glow`, `floorplan-room-cool-glow`, `floorplan-area-border`, `floorplan-area-radius`, `floorplan-area-blur`.
- **`docs/floorplan-snippets.yaml`** — picture-element snippets: room marker, heatmap, warning-pulse.
- **`docs/card-mod-snippets.yaml`** extended with snippets 7–9: toast styling, pulse-on-active (pure CSS, no Pyscript), per-room glow.
- **`README.de.md`** — German translation of the README.

### Changed
- **Auto-switch in `Liquid Glass` is now complete** — every relevant variable is mirrored in `modes:light` (background image, sidebar colors, modal vars, glass tokens, scrim). No more half-applied light mode on iOS.
- README rewritten around the six-variant model.

### Removed
- The previous `modes:` block that only switched a subset of variables (causing the iOS half-light/half-dark bug). Replaced by the complete `modes:` block in `Liquid Glass` and the standalone variants.

## [1.1.2] - 2026-05-08

### Fixed
- **Mixed light/dark rendering on iOS** — Removed incomplete `modes:` block from "Liquid Glass". Each variant now stays consistent.

## [1.1.1] - 2026-05-08

### Fixed
- **System UI legibility** — Settings dialogs were shown semi-transparent and visually overlapped by underlying setting cards. Modal/dialog surfaces are now opaque.
- **Card stacking context** — `card-background-color` from `rgba(255,255,255,0.05)` to `rgba(20,25,40,0.75)`. Eliminates Frontend 20260429.3 stacking-context bug.

### Changed
- Background image active by default. Font stack replaced with cross-platform neutral stack.

### Added
- Background Pack (`dawn.svg`, `night.svg`, `calm.svg`).

## [1.1.0] - 2026-05-08

### Added
- Liquid Glass Light & Compact variants
- Background image support, sidebar refinement, per-domain status colors
- Animation variables, extended Mushroom tokens
- Demo dashboard, card-mod snippets, three SVG previews

## [1.0.0] - 2026-05-08

### Added
- Initial public release of Liquid Glass Theme

[Unreleased]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.2.0...HEAD
[1.2.0]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.1.2...v1.2.0
[1.1.2]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.1.1...v1.1.2
[1.1.1]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.1.0...v1.1.1
[1.1.0]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/releases/tag/v1.0.0
