# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Changed
- **"Tested With" refreshed** to Core 2026.8.1 / Frontend 20260729.6 / Supervisor 2026.07.5 / OS 18.2 in README, README.de and info.md — the previous entry still named Core 2026.5.0. Added a note asking reporters for the frontend build number alongside the Core version, because component styling can differ between frontend builds shipping with the same Core release, which is what made [#5](https://github.com/studio-prisma/homeassistant-theme-liquid-glass/issues/5) hard to pin down.

## [1.5.1] - 2026-08-09

### Fixed
- **Heading cards no longer receive the glass treatment** (all 7 variants). HA's heading card is chrome-less by design and resets `background`, `border` and `box-shadow` on its own `ha-card`, which outranked the theme's zero-specificity `:where(ha-card)` rule — but the running frontend build carried **no `backdrop-filter` reset**, so the global blur applied unopposed and left a blurred rectangle where the card is otherwise invisible. Diagnosed by dumping the heading card's `adoptedStyleSheets` at runtime, not inferred from upstream source. The theme now resets the glass properties itself via `:host(.type-heading) ha-card, :host(hui-heading-card) ha-card` (specificity `0,1,1`), so the result no longer depends on what upstream happens to reset. ([#5](https://github.com/studio-prisma/homeassistant-theme-liquid-glass/issues/5))
- **README + README.de "Customization" section rewritten** — the `Liquid Glass: primary-color: …` snippet was shown without any indication of where it belongs, and the obvious reading (a separate file in `config/themes/`) silently destroys the theme: Home Assistant merges theme files with a flat `dict.update()` via `!include_dir_merge_named`, so a second file reusing the `Liquid Glass` key replaces the entire theme instead of extending it. New "Where customization goes" subsection documents the two routes that work (derived variant / edit in place), the `card-mod-theme:` rename that Route A requires, and the Reload-Themes step. Same correction applied to the per-room token override block. ([#4](https://github.com/studio-prisma/homeassistant-theme-liquid-glass/issues/4))

### Changed
- **The global `card-mod-card` block is defined once and reused via a YAML anchor** (`&glass_card_mod` / `*glass_card_mod`). It had been duplicated verbatim across six variants, which is why the missing heading-card exception had to be fixed in six places rather than one. Liquid Glass Lite keeps its own block (no `backdrop-filter`). Purely structural — the parsed theme dictionary is byte-identical to before.

## [1.5.0] - 2026-05-19

Promotion of `v1.5.0-rc.1` to stable after HACS-beta-channel soak-test. No functional changes since the release candidate — see the [1.5.0-rc.1](#150-rc1---2026-05-18) section below for the full change list.

## [1.5.0-rc.1] - 2026-05-18

### Added
- **Liquid Glass Lite variant** (7th variant in `themes/liquid_glass.yaml`) — same translucent look, **no `backdrop-filter`**. Targets wall tablets, older iPads, and low-end devices where GPU-blur is expensive. Inherits the same `--glass-*` tokens as the default variant; only `glass-bg` slightly more opaque (0.09 vs 0.05) to keep visual depth without blur.
- **Auto-Switch Blueprint** at `blueprints/automation/studio-prisma/liquid_glass_auto_switch.yaml` — 1-click sunset/sunrise theme-toggle via My-Home-Assistant import button. Inputs for dark/light theme name, sunset/sunrise offsets, optional notification.
- **My-Home-Assistant install button** in README EN + DE — `my.home-assistant.io/redirect/hacs_repository/` redirect drops HACS-install-flow from ~5 steps to 1 click.
- **My-Home-Assistant blueprint import button** in README EN + DE — `my.home-assistant.io/redirect/blueprint_import/` redirect for the new Auto-Switch Blueprint.
- README + README.de **FAQ entry "Can I use my own background image without copying PNGs?"** — documents `background: url(...)` dashboard-level override, both remote URLs and local `/config/www/` paths.
- README + README.de **Liquid Glass Lite section** in Variants table and "What you get out of the box" table.
- README + README.de **v1.5.0 banner line** under the existing v1.4.0 plug-and-play banner, summarizing the three new highlights.

### Changed
- **Global `card-mod-card` rule now uses CSS `:where(ha-card)`** instead of `ha-card` (all 7 variants). Zero-specificity selector means a per-card `card_mod` block with a regular `ha-card` selector wins automatically — no `!important` needed for user overrides.
- README + README.de **"Want to override per card?"** subsection extended with a note explaining the `:where()` specificity behavior.
- README + README.de **Auto-Switch section** restructured: "Auto-Switch Blueprint (1-click install)" is now the primary path; the manual YAML automation pattern is kept as "Auto-Switch Strategy (manual YAML — alternative)".

### Notes
- This is a **release candidate** — not a stable v1.5.0. Tagged `v1.5.0-rc.1` for community testing. Promotion to `v1.5.0` after smoke-test feedback from early adopters.
- Bubble Card compatibility: continues to require post-v3.2.0-beta4 (no change from v1.4.0).


## [1.4.0] - 2026-05-18

### Added
- **Global `card-mod-card` rule shipped in all six theme variants** — every `ha-card` now automatically gets the full glass-morphism look (translucent surface, `backdrop-filter` blur, soft border, glass-grade shadow). Replaces the previous per-card opt-in (`glass_card_base` snippet under each card). Closes the "Does every card need the card-mod snippet?" community-forum feedback ([thread post #3](https://community.home-assistant.io/t/liquid-glass-premium-glass-morphism-theme-with-six-variants/1009825/3)).
- README + README.de **"What you get out of the box" section** (replaces the previous "Effect Tiers" Tier-1-vs-Tier-2 split). Documents the global rule, lists card-family expectations, and explains the v1.3.x → v1.4.0 architectural change.
- README + README.de **"Why v1.4.0" subsection** documenting the upstream Bubble Card issue #2347 fix (pop-ups moved outside `ha-card` tree, post-v3.2.0-beta4) that makes a global blur safe again.
- Prerequisites block in README + README.de + info.md: `card-mod` is now a hard install requirement (was: optional for "extras only"); minimum Bubble Card release for pop-up compatibility documented.

### Changed
- **Plug-and-play banner** (README + README.de + info.md) reformulated from "Plug-and-play, with two effect tiers" → "True plug-and-play". Tier-1 vs. Tier-2 terminology removed throughout — there is now only one tier.
- **FAQ "Do I need card-mod for every card?"** rewritten — card-mod is required once (HACS install), no per-card work.
- **FAQ "Why don't my Tile/Thermostat/Area cards have the same blur as the screenshots?"** rewritten — they should, since v1.4.0; if not, troubleshooting steps (card-mod installed? Bubble Card current? Edit-Mode off? Cache cleared?).
- **FAQ "What dashboard cards are shown in the screenshots?"** clarified — since v1.4.0 every visible card (including stock Tile) renders with the full glass look out-of-the-box.
- **Screenshot captions** updated for Overview and Home Security views — no more references to "Tier-2 snippet".
- **`docs/card-mod-snippets.yaml` snippet #1 (`glass_card_base`) header** rewritten — explains it is now built-in, kept as a copy-paste template for per-card overrides + as a YAML anchor for shared dashboard overrides.
- **"Optional: Card-mod Snippets" section** intro: `card-mod` is now required (for the global rule); listed snippets are opt-in extras *beyond* that.

### Decided
- v1.4.0 is a minor version bump (not patch) because the default behavior changes: previously a global blur was deliberately not shipped (Bubble Card pop-up safety), now it is. Users on Bubble Card builds older than v3.2.0-beta4 will see empty pop-ups under the new global blur — documented as a prerequisite, not a regression.

### Added
- `SECURITY.md` — disclosure policy. Documents the narrow security surface (frontend theme = no backend, no user data, no auth), points reporters to GitHub Private Vulnerability Reporting, defines a 14-day first-response target, lists supported versions (1.3.x), and clarifies out-of-scope items.
- Three real dashboard screenshots replacing the previous SVG mockups: `preview-welcome.png` (hero — Welcome Home dashboard with gauges, energy stats, 24h temperature graph), `preview-overview.png` (Mushroom-style lights/media/switches/vacuum grid), `preview-security.png` (Home Security view with door sensors, cameras, presence tiles).
- `docs/demo-dashboard.yaml` — fully sanitized generic showcase. All entity IDs and labels migrated to placeholder names (`light.living_room`, `switch.dishwasher`, `media_player.tv_living_room`, etc.) so users can map directly to their own setup. No personal references, no brand-specific identifiers (Verisure, Roborock, Samsung, Somneo etc. removed).
- README **plug-and-play banner** directly under the hero image: explicit statement that the theme works on stock Lovelace cards with no per-card configuration. Clarifies that `card-mod` is optional and only required for the advanced snippets in `docs/`.
- README **FAQ section** addressing the most common adoption questions: "Do I need card-mod for every card?" (no), "Do I need to edit YAML?" (no), "What cards are in the screenshots?" (stock + popular community), background-install rationale, troubleshooting pointer.
- `info.md` plug-and-play note added so the same clarification appears in HACS' detail panel without users having to scroll into the README.
- `CONTRIBUTING.md` "Translations" section: documents EN as source-of-truth, DE as best-effort by the maintainer, opens the door for community-PR translations (FR, ES, IT, NL, etc.) with clear contribution rules and a stale-translation-removal policy.
- README + README.de **"Effect Tiers" section** between Features and Tested With. Per-card-family table (Tile / Thermostat / Area / Entities / Mushroom / Bubble Card / picture-elements) makes explicit what the theme delivers at Tier 1 (automatic, no plugin) vs. Tier 2 (opt-in via `glass_card_base` snippet). Includes the 8-line copy-paste recipe and a short rationale for why a global `ha-card` blur is intentionally not shipped (Bubble Card v3 pop-up compatibility). Addresses community forum feedback that "tile / thermostat / area cards don't show the same blur as the screenshots".
- README + README.de **new FAQ entry** "Why don't my Tile / Thermostat / Area cards have the same blur as the screenshots?" — points to the Effect Tiers section and the copy-paste snippet.
- `docs/card-mod-snippets.yaml` **expanded header for snippet #1 `glass_card_base`** — explicitly labels it as "the 'screenshot look' recipe", documents the design choice not to ship a global `ha-card` blur (Bubble Card issue #2347), and inlines a usage example so users don't have to scroll.

### Changed
- README hero + sections updated. "Card Anatomy" → "Overview — Lights, Media, Switches" and "Mushroom Cards" → "Home Security View" with matching real-screenshot captions.
- README "Card-mod Snippets" section retitled to "**Optional: Card-mod Snippets**" with an explicit opt-in note ("Skip this section unless you want extra polish"). The per-room accent token example now leads with the theme-only path (no plugin required) and presents the card-mod variant as the optional second option — closes the community feedback "Does every card need the card-mod snippet?".
- README + README.de **hero banner reformulated** from a flat "plug-and-play" assertion to an honest two-tier description ("Plug-and-play, with two effect tiers"). Tier 1 = automatic token-inheritance; Tier 2 = opt-in backdrop blur via card-mod. Eliminates the expectation gap between the screenshot aesthetic (which uses Tier-2 snippets on stock cards) and what users see immediately after install on Tile / Thermostat / Area cards.
- README + README.de **screenshot captions** clarified for Overview and Home Security views — explicit note that Mushroom cards bring their own blur while stock Tile/Thermostat cards in the same screenshot use the Tier-2 snippet.
- README + README.de **"Optional: Card-mod Snippets" section** now references twelve snippets (was nine pre-v1.3.x) and explicitly names `glass_card_base` as the Tier-2 starting point.

### Fixed
- README badge row: empty `href` on the HA-version badge (`[![HA](...)]()`) was breaking subsequent badges in HACS' Markdown renderer (License, Lang showed as plain text instead of badge images). HA badge now points to https://www.home-assistant.io/. Reordered badges in adoption-priority sequence (HACS · Min HA · License · Lang). DE-language badge label switched from "DE" to "Deutsch" for clarity.
- `README.de.md` fully resynchronized with the EN README — was lagging behind for several releases. Now mirrors all current content: plug-and-play banner, Overview/Home-Security section names, real screenshot refs, Optional Card-mod heading, theme-only-first per-room accent example, Auto-variant WCAG audit closure, FAQ section.

### Removed
- SVG mockups in `docs/assets/screenshots/` (`preview-main.svg`, `preview-cards.svg`, `preview-mushroom.svg`) — superseded by the three real PNGs above.

### Decided
- **Code scanning (CodeQL etc.) intentionally not enabled.** Codebase is YAML and Markdown only — no executable program logic to analyze. Supply-chain hygiene for GitHub Actions covered by Dependabot. Documented in `SECURITY.md` so the "Code scanning alerts: Enabled" status without a backing workflow is recognized as a deliberate maintainer choice, not an oversight.

## [1.3.0] - 2026-05-09

### Added
- README "Architecture — Token Layers" section (EN + DE) documenting the six token generations the theme has to cover (mdc / paper / input / wa-color / ha-color-fill / md-sys-color) and the `modes:` mechanic that unlocks HA's dark token system.
- README "Known limitations" subsection clarifying Auto-theme behavior and v1.2.8 audit scope.
- CONTRIBUTING "Diagnosing color / white-on-white / unreadable text bugs" section with DOM-inspect walkthrough — meant to prevent the speculative-fix-stacking pattern that hit v1.2.2–v1.2.4.
- `.github/workflows/release.yml` — auto-creates a GitHub Release with extracted CHANGELOG notes whenever a `v*` tag is pushed. Includes `workflow_dispatch` for backfilling releases on existing tags.
- `.github/workflows/validate.yml` — HACS Action validation for category `theme` on push, pull_request, daily schedule, and manual dispatch.
- `.github/dependabot.yml` — weekly bumps of GitHub Actions dependencies (Mondays, Europe/Berlin), labeled `dependencies` + `ci`.
- README "Per-room accent tokens" subsection (EN + DE) documenting the eight `--room-*-rgb` tokens with default values, suggested areas, and concrete card-mod + theme-override examples.

### Changed
- `hacs.json` `name`: "Liquid Glass Theme" → "Liquid Glass by Studio Prisma" (HACS-listing branding only — in-HA theme dropdown labels unchanged for backwards compatibility with existing `theme: Liquid Glass` configs).
- `info.md` tested-versions block synced with current README (HA Core 2026.5.0, Frontend 20260509.x, Supervisor 2026.05.0, OS 17.3) plus explicit minimum-supported note.

### Fixed (Auto-Variant `modes.light` WCAG AA audit — completed v1.2.8 deferral)
Re-ran the same 13-pair contrast methodology from v1.2.8, this time on the Auto variant's nested `modes.light` block. Initial audit found 3 marginal fails — all fixed in this release:

- **`text-primary-color`** in `modes.light`: `"#0a0d18"` → `"#ffffff"`. Was inheriting near-black from the dark-mode definition; on the mid-blue brand accent the contrast was 3.63:1 (FAIL). Fix raises filled-brand button text to **5.34:1** (full WCAG AA pass).
- **`primary-color`** in `modes.light`: `"#3a7fcf"` → `"#2a6cb8"`. Aligned with the v1.2.8 dark-primary token. Tinted-brand text on white card was 4.10:1 (marginal fail), now **5.34:1** (full WCAG AA pass).
- **`error-color`** added to `modes.light`: `"#c4334a"` (previously fell back to dark-mode `#ff5a6e`, which had only 3.03:1 on white card). Now **5.36:1** (full WCAG AA pass).

Full audit result: **all 13 critical pairs pass** (3.78:1 sidebar-icon to 17.18:1 sidebar-selected).

## [1.2.8] - 2026-05-09

### Fixed (WCAG AA contrast audit)
Systematic audit of all foreground/background pairs across all variants. Two findings remediated:

- **Light only — sidebar selected text was unreadable** on the semi-transparent blue tint over cream background. Changed `sidebar-selected-text-color` from a fixed dark hex to `var(--primary-text-color)` so it inherits the variant's primary text and stays legible.
- **Liquid Glass / Compact / Floorplan — filled brand-button text contrast at 4.10:1** (marginal WCAG AA fail). Adjusted `--dark-primary-color` from `#3a7fcf` to `#2a6cb8` (slightly darker mid-blue). White text on the new accent now hits **5.47:1** (full WCAG AA pass). Sunset's rose accent (`#cf3a7f`) remains — already at 4.60:1.

### Audit methodology
Custom Python contrast checker resolves CSS `var()` chains within each variant, falls back to HA's known core color scale (from `src/resources/theme/color/core.globals.ts`), and computes WCAG-formula contrast ratios. Thresholds: 4.5:1 for normal text, 3:1 for interactive surfaces and large text.

13 critical token pairs checked per variant (primary text on card/popup/primary-bg, secondary text, sidebar text, sidebar selected, app-header, toast, filled-brand text on accent, tinted-brand text, state icon, sidebar icon). Almost all pairs scored 12:1 to 19:1 — well above AAA — with only the two findings above.

### Not changed
- Sunset filled-brand at 4.60:1 — passes, no action needed.
- Auto (experimental) — its `modes.light` block has its own light-mode tokens; audit was not extended into nested mode blocks (deferred to v1.3.x if needed).

## [1.2.7] - 2026-05-09

### Fixed
- **Bright blue (#009ac7) on filled brand buttons no longer clashes with theme palette.** "Bedingung hinzufügen" / "Aktion hinzufügen" / similar `ha-button[variant="brand"][appearance="filled"]` controls now use the theme's own accent colors (`--dark-primary-color` at rest/active, `--primary-color` on hover).

### Root cause
HA Frontend's `darkSemanticColorStyles` (in `src/resources/theme/color/semantic.globals.ts`) defines fill-primary tokens only for **`quiet`** and **`normal`** intensities — the **`loud`** variants (`fill-primary-loud-resting/hover/active`) are simply missing from the dark block. Browsers fall through to the light-mode defaults, which resolve to `--ha-color-primary-40 = #009ac7` (HA's stock bright blue). That bright blue collides with theme palettes that use a different accent (Sunset rose, Liquid Glass mid-blue, etc.).

### Added
Per dark variant (Liquid Glass, Compact, Sunset, Floorplan), nine override tokens:
- `ha-color-fill-primary-loud-resting/hover/active`
- `ha-color-fill-primary-normal-resting/hover/active`
- `ha-color-on-primary-quiet/normal/loud` (text color on primary surfaces)

Background tokens map to `var(--dark-primary-color)` (rest/active) or `var(--primary-color)` (hover); text tokens map to `var(--primary-text-color)` / `var(--text-primary-color)`. Per-variant palettes drive both background **and** legible text automatically — no hardcoded hex, no light-blue-on-light-blue.

Also added `--light-primary-color` and `--dark-primary-color` to **Compact** and **Floorplan** variants (were missing — both fell back to undefined behavior).

### Out of scope (deferred to v1.2.8)
A full WCAG AA contrast audit of all token combinations (4.5:1 text, 3:1 interactive surfaces). v1.2.7 fixes the most visible clash; the systematic audit comes next.

## [1.2.6] - 2026-05-08

### Fixed
- **Tooltips, dropdown popovers, action-add dialogs, active-filter pills, section titles** — all the remaining white-on-white spots reported after v1.2.5 (Verisure tooltip, Browser-Mod tooltip, language-picker dropdown, automation-trigger "Zu" popover, action-hinzufügen drop zone, integrations active-filters bar).
- **`wa-color-surface-raised` no longer semi-transparent** — the previous `rgba(20, 25, 40, 0.75)` value let the white body bleed through whenever a popover/dialog rendered on top. Now opaque (`#141928` dark, `#ffffff` light).

### Root cause (this time the actual one)

HA Frontend has a complete dark-mode token system (`darkSemanticColorStyles` + `darkColorStyles`) that automatically supplies dark values for **every** `--ha-color-fill-*-*-*`, `--ha-color-surface-*`, `--ha-color-form-*`, `--ha-color-text-*`, `--ha-color-border-*` token — but only when HA decides the theme is "dark".

How HA decides (from `themes-mixin.ts`):

```ts
if (!selectedTheme.modes || !("dark" in selectedTheme.modes)) {
  darkMode = false;          // ← without modes.dark, theme is forced LIGHT
} else if (!("light" in selectedTheme.modes)) {
  darkMode = true;            // ← only modes.dark, no modes.light → forced DARK
}
```

Our dark variants ("Liquid Glass", "Compact", "Sunset", "Floorplan") had **no `modes:` block at all** → HA forced `darkMode = false` → none of HA's dark tokens were ever loaded. That's why the v1.2.4 / v1.2.5 token guesswork only patched the most visible spots and never reached tooltips, dialog overlays, and active-filter pills.

### Added
- **`modes: dark: {}`** (empty, declarative) on every dark variant: Liquid Glass, Compact, Sunset, Floorplan.
- **`modes: light: {}`** on Light only.
- Auto (experimental) unchanged — its existing `modes.light` block is intentional (v1.1.2 "disable auto switching" decision).

### Side-effect bonus
HA also injects `<meta name="color-scheme" content="dark">` whenever `darkMode = true`. That sets the actual CSS `color-scheme` property browsers need for the `light-dark()` function — which means the **`light-dark()` border-color residue from v1.2.4 is fixed by this release too.** v1.3.0 (JS-loader) likely no longer required.

### Diagnostic credit
- DOM inspection on `<wa-input>`, `<ha-combo-box-item>`, `<ha-tooltip>`, `<ha-section-title>`, `<wa-dialog>`, `.active-filters` confirmed the missing token layers.
- Source-code analysis of HA frontend `dev` branch:
  - `src/state/themes-mixin.ts` (darkMode resolution logic)
  - `src/common/dom/apply_themes_on_element.ts` (theme rules merging + dark variables injection)
  - `src/resources/theme/color/semantic.globals.ts` (full `--ha-color-fill-*` / `--ha-color-surface-*` token definitions for both light and dark)
  - `src/resources/theme/color/color.globals.ts` (`darkColorStyles` triggers for `--primary-background-color`, `--card-background-color`)

### Cleanup deferred to v1.2.7
Many tokens added in v1.2.4 / v1.2.5 (`--mdc-*`, `--paper-*`, `--input-*`, `--wa-color-*`, the explicit `--ha-color-form-*` and `--md-sys-color-*` overrides) are now **redundant** because HA's dark variables cover them. Keeping them for one release as defense-in-depth; v1.2.7 will prune to the minimum required set.

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

[Unreleased]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.5.1...HEAD
[1.5.1]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.5.0...v1.5.1
[1.5.0]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.5.0-rc.1...v1.5.0
[1.5.0-rc.1]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.4.0...v1.5.0-rc.1
[1.4.0]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.3.0...v1.4.0
[1.3.0]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.2.8...v1.3.0
[1.2.8]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.2.7...v1.2.8
[1.2.7]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.2.6...v1.2.7
[1.2.6]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.2.5...v1.2.6
[1.2.5]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.2.4...v1.2.5
[1.2.4]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.2.3...v1.2.4
[1.2.3]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.2.2...v1.2.3
[1.2.2]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.2.1...v1.2.2
[1.2.1]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.2.0...v1.2.1
[1.2.0]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/studio-prisma/homeassistant-theme-liquid-glass/releases/tag/v1.0.0
