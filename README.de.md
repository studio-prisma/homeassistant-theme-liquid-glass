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

HA Core 2026.5.0 · Frontend 20260509.x · Supervisor 2026.05.0 · OS 17.3
Browser: Chrome/Firefox/Safari/Edge Desktop, iOS Companion App
WCAG AA Kontrast verifiziert für alle Dark-Varianten (Audit in v1.2.8).
Minimum: HA Core 2024.1.0.

## Architektur — Token-Layer

HAs Frontend hat über die Jahre mehrere CSS-Token-Generationen angesammelt. Ein Theme, das auf modernen HA-Installationen sauber rendert, muss alle abdecken — daher die Größe der YAML.

| Layer | Genutzt von | Generation |
|---|---|---|
| `--mdc-*` | Legacy Material Design Components | HA ≤ 2023 |
| `--paper-*` | Polymer-Inputs | HA ≤ 2022 |
| `--input-*`, `--mwc-*` | HA-Aliases der obigen | Bridge-Layer |
| `--wa-color-*` | WebAwesome (Shoelace-Fork) — moderne Form-Controls | HA 2025+ |
| `--ha-color-*`, `--ha-color-fill-*-*-*`, `--ha-color-surface-*` | HA's eigenes Semantik-Token-System | HA 2025+ |
| `--md-sys-color-*`, `--md-list-item-*` | Material Web 3 — Combo-Boxen, Dialoge, List-Items | HA 2025+ |

### Wie `modes:` den Dark-Mode aktiviert

HAs Resolver (`src/state/themes-mixin.ts`) lädt `darkSemanticColorStyles` + `darkColorStyles` nur, wenn das Theme einen `modes:`-Block deklariert. Jede dunkle Variante in diesem Theme deklariert ein leeres `modes: dark: {}`, um diesen Load zu triggern — dadurch rendern Tooltips, Dropdown-Popovers, Dialog-Hintergründe und Active-Filter-Pills automatisch dunkel, ohne dass wir jeden Token einzeln aufzählen müssen.

Nebeneffekt: HA injiziert dann auch `<meta name="color-scheme" content="dark">`, was Browsern die echte CSS-`color-scheme`-Property gibt — die wiederum Native `<input type="time">` und `<input type="number">` (Alarm-Code, Time-Picker) korrekt rendern lässt.

### Bekannte Limitierungen

- **Auto (experimental)** — der `modes.light`-Block ist voll für OS-gesteuertes Switching, aber `modes.dark` ist bewusst nicht deklariert (Legacy-Entscheidung aus v1.1.2 zur Deaktivierung von HA's Auto-Switch). Für verlässlichen Light/Dark-Wechsel: Automation-Pattern aus dem [Auto-Switch-Abschnitt](#auto-switch--empfohlene-variante) nutzen.
- **WCAG AA-Audit-Scope** — alle Top-Level-Varianten geprüft. Auto's verschachtelter `modes.light`-Block wurde in v1.2.8 nicht token-by-token auditiert (deferred — überlappt stark mit Light-only, das geprüft wurde).

### Issues diagnostizieren

DevTools → Elements → `#shadow-root`-Ketten aufklappen → Computed-Tab → CSS-Variable identifizieren, die die falsche Farbe resolved. Issue-Templates in [`CONTRIBUTING.md`](CONTRIBUTING.md) führen durch das Format.

## Snippets

- [`docs/demo-dashboard.yaml`](docs/demo-dashboard.yaml) — Showcase
- [`docs/card-mod-snippets.yaml`](docs/card-mod-snippets.yaml) — 9 Drop-in-Mods
- [`docs/floorplan-snippets.yaml`](docs/floorplan-snippets.yaml) — Picture-Element-Snippets

## Lizenz

MIT — siehe [LICENSE](LICENSE).
