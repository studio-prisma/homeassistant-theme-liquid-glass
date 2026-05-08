# Liquid Glass — Home Assistant Theme

[![HACS Custom](https://img.shields.io/badge/HACS-Custom-orange.svg)](https://hacs.xyz/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![EN](https://img.shields.io/badge/Lang-EN-lightgrey.svg)](README.md)

Premium Glass-Morphism-Theme für Home Assistant — durchscheinende Oberflächen, sanfte Akzente, Dark UI. Sechs Varianten.

> Maintained by **studio-prisma**.

![Preview](docs/assets/screenshots/preview-main.svg)

## Varianten

| Theme-Name (HA Dropdown) | Verhalten |
|---|---|
| **Liquid Glass** ⭐ | **Standard — immer dunkel** mit `aurora.png` Hintergrund |
| **Liquid Glass Auto (experimental)** | OS-gesteuerter Light/Dark-Switch — bekannte HA-Limitierungen |
| **Liquid Glass Light only** | Immer hell — `dawn.png` Hintergrund |
| **Liquid Glass Compact** | Immer dunkel + tighter Spacing für Wall-Tablets |
| **Liquid Glass Sunset** | Immer dunkel + warme Rosa/Amber-Palette |
| **Liquid Glass Floorplan** | Immer dunkel + Heatmap-Glow für Picture-Element-Cards |

> ⚠️ **Warum ist "Auto" experimental?** HAs `modes:`-Block kann `lovelace-background` und einige Form-Komponenten (Sprache-Picker, Suchfelder) nicht zuverlässig zwischen Light/Dark umschalten. Für verlässliche Ergebnisse: feste Variante wählen. Für Auto-Switch nach Sonnenstand: Automation zwischen **Liquid Glass** und **Liquid Glass Light only** (siehe unten).

## Installation

### Schritt 1 — Theme via HACS

1. **HACS** → **Frontend** → 3-Punkte → **Custom repositories**
2. URL: `https://github.com/studio-prisma/homeassistant-theme-liquid-glass`
3. Kategorie: **Theme** → Add → installieren → HA neu starten

`configuration.yaml`:

```yaml
frontend:
  themes: !include_dir_merge_named themes/
```

### Schritt 2 — Hintergrundbilder einrichten (einmalig)

1. Ordner anlegen: `/config/www/liquid_glass/`
2. Alle vier PNGs aus [`docs/assets/backgrounds/`](docs/assets/backgrounds/) reinkopieren
3. **Developer Tools → YAML → Reload Themes**

### Schritt 3 — Aktivieren

**Profil → Theme → Liquid Glass** (Standard-Empfehlung).

## Auto-Switch — empfohlene Variante

Statt der experimental-Variante: HA-Automation, läuft zuverlässig:

```yaml
alias: Theme — Sonnenuntergang zu Dark
trigger:
  - platform: sun
    event: sunset
    offset: "-00:30:00"
action:
  - service: frontend.set_theme
    data:
      name: Liquid Glass

alias: Theme — Sonnenaufgang zu Light
trigger:
  - platform: sun
    event: sunrise
action:
  - service: frontend.set_theme
    data:
      name: Liquid Glass Light only
```

## Hintergrundbild wechseln (per Dashboard)

```yaml
title: Home
theme: Liquid Glass
background: 'center / cover no-repeat url("/local/liquid_glass/night.png") fixed'
```

## Eigene Bilder

1920×1200+, dunkel, ≤ 500 KB. In `/config/www/liquid_glass/` ablegen.

Quellen: [Unsplash](https://unsplash.com/), [Pexels](https://pexels.com/), [Pixabay](https://pixabay.com/), oder AI-Generatoren (Prompt: "premium dashboard background, deep blue ambient, soft gradient, minimal, 16:10").

## Getestet

HA Core 2026.5.0 · Frontend 20260429.3 · Supervisor 2026.04.2 · OS 17.3
Minimum: HA Core 2024.1.0.

## Snippets

- [`docs/demo-dashboard.yaml`](docs/demo-dashboard.yaml) — Showcase
- [`docs/card-mod-snippets.yaml`](docs/card-mod-snippets.yaml) — 9 Drop-in-Mods
- [`docs/floorplan-snippets.yaml`](docs/floorplan-snippets.yaml) — Picture-Element-Snippets

## Lizenz

MIT — siehe [LICENSE](LICENSE).
