# Liquid Glass Theme

A premium glass-morphism theme for Home Assistant — translucent surfaces, soft accents, refined dark UI.

> 🎯 **Plug-and-play, with two effect tiers.** Install via HACS → activate the theme → done. **Tier 1** (automatic, no card-mod): every Lovelace card inherits the Liquid Glass color tokens — translucent dark surface, rounded corners, refined borders, WCAG-AA-compliant text. **Tier 2** (opt-in, card-mod required): the full backdrop blur seen in the screenshots — added per card via a single drop-in `glass_card_base` snippet from `docs/card-mod-snippets.yaml`. The split is deliberate to preserve Bubble Card v3 pop-up compatibility (a global `ha-card` blur is known to break those). Full details and snippet in the README "Effect Tiers" section.

## Six variants

- **Liquid Glass** ⭐ — default, always dark with aurora.png background
- **Liquid Glass Auto (experimental)** — OS-driven, known limitations
- **Liquid Glass Light only** — always light
- **Liquid Glass Compact** — wall-tablets, dense layouts
- **Liquid Glass Sunset** — warm rose/amber palette
- **Liquid Glass Floorplan** — heatmap-glow for picture-element cards

## Setup

After install, restart HA. Then:

1. Create folder `/config/www/liquid_glass/`
2. Copy all PNGs from `docs/assets/backgrounds/` into it (`aurora`, `dawn`, `night`, `calm`)
3. Reload themes
4. **Profile → Theme → Liquid Glass**

`configuration.yaml`:

```yaml
frontend:
  themes: !include_dir_merge_named themes/
```

## Tested

HA Core 2026.5.0 · Frontend 20260509.x · Supervisor 2026.05.0 · OS 17.3
Minimum supported: Core 2024.1.0.

## Maintainer

[studio-prisma](https://github.com/studio-prisma)
