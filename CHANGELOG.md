# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.2.5] - 2026-05-08

### Fixed
- **Form-field backgrounds finally dark in dark mode** — The remaining white-background problem on alarm-code input, to-do "add entry", time-pickers, and language/dropdown selectors. Root cause: HA Frontend 2026.x routes these components through two new token namespaces that no prior version of this theme covered:
  - `--ha-color-form-*` (used by `ha-input` → `wa-input` for form-control backgrounds, borders, hover/disabled states)
  - `--md-sys-color-*` and `--md-list-item-*` (used by `ha-combo-box-item`, `ha-generic-picker`, all Material Web 3 dialogs and dropdowns)

  The theme's existing `mdc-*`, `paper-*`, `input-*`, and `wa-color-*` tokens never reached these elements because Home Assistant has migrated their styling to the new token families.

### Added
**HA form-control tokens** (10 per variant — drives all `ha-input` / `wa-input` form controls):
`ha-color-form-background`, `ha-color-form-background-hover`, `ha-color-form-background-disabled`, `ha-color-border-neutral-quiet`, `ha-color-border-neutral-normal`, `ha-color-border-neutral-loud`, `ha-color-border-danger-normal`, `ha-color-text-primary`, `ha-color-text-secondary`, `ha-color-neutral-60`

**Material Web 3 surface tokens** (16 per variant — drives Material Web 3 dialogs, combo-boxes, dropdowns, list-items):
`md-sys-color-surface`, `md-sys-color-surface-container`, `md-sys-color-surface-container-low`, `md-sys-color-surface-container-high`, `md-sys-color-surface-container-highest`, `md-sys-color-surface-variant`, `md-sys-color-on-surface`, `md-sys-color-on-surface-variant`, `md-sys-color-primary`, `md-sys-color-on-primary`, `md-sys-color-secondary-container`, `md-sys-color-on-secondary-container`, `md-sys-color-outline`, `md-sys-color-outline-variant`, `md-sys-color-background`, `md-sys-color-on-background`, `md-list-item-label-text-color`, `md-list-item-supporting-text-color`, `md-list-item-leading-icon-color`, `md-list-item-container-color`

All new tokens use `var(--primary-text-color)`, `var(--card-background-color)` and friends, so per-variant palettes (Sunset rose/amber, Floorplan heatmap) inherit automatically.

### Diagnostic credit
- DOM inspection on `<wa-input>` (To-Do input + alarm-code) confirmed `appearance="material"` + transparent `<input>` background — proving the white background comes from the surrounding container, not the input itself.
- DOM inspection on `<ha-combo-box-item>` (language picker) revealed `color: var(--md-list-item-label-text-color, var(--md-sys-color-on-surface, #1d1b20))` — the `#1d1b20` fallback is what was rendering on dark theme.
- Cross-referenced HA frontend source `src/components/input/ha-input.ts` and `src/components/ha-base-time-input.ts` to enumerate every CSS custom property used.

### Known not-yet-fixed
- `light-dark()`-driven default border colors on native `<input>` elements (the grey 118/118/118 vs 133/133/133 pair) remain — they only respond to the actual CSS `color-scheme` property, which HA exposes only as a regular theme token (rendered as `--color-scheme: dark` and ignored by browsers). Workaround for v1.3.0: ship a small `extra_module_url` JS loader that sets `document.documentElement.style.colorScheme`.

## [1.2.4] - 2026-05-08

### Fixed
- **Form fields with `light-dark()` and `wa-input` now render correctly dark** — HA Frontend 2026.x switched to the WebAwesome component library (`wa-input`, `wa-base`). Many form elements use the native CSS `light-dark()` function which depends on the document's `color-scheme` property — not on any `mdc-*` or `input-*` theme variable. This explains why earlier rounds of fixes didn't fully solve the issue.

### Added
- **`color-scheme: dark`** in every dark variant (and `color-scheme: light` in Light only / Auto's modes:light). Tells the browser to render native form elements, scrollbars, and `light-dark()`-driven CSS in dark mode.
- **WebAwesome surface tokens** for `wa-input` and friends:
  - `wa-color-surface-default` / `-raised` / `-lowered`
  - `wa-color-text-normal` / `-quiet`
  - `wa-color-neutral-fill-quiet` / `-normal`
  - `wa-color-neutral-border-normal`
  - `wa-color-brand-fill-normal` / `-loud` / `-on-loud` / `-text-normal`

### Diagnostic credit
- Caught via Chrome DevTools — the inspected element revealed `wa-input::part(input)` with `border-color: light-dark(...)`. That confirmed the new component model and the `color-scheme` lever.

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

[Unreleased]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.2.4...HEAD
[1.2.4]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.2.3...v1.2.4
[1.2.3]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.2.2...v1.2.3
[1.2.2]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.2.1...v1.2.2
[1.2.1]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.2.0...v1.2.1
[1.2.0]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.1.2...v1.2.0
[1.1.2]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.1.1...v1.1.2
[1.1.1]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.1.0...v1.1.1
[1.1.0]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/releases/tag/v1.0.0
