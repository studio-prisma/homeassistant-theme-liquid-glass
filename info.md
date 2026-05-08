# Liquid Glass Theme

A premium glass-morphism theme for Home Assistant — translucent surfaces, soft accents, refined dark UI.

## Six variants

- **Liquid Glass** — auto-switch (colors only, no background image)
- **Liquid Glass Light only** — always light, with `dawn.png` background
- **Liquid Glass Dark only** — always dark, with `aurora.png` background
- **Liquid Glass Compact** — wall-tablets, dense layouts
- **Liquid Glass Sunset** — warm rose/amber palette
- **Liquid Glass Floorplan** — heatmap-glow for picture-element cards

## Setup

After install, restart HA. Then:

1. Create folder `/config/www/liquid_glass/`
2. Copy all PNGs from `docs/assets/backgrounds/` into it (`aurora`, `dawn`, `night`, `calm`)
3. Reload themes
4. **Profile → Theme** → select your variant

`configuration.yaml`:

```yaml
frontend:
  themes: !include_dir_merge_named themes/
```

## Tested

HA Core 2026.5.0 · Frontend 20260429.3 · Supervisor 2026.04.2 · OS 17.3

## Maintainer

[studio-prisma](https://github.com/studio-prisma).
