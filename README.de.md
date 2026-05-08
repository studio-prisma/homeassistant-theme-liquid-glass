# Liquid Glass — Home Assistant Theme

[![HACS Custom](https://img.shields.io/badge/HACS-Custom-orange.svg)](https://hacs.xyz/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![HA](https://img.shields.io/badge/HA-2024.1.0%2B-blue.svg)]()
[![EN](https://img.shields.io/badge/Lang-EN-lightgrey.svg)](README.md)

Premium Glass-Morphism-Theme für Home Assistant — durchscheinende Oberflächen, sanfte Akzente, Dark UI. Sechs Varianten in einer Datei.

> Maintained by **studio-prisma**.

![Liquid Glass Dashboard Preview](docs/assets/screenshots/preview-main.svg)

## Varianten

| Theme-Name (HA Dropdown) | Verhalten |
|---|---|
| **Liquid Glass** | Auto-Switch via OS — nur Farben (kein Hintergrundbild) |
| **Liquid Glass Light only** | Immer hell — `dawn.png` als Hintergrund |
| **Liquid Glass Dark only** | Immer dunkel — `aurora.png` als Hintergrund |
| **Liquid Glass Compact** | Immer dunkel + tighter Spacing für Wall-Tablets |
| **Liquid Glass Sunset** | Immer dunkel + warme Rosa/Amber-Palette — `dawn.png` |
| **Liquid Glass Floorplan** | Immer dunkel + Heatmap-Glow für Picture-Element-Cards |

> **Warum hat Auto-Switch kein Hintergrundbild?** Das HA `modes:`-Block kann die `lovelace-background`-Variable nicht zuverlässig zwischen Light/Dark umschalten. Wenn du Light/Dark mit jeweils eigenem Hintergrund willst, nutze eine Automation die zwischen **Light only** und **Dark only** wechselt (siehe Auto-Switch-Strategie unten).

## Installation

### Schritt 1 — Theme via HACS Custom Repository

1. **HACS** → **Frontend** → 3-Punkte-Menü → **Custom repositories**
2. URL: `https://github.com/studio-prisma/homeassistant-theme-liquid-glass`
3. Kategorie: **Theme** → **Add** → Liquid Glass installieren → HA neu starten

`configuration.yaml`:

```yaml
frontend:
  themes: !include_dir_merge_named themes/
```

### Schritt 2 — Hintergrundbilder einrichten (einmalig)

Theme erwartet Bilder unter `/local/liquid_glass/`:

1. Ordner anlegen: `/config/www/liquid_glass/`
2. Alle vier PNGs aus [`docs/assets/backgrounds/`](docs/assets/backgrounds/) reinkopieren:
   - `aurora.png` (Dark only, Compact, Floorplan)
   - `dawn.png` (Light only, Sunset)
   - `night.png` (Alternative)
   - `calm.png` (Alternative)
3. **Developer Tools → YAML → Reload Themes**

Fehlt ein Bild → Fallback auf Solid-Color, kein Crash.

### Schritt 3 — Theme aktivieren

**Profil → Theme** → gewünschte Variante.

## Hintergrundbild wechseln

**Per Dashboard (überlebt HACS-Updates):**

```yaml
title: Home
theme: Liquid Glass Dark only
background: 'center / cover no-repeat url("/local/liquid_glass/night.png") fixed'
views:
  - title: Overview
```

## Eigene Bilder

Jedes 1920×1200+ PNG/JPG funktioniert. In `/config/www/liquid_glass/` ablegen und über Dashboard-Background oder im Theme referenzieren.

**Lizenzfreie Quellen:**
- [Unsplash](https://unsplash.com/) — hochwertige Fotografie
- [Pexels](https://pexels.com/) — breite Bibliothek
- [Pixabay](https://pixabay.com/) — Fotos + Vektoren
- AI-Generatoren: Midjourney, DALL-E — Prompt: "premium dashboard background, deep blue ambient, soft gradient, minimal, 16:10"

Ziel: dunkel, kontrastarm, ≤ 500 KB. Reichhaltige Fotos lenken vom Inhalt ab.

## Auto-Switch zwischen Light/Dark

**Variante A — `Liquid Glass`** (eingebaut, nur Farben)
Sidebar, Cards, Dialoge folgen OS. Bild bleibt das Default-Bild.

**Variante B — Automation zwischen Light only / Dark only** (volle Abdeckung)

```yaml
alias: Theme — Sonnenuntergang zu Dark
trigger:
  - platform: sun
    event: sunset
    offset: "-00:30:00"
action:
  - service: frontend.set_theme
    data:
      name: Liquid Glass Dark only

alias: Theme — Sonnenaufgang zu Light
trigger:
  - platform: sun
    event: sunrise
action:
  - service: frontend.set_theme
    data:
      name: Liquid Glass Light only
```

Variante B = volle Light/Dark-Trennung inkl. Hintergrundbild.

## Getestet mit

HA Core 2026.5.0 · Frontend 20260429.3 · Supervisor 2026.04.2 · OS 17.3
Minimum: HA Core 2024.1.0.

## Demo Dashboard & Snippets

- [`docs/demo-dashboard.yaml`](docs/demo-dashboard.yaml) — Showcase
- [`docs/card-mod-snippets.yaml`](docs/card-mod-snippets.yaml) — 9 Drop-in-Mods
- [`docs/floorplan-snippets.yaml`](docs/floorplan-snippets.yaml) — Picture-Element-Snippets

## Lizenz

MIT — siehe [LICENSE](LICENSE).
