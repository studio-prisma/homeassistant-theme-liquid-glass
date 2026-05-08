# Liquid Glass — Home Assistant Theme

[![HACS Custom](https://img.shields.io/badge/HACS-Custom-orange.svg)](https://hacs.xyz/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![HA](https://img.shields.io/badge/HA-2024.1.0%2B-blue.svg)]()
[![EN](https://img.shields.io/badge/Lang-EN-lightgrey.svg)](README.md)

Premium Glass-Morphism-Theme für Home Assistant — durchscheinende Oberflächen, sanfte Akzente, raffiniertes Dark UI. Sechs Varianten in einer Datei.

> Maintained by **studio-prisma**.

![Liquid Glass Dashboard Preview](docs/assets/screenshots/preview-main.svg)

## Varianten

| Theme-Name (HA Dropdown) | Verhalten |
|---|---|
| **Liquid Glass** | Auto-Switch via OS-Setting (Light/Dark) |
| **Liquid Glass Light only** | Immer hell — ignoriert OS |
| **Liquid Glass Dark only** | Immer dunkel — ignoriert OS |
| **Liquid Glass Compact** | Immer dunkel + tighter Spacing für Wall-Tablets |
| **Liquid Glass Sunset** | Immer dunkel + warme Rosa/Amber-Palette |
| **Liquid Glass Floorplan** | Immer dunkel + Heatmap-Glow für Picture-Element-Cards |

Auswahl in **Profil → Theme** oder per Dashboard via `theme: Liquid Glass Compact`.

## Features

- Glass-Morphism mit translucenten Surfaces und Blur
- Per-Domain-Status-Farben für Licht, Schalter, Klima, Cover, Lüfter, Media, Person, Lock, Vacuum
- **Per-Raum-Akzent-Tokens** (`room-living-rgb` etc.) — Cards je Raum unterschiedlich einfärben
- **Energy-Dashboard-Integration** — Verbrauch, Solar, Batterie, Gas, Wasser harmonisch gefärbt
- **Notification-Toasts** — System-Pop-Ups passen zum Theme
- **Sidebar-Refinement**, Mushroom-, Bubble-Card-Tokens
- Card-Mod-Variablen für Inline-Mods
- Drei Hintergrund-Optionen: Default-PNG + Dawn/Night/Calm-SVGs

## Getestet mit

- Home Assistant Core 2026.5.0
- Frontend 20260429.3
- Supervisor 2026.04.2 / OS 17.3

Mindestens HA Core 2024.1.0.

## Installation (HACS Custom Repository)

1. **HACS** → **Frontend** → 3-Punkte-Menü → **Custom repositories**
2. URL: `https://github.com/studio-prisma/homeassistant-theme-liquid-glass`
3. Kategorie: **Theme**
4. **Add** → **Liquid Glass Theme** auswählen → **Download**
5. Home Assistant neu starten
6. **Profil → Theme** → gewünschte Variante wählen

`configuration.yaml`:

```yaml
frontend:
  themes: !include_dir_merge_named themes/
```

## Hintergrundbild

Standard: `liquid_glass_bg.png` muss einmalig nach `/config/www/` kopiert werden. Dann sofort aktiv.

**Alternative Atmosphären** in `docs/assets/backgrounds/`:

| Datei | Stil |
|---|---|
| `dawn.svg` | Pastelliger Sonnenaufgang |
| `night.svg` | Tiefes Indigo + Sterne |
| `calm.svg` | Minimalistisches Türkis |

**Wechseln per Dashboard** (überlebt HACS-Updates):

```yaml
title: Home
theme: Liquid Glass
background: 'center / cover no-repeat url("/local/dawn.svg") fixed'
```

## Auto-Switch (OS-gesteuert)

Wähle **Liquid Glass** — folgt automatisch dem System-Setting (iOS/macOS/Windows Light/Dark). Hintergrundbild, Sidebar, Modal, Cards, Glass-Tokens — alles wird konsistent umgestellt.

Für **manuelle Steuerung** (z.B. nach Sonnenstand): Wähle `Liquid Glass Light only` oder `Liquid Glass Dark only` und nutze eine Automation:

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
```

## Demo Dashboard

`docs/demo-dashboard.yaml` — Generic Showcase mit Overview / Mushroom / Compact Views. Entitäts-IDs auf eigene anpassen.

## Card-mod-Snippets

`docs/card-mod-snippets.yaml` — neun Drop-in-Mods (Glass-Base, Status-Glow, Pulse, Toast, Per-Raum etc.). Setzt das `card-mod` HACS-Plugin voraus.

`docs/floorplan-snippets.yaml` — Picture-Element-Snippets für die Floorplan-Variante (Room-Marker, Heatmap, Warning-Pulse).

## Versionierung

[Semantic Versioning](https://semver.org/). Änderungen in [CHANGELOG.md](CHANGELOG.md) und [GitHub Releases](../../releases).

## Lizenz

MIT — siehe [LICENSE](LICENSE).
