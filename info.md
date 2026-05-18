# Liquid Glass Theme

A premium glass-morphism theme for Home Assistant — translucent surfaces, soft accents, refined dark UI.

> 🎯 **True plug-and-play (since v1.4.0).** Install via HACS → activate the theme → done. Every Lovelace card automatically renders with the full glass-morphism look — translucent surface, backdrop blur, soft border, glass-grade shadow, WCAG-AA-compliant text. Prerequisites: `card-mod` installed via HACS (one-time, the global glass rule rides on top of card-mod's `card-mod-theme` mechanism) and Bubble Card on the current official release. Mushroom and Bubble Card are supported; pop-ups remain intact thanks to the upstream fix in Bubble Card issue #2347 (post-v3.2.0-beta4).

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
