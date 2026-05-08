# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.2.3] - 2026-05-08

### Fixed
- **More white-on-white form fields** — Time-pickers, date-pickers, password fields, language picker, "add entry" inputs and header-menu hover states still rendered with default browser colors after v1.2.2. HA Frontend uses additional variables that v1.2.2 didn't cover.

### Added
Twenty-five additional theme variables across all variants:

**HA `input-*` aliases** (drives `ha-textfield`, `ha-combo-box`, `ha-time-input`, `ha-date-input`):
`input-fill-color`, `input-ink-color`, `input-label-ink-color`, `input-idle-line-color`, `input-hover-line-color`, `input-outlined-idle-border-color`, `input-outlined-hover-border-color`, `input-disabled-fill-color`, `input-disabled-ink-color`, `input-disabled-line-color`

**Outlined text fields**:
`mdc-text-field-outlined-idle-border-color`, `mdc-text-field-outlined-hover-border-color`, `mdc-text-field-outlined-disabled-border-color`

**Menu surfaces & text colors** (dropdown background, list text, hint text):
`mdc-menu-surface-fill-color`, `mdc-theme-text-primary-on-background`, `mdc-theme-text-secondary-on-background`, `mdc-theme-text-hint-on-background`, `mdc-theme-text-disabled-on-background`

**Hover states** (header menu, list rows):
`mdc-list-item-hover-state-layer-color`, `mdc-list-item-hover-state-layer-opacity`, `mdc-list-item-focus-state-layer-color`

**Disabled buttons** (Save / Submit when greyed):
`mdc-button-disabled-fill-color`, `mdc-button-disabled-ink-color`, `mdc-button-outline-color`

All values present in every dark variant (Liquid Glass, Compact, Sunset, Floorplan, Auto's main block) plus light pendants in Light only and Auto's modes:light.

## [1.2.2] - 2026-05-08

### Changed
- **Renaming for clarity** — "Liquid Glass" is now the **default fixed-dark variant** (recommended). The OS-driven auto-switch was renamed to "Liquid Glass Auto (experimental)" and clearly marked as best-effort.
  - Old `Liquid Glass Dark only` → renamed to `Liquid Glass`
  - Old `Liquid Glass` (auto-switch) → renamed to `Liquid Glass Auto (experimental)`

### Fixed
- **White text on white background in form fields** — language picker, search inputs, dropdowns and select components rendered with default browser white due to missing `mdc-text-field-*` and `mdc-select-*` theme variables. Fixed by setting:
  - `mdc-text-field-fill-color`, `mdc-text-field-ink-color`, `mdc-text-field-label-ink-color`, `mdc-text-field-idle-line-color`, `mdc-text-field-hover-line-color`, `mdc-text-field-disabled-*`
  - `mdc-select-fill-color`, `mdc-select-ink-color`, `mdc-select-label-ink-color`, `mdc-select-idle-line-color`, `mdc-select-disabled-*`
  - `mdc-list-item-text-color`, `mdc-list-item-graphic-color`, `mwc-list-item-text-color`
  - `paper-listbox-background-color`, `paper-listbox-color`
  - `paper-input-container-color`, `paper-input-container-input-color`, `paper-input-container-focus-color`
  - All variables present in every dark variant + light pendants in Light only and Auto's modes:light block.

### Migration
- If you previously had **"Liquid Glass"** active (auto-switch), you'll now see the fixed dark variant — same look as before but no more light-mode mixing on iOS.
- If you actively want the experimental auto behavior, switch to **"Liquid Glass Auto (experimental)"** in Profile → Theme.

## [1.2.1] - 2026-05-08

### Fixed
- **Auto-switch background bug** — `lovelace-background` could not reliably be overridden in `modes:light` (HA `modes:` block limitation with complex CSS shorthands). The `Liquid Glass` auto-switch variant no longer sets a background image — it switches colors only. For full light/dark with backgrounds, switch between `Liquid Glass Light only` and `Liquid Glass Dark only` via automation (see README).

### Changed
- **Background folder reorganized** — all four backgrounds now live in `/config/www/liquid_glass/` (instead of `/config/www/`). Cleaner structure, easier to manage.
- **All backgrounds are now PNGs** — `aurora.png`, `dawn.png`, `night.png`, `calm.png`. Higher visual fidelity than the previous SVG vectors. Each ~300–500 KB.
- Theme paths updated: `/local/liquid_glass/aurora.png` (was `/local/liquid_glass_bg.png`), `/local/liquid_glass/dawn.png` (was `/local/dawn.svg`).
- README rewritten with clearer 3-step install (theme + backgrounds + activate) and a section pointing users to free background sources (Unsplash, Pexels, AI generators).

### Removed
- `dawn.svg`, `night.svg`, `calm.svg` from `docs/assets/backgrounds/` (replaced by PNG versions).
- `liquid_glass_bg.png` from `docs/assets/` (now `docs/assets/backgrounds/aurora.png`).

### Migration
- Create `/config/www/liquid_glass/` and copy all four PNGs in.
- If you had `liquid_glass_bg.png` in `/config/www/`, you can remove it.
- Theme will fall back to solid color if PNG is missing — no crash.

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

[Unreleased]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.2.3...HEAD
[1.2.3]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.2.2...v1.2.3
[1.2.2]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.2.1...v1.2.2
[1.2.1]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.2.0...v1.2.1
[1.2.0]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.1.2...v1.2.0
[1.1.2]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.1.1...v1.1.2
[1.1.1]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.1.0...v1.1.1
[1.1.0]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/releases/tag/v1.0.0
