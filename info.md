# Liquid Glass Theme

A premium glass-morphism theme for Home Assistant — translucent surfaces, soft accents, refined dark UI.

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

HA Core 2026.5.0 · Frontend 20260429.3 · Supervisor 2026.04.2 · OS 17.3

## Maintainer

[studio-prisma](https://github.com/studio-prisma).
