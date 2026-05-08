# Liquid Glass Theme

A premium glass-morphism theme for Home Assistant — translucent surfaces, soft accents, and a refined dark UI.

## Variants

Three variants are bundled — switch in **Profile → Theme**:

- **Liquid Glass** — default dark
- **Liquid Glass Light** — daytime
- **Liquid Glass Compact** — wall-tablets, dense layouts

## Activation

After installation, restart Home Assistant, then go to **Profile** → **Theme** → select your variant.

Make sure your `configuration.yaml` includes:

```yaml
frontend:
  themes: !include_dir_merge_named themes/
```

## Optional Background Image

A preset background image is included in the repo (`docs/assets/liquid_glass_bg.png`). Copy it into `/config/www/` and uncomment the `lovelace-background` line in `themes/liquid_glass.yaml`.

## Tested With

HA Core 2026.5.0 · Frontend 20260429.3 · Supervisor 2026.04.2 · OS 17.3

## Maintainer

Maintained by [studio-prisma](https://github.com/studio-prisma).
