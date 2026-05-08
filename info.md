# Liquid Glass Theme

A premium glass-morphism theme for Home Assistant — translucent surfaces, soft accents, refined dark UI.

## Six variants

- **Liquid Glass** — auto-switches with OS (Light/Dark)
- **Liquid Glass Light only** — always light
- **Liquid Glass Dark only** — always dark
- **Liquid Glass Compact** — wall-tablets, dense layouts
- **Liquid Glass Sunset** — warm rose/amber palette
- **Liquid Glass Floorplan** — heatmap-glow for picture-element cards

## Activation

After install, restart HA → **Profile → Theme** → select your variant.

`configuration.yaml`:

```yaml
frontend:
  themes: !include_dir_merge_named themes/
```

## Optional Background

Copy `docs/assets/liquid_glass_bg.png` (or any SVG from `docs/assets/backgrounds/`) into your `/config/www/` folder. Theme uses it automatically.

## Tested

HA Core 2026.5.0 · Frontend 20260429.3 · Supervisor 2026.04.2 · OS 17.3

## Maintainer

[studio-prisma](https://github.com/studio-prisma).
