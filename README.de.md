# Liquid Glass — Home Assistant Theme

[![HACS Custom](https://img.shields.io/badge/HACS-Custom-orange.svg)](https://hacs.xyz/)
[![Min HA Version](https://img.shields.io/badge/HA-2024.1.0%2B-blue.svg)](https://www.home-assistant.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![English](https://img.shields.io/badge/Lang-English-lightgrey.svg)](README.md)

Premium Glass-Morphism-Theme für Home Assistant — durchscheinende Oberflächen, geschichteter Blur, sanfte Akzente, Dark UI. Sechs Varianten in einer Datei.

> Maintained by **studio-prisma**.

![Liquid Glass — Welcome Home Dashboard](docs/assets/screenshots/preview-welcome.png)

> 🎯 **Echtes Plug-and-Play (seit v1.4.0).** Über HACS installieren → Theme aktivieren → fertig. Jede Karte erhält automatisch den vollen Glass-Morphism-Look — durchscheinende Oberfläche, Backdrop-Blur, feine Border, Glas-Schatten, harmonisierte Pro-Domain-Statusfarben, WCAG-AA-konformer Text. Kein Per-Card-Snippet mehr nötig. Mushroom und Bubble Card werden unterstützt; Pop-ups bleiben intakt dank des Upstream-Fix in [Bubble Card Issue #2347](https://github.com/Clooos/Bubble-Card/issues/2347). Voraussetzungen: `card-mod` einmalig via HACS installieren und Bubble Card auf dem aktuellen offiziellen Release. Details: [Was du out-of-the-box bekommst](#was-du-out-of-the-box-bekommst).

## Varianten

| Theme-Name (HA-Dropdown) | Verhalten |
|---|---|
| **Liquid Glass** ⭐ | **Standard — immer dunkel** mit `aurora.png`-Hintergrund. Empfohlen. |
| **Liquid Glass Auto (experimental)** | OS-gesteuerter Light/Dark-Switch — bekannte HA-Limitierungen (siehe Hinweis) |
| **Liquid Glass Light only** | Immer hell, ignoriert OS — `dawn.png`-Hintergrund |
| **Liquid Glass Compact** | Immer dunkel + tighter Spacing für Wall-Tablets |
| **Liquid Glass Sunset** | Immer dunkel + warme Rosa/Amber-Palette |
| **Liquid Glass Floorplan** | Immer dunkel + Heatmap-Glow für Picture-Element-Karten |

> ⚠️ **Warum ist "Auto" experimental?** HAs `modes:`-Block überschreibt die `lovelace-background`-CSS-Variable nicht zuverlässig, und einige Form/Dropdown-Komponenten (Suchfelder, Sprache-Picker) rendern mit nicht-passenden Farben. Die Auto-Variante ist Best-Effort. Für konsistente Ergebnisse: feste Variante wählen.

Auswählen unter **Profil → Theme** oder pro Dashboard via `theme: Liquid Glass Compact`.

## Übersicht — Lichter, Medien, Schalter

![Übersichts-View mit Mushroom-Karten, Staubsauger, Media Players und Switch-Tiles](docs/assets/screenshots/preview-overview.png)

> *Standard-Tile-, Thermostat-, Area- und Mushroom-Karten — alle seit v1.4.0 automatisch mit vollem Glas-Look. Keine Per-Card-Snippets nötig.*

## Home-Security-View

![Security-View mit Tür-Sensoren, Kameras und Anwesenheits-Tiles](docs/assets/screenshots/preview-security.png)

> *Die Tile-Karten in dieser View rendern out-of-the-box mit dem vollen Glas-Effekt; das Picture-Element-Kamera-Grid nutzt die Floorplan-Varianten-Tokens.*

## Features

- Glass-Morphism mit gestaffelten transparenten Oberflächen und Blur
- Pro-Domain-Statusfarben: light, switch, climate, cover, fan, media_player, person, lock, vacuum
- **Per-Room-Accent-Tokens** (`room-living-rgb`, ...) — Karten pro Bereich einfärben
- **Energy-Dashboard-Integration** — Grid, Solar, Batterie, Gas, Wasser harmonisiert
- **Notification-Toast-Styling** — System-Pop-ups passen sich dem Theme an
- **Form-Field- & Dropdown-Styling** — Sprache-Picker, Suchfelder, Selects, Alarmcode-Input, Time-Picker, Tooltips, Dialog-Popovers rendern alle korrekt im Dark Mode
- Sidebar-Refinement, Mushroom- & Bubble-Card-Tokens
- **Globale `card-mod-card`-Regel** (seit v1.4.0) — jede Karte erhält automatisch den vollen Glass-Morphism-Look; kein Per-Card-Snippet nötig
- **Background-Pack** — vier PNGs (Aurora, Dawn, Night, Calm)

## Was du out-of-the-box bekommst

Seit v1.4.0 liefert das Theme eine globale `card-mod-card`-Regel (eine pro Variante), die den vollen Glass-Morphism-Look — durchscheinende Oberfläche, `backdrop-filter`-Blur, feine Border, Glas-Schatten — automatisch auf jedes `ha-card` anwendet. Einfach Theme installieren und aktivieren.

| Karten-Familie | Look out-of-the-box |
|---|---|
| **Tile / Thermostat / Area / Entities / Glance / Button** | Voller Glas-Look: durchscheinende Oberfläche + Backdrop-Blur + feine Border + Hover-Glow |
| **Mushroom** | Mushrooms eigener Blur via `--mush-*`-Tokens + Theme-Transparenz |
| **Bubble Card** | Theme-Tokens werden angewendet; Pop-ups bleiben intakt (rendern seit dem Upstream-Fix außerhalb des `ha-card`-Trees) |
| **picture-elements (Floorplan-Variante)** | Heatmap-Glow-Tokens via `--floorplan-*` |

### Warum v1.4.0 — und was sich geändert hat

Frühere Releases haben den Glas-Effekt als Per-Card-Opt-in (`glass_card_base`-Snippet) ausgeliefert, weil ein global angewendetes `backdrop-filter: blur(...)` auf `ha-card` Bubble-Card-v3-Pop-ups gebrochen hat ([Bubble Card Issue #2347](https://github.com/Clooos/Bubble-Card/issues/2347)). Der Upstream-Fix (post-v3.2.0-beta4) verschiebt Bubble-Card-Pop-ups aus dem `ha-card`-Tree heraus — eine globale Regel betrifft sie nicht mehr. v1.4.0 liefert diese globale Regel als Default.

### Voraussetzungen

- [`card-mod`](https://github.com/thomasloven/lovelace-card-mod) via HACS installiert — Pflicht für jede Liquid Glass v1.4.0+-Installation, weil die globale Regel via `card-mod-theme`-Mechanik ausgeliefert wird.
- **Bubble Card auf dem aktuellen offiziellen Release** (alles ab v3.2.0-beta4 enthält den Fix). Ältere Bubble-Card-Versionen rendern Pop-ups leer unter einem globalen Blur — das ist Upstream-gefixt, kein Theme-Bug.

### Pro Karte überschreiben?

`card_mod` direkt auf der Karte setzt die globale Regel außer Kraft, oder eines der Snippets in [`docs/card-mod-snippets.yaml`](docs/card-mod-snippets.yaml) nutzen — alle verwenden dieselben `--glass-*`-Tokens, Overrides bleiben farblich konsistent.


## Getestet mit

- Home Assistant Core 2026.5.0
- Frontend 20260509.x (WebAwesome + Material Web 3 Komponenten)
- Supervisor 2026.05.0 / OS 17.3
- Browser: Chrome/Firefox/Safari/Edge Desktop, iOS Companion App

Mindestens unterstützt: **Core 2024.1.0**. WCAG-AA-Kontrast für alle Varianten verifiziert (v1.2.8 + v1.3.0 für Auto).

## Installation

### Schritt 1 — Theme via HACS

1. **HACS** → **Frontend** → 3-Punkte-Menü → **Custom repositories**
2. URL: `https://github.com/studio-prisma/homeassistant-theme-liquid-glass`
3. Kategorie: **Theme** → **Add** → installieren → HA neu starten

`configuration.yaml`:

```yaml
frontend:
  themes: !include_dir_merge_named themes/
```

### Schritt 2 — Hintergrundbilder einrichten (einmalig)

1. Ordner anlegen: `/config/www/liquid_glass/`
2. Alle vier PNGs aus [`docs/assets/backgrounds/`](docs/assets/backgrounds/) reinkopieren
3. Entwicklerwerkzeuge → YAML → **Themes neu laden**

### Schritt 3 — Aktivieren

**Profil → Theme → Liquid Glass** (Standard-Empfehlung).

## Auto-Switch-Strategie (empfohlen)

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

Vollständige Light/Dark-Übergänge inklusive Hintergründe, ohne Überraschungen.

## Demo-Dashboard

[`docs/demo-dashboard.yaml`](docs/demo-dashboard.yaml) — generischer Showcase mit Platzhalter-Entity-IDs. Anpassen an dein Setup.

## Optional: Card-mod-Snippets

> ℹ️ **`card-mod` ist jetzt Pflicht** (seit v1.4.0 — für die globale Glas-Regel). Die folgenden Dateien sind **Opt-in-Extras** darüber hinaus: Per-Card-Overrides, Glow-Effekte, Per-Room-Akzente, Mushroom-Polish.

Snippet-Bibliotheken:

- [`docs/card-mod-snippets.yaml`](docs/card-mod-snippets.yaml) — zwölf Drop-in-Mods (`glass_card_base` ist jetzt im Theme gebündelt; das Snippet bleibt als Copy-Paste-Template für Per-Card-Overrides)
- [`docs/floorplan-snippets.yaml`](docs/floorplan-snippets.yaml) — Picture-Element-Snippets

## Anpassung

### Basis-Farben überschreiben

```yaml
Liquid Glass:
  primary-color: "#ff7a8a"
  accent-color: "#7af5b8"
```

### Per-Room-Accent-Tokens

Jede Variante liefert acht Raum-Tokens als RGB-Triplets — ready-to-use für `rgb()` / `rgba()`, um Karten pro Bereich einzufärben.

| Token | Default (Liquid Glass) | Vorgeschlagener Bereich |
|---|---|---|
| `--room-living-rgb` | `255, 180, 84` (Amber) | Wohnzimmer |
| `--room-bedroom-rgb` | `157, 130, 230` (Lavendel) | Schlafzimmer |
| `--room-office-rgb` | `122, 184, 255` (Sky Blue) | Büro / Arbeitsplatz |
| `--room-kitchen-rgb` | `255, 139, 74` (Coral) | Küche |
| `--room-bathroom-rgb` | `100, 220, 220` (Teal) | Bad |
| `--room-garden-rgb` | `74, 210, 149` (Mint) | Garten / Outdoor |
| `--room-garage-rgb` | `120, 120, 130` (Graphit) | Garage / Werk |
| `--room-workshop-rgb` | `255, 200, 100` (warmes Gold) | Werkstatt / Hobby |

**Theme-only-Nutzung (kein Plugin nötig):** Die Tokens sind bereits in den Pro-Domain-Farben verdrahtet.

**Optional — Per-Card-Override via card-mod** (benötigt das card-mod-Plugin):

```yaml
type: tile
entity: light.wohnzimmer_main
card_mod:
  style: |
    ha-card {
      background: rgba(var(--room-living-rgb), 0.18);
      border-left: 3px solid rgb(var(--room-living-rgb));
    }
```

**Global überschreiben (pro Theme, kein Plugin):**

```yaml
Liquid Glass:
  room-living-rgb: "210, 90, 130"
  room-office-rgb: "90, 200, 170"
```

## Architektur — Token-Layer

HAs Frontend hat über die Zeit mehrere CSS-Token-Generationen angesammelt. Ein Theme, das auf einer modernen HA-Installation korrekt rendern soll, muss alle abdecken.

| Layer | Genutzt von | Generation |
|---|---|---|
| `--mdc-*` | Legacy Material Design Components | HA ≤ 2023 |
| `--paper-*` | Polymer-Inputs | HA ≤ 2022 |
| `--input-*`, `--mwc-*` | HA-Aliases der obigen | Bridge-Layer |
| `--wa-color-*` | WebAwesome (Shoelace-Fork) — moderne Form-Controls | HA 2025+ |
| `--ha-color-*`, `--ha-color-fill-*-*-*`, `--ha-color-surface-*` | HAs eigenes Semantik-Token-System | HA 2025+ |
| `--md-sys-color-*` | Material Web 3 — Combo-Boxen, Dialoge | HA 2025+ |

### Wie `modes:` den Dark Mode aktiviert

HAs Resolver lädt `darkSemanticColorStyles` + `darkColorStyles` nur, wenn das Theme einen `modes:`-Block deklariert. Jede dunkle Variante deklariert ein leeres `modes: dark: {}`, um den Load zu triggern.

### Bekannte Limitierungen

- **Auto (experimental)** — `modes.light`-Block voll für OS-gesteuertes Switching, `modes.dark` bewusst nicht deklariert. Für verlässlichen Light/Dark-Wechsel: Automation-Pattern aus dem Auto-Switch-Abschnitt nutzen.
- **WCAG-AA-Audit** — Alle Varianten auditiert: Top-Level + Auto `modes.light`. **13/13 Paare bestehen** (3.78:1 bis 17.18:1) seit v1.3.0.

### Issues diagnostizieren

DevTools → Elements → `#shadow-root`-Ketten aufklappen → Computed-Tab → CSS-Variable identifizieren. Issue-Templates in [`CONTRIBUTING.md`](CONTRIBUTING.md).

## Versionierung

[Semantic Versioning](https://semver.org/). Siehe [`CHANGELOG.md`](CHANGELOG.md).

## Beitragen

Siehe [`CONTRIBUTING.md`](CONTRIBUTING.md).

## Credits

- Designed & maintained by **studio-prisma**
- Mushroom- & Bubble-Card-Token-Kompatibilität sichergestellt

## FAQ

### Brauche ich card-mod für jede Karte?

Nein. `card-mod` muss einmalig via HACS installiert sein — aber du fügst pro Karte nichts hinzu. Seit v1.4.0 liefert das Theme eine globale `card-mod-card`-Regel, die den vollen Glas-Look automatisch auf jedes `ha-card` anwendet. Per-Card-Overrides bleiben möglich für Custom-Looks; siehe [`docs/card-mod-snippets.yaml`](docs/card-mod-snippets.yaml).

### Warum haben meine Tile- / Thermostat- / Area-Karten nicht den gleichen Blur wie in den Screenshots?

Sollten sie — seit v1.4.0 wird der volle Glas-Effekt global angewendet. Falls du ihn nicht siehst, prüfe: (1) ist `card-mod` via HACS installiert? (2) ist Bubble Card auf dem aktuellen offiziellen Release (post-v3.2.0-beta4)? (3) ist Dashboard-Edit-Mode aus? (4) Browser-Cache geleert? Falls alle Punkte ✓ und der Look fehlt weiterhin, Issue mit DOM-Inspect-Screenshot öffnen. Setup-Details: [Was du out-of-the-box bekommst](#was-du-out-of-the-box-bekommst).

### Muss ich YAML editieren, um das Theme zu nutzen?

Nein. Der einzige manuelle Schritt ist, die vier Hintergrund-PNGs in `/config/www/liquid_glass/` zu kopieren (einmaliges Setup). Alles andere funktioniert automatisch.

### Welche Dashboard-Karten sind in den Screenshots zu sehen?

Standard- + populäre Community-Karten: Lovelace-Tile, [Mushroom](https://github.com/piitaya/lovelace-mushroom), [mini-graph-card](https://github.com/kalkih/mini-graph-card), [mini-media-player](https://github.com/kalkih/mini-media-player), [vacuum-card](https://github.com/denysdovhan/vacuum-card). Seit v1.4.0 erhält jede sichtbare Karte — auch Standard-Tile — automatisch den vollen Glas-Look. Mushroom- und mini-graph-Karten layern ihren eigenen Blur on top. Referenz-Dashboard mit Platzhalter-Entity-IDs: [`docs/demo-dashboard.yaml`](docs/demo-dashboard.yaml).

### Was ist in `themes/liquid_glass.yaml`?

Eine ~1250-zeilige YAML-Datei mit sechs Theme-Varianten. Du musst sie nicht öffnen oder editieren — HACS installiert sie, HA lädt sie automatisch.

### Warum werden die Hintergründe nicht automatisch installiert?

HACS kann Theme-YAML ausliefern, aber nicht in `/config/www/` schreiben. Lovelace referenziert Bilder per URL-Pfad — die vier PNGs müssen also einmalig in den `www/`-Ordner deiner Config.

### Etwas sieht falsch aus / Kontrast stimmt nicht / ein Popup ist Weiß-auf-Weiß

Issue öffnen mit: HA-Core-Version, Browser, betroffenes Element (DevTools-Screenshot der computed CSS-Variable). Der Abschnitt "Issues diagnostizieren" oben führt durch.

## Lizenz

MIT — siehe [LICENSE](LICENSE).
