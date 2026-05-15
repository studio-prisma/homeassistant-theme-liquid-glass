# Liquid Glass — Home Assistant Theme

[![HACS Custom](https://img.shields.io/badge/HACS-Custom-orange.svg)](https://hacs.xyz/)
[![Min HA Version](https://img.shields.io/badge/HA-2024.1.0%2B-blue.svg)](https://www.home-assistant.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![English](https://img.shields.io/badge/Lang-English-lightgrey.svg)](README.md)

Premium Glass-Morphism-Theme für Home Assistant — durchscheinende Oberflächen, geschichteter Blur, sanfte Akzente, Dark UI. Sechs Varianten in einer Datei.

> Maintained by **studio-prisma**.

![Liquid Glass — Welcome Home Dashboard](docs/assets/screenshots/preview-welcome.png)

> 🎯 **Plug-and-play, mit zwei Effekt-Tiers.** Über HACS installieren → Theme aktivieren → fertig. **Tier 1** (automatisch, kein card-mod): jede Karte erbt die Liquid-Glass-Color-Tokens — durchscheinende dunkle Oberfläche, abgerundete Ecken, feine Borders, harmonisierte Pro-Domain-Statusfarben, WCAG-AA-konformer Text. **Tier 2** (Opt-in, card-mod nötig): der volle Glass-Morphism-Backdrop-Blur wie in den Screenshots — pro Karte per einzeiligem Drop-in-Snippet. Der Tier-2-Split ist Absicht: ein globaler Blur auf `ha-card` ist bekannt dafür, Bubble-Card-v3-Pop-ups zu brechen, deshalb liefern wir ihn als expliziten Opt-in. Siehe [Effekt-Tiers](#effekt-tiers--was-das-theme-automatisch-liefert-vs-opt-in) unten für die Tabelle und das Copy-Paste-Snippet, oder direkt zur [FAQ](#faq).

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

> *Screenshot-Komposition: Mushroom-Karten bringen ihren eigenen Blur über `--mush-control-*`-Tokens mit (kein card-mod nötig); Standard-Tile-/Thermostat-Karten in der unteren Hälfte nutzen das [Tier-2-Snippet](#effekt-tiers--was-das-theme-automatisch-liefert-vs-opt-in), um die umgebende Ästhetik zu treffen. Ohne Tier-2-Snippet rendern sie mit reiner Tier-1-Token-Transparenz.*

## Home-Security-View

![Security-View mit Tür-Sensoren, Kameras und Anwesenheits-Tiles](docs/assets/screenshots/preview-security.png)

> *Die Tile-Karten in dieser View nutzen das Tier-2-`glass_card_base`-Snippet; das Picture-Element-Kamera-Grid nutzt die Floorplan-Varianten-Tokens direkt.*

## Features

- Glass-Morphism mit gestaffelten transparenten Oberflächen und Blur
- Pro-Domain-Statusfarben: light, switch, climate, cover, fan, media_player, person, lock, vacuum
- **Per-Room-Accent-Tokens** (`room-living-rgb`, ...) — Karten pro Bereich einfärben
- **Energy-Dashboard-Integration** — Grid, Solar, Batterie, Gas, Wasser harmonisiert
- **Notification-Toast-Styling** — System-Pop-ups passen sich dem Theme an
- **Form-Field- & Dropdown-Styling** — Sprache-Picker, Suchfelder, Selects, Alarmcode-Input, Time-Picker, Tooltips, Dialog-Popovers rendern alle korrekt im Dark Mode
- Sidebar-Refinement, Mushroom- & Bubble-Card-Tokens
- Card-Mod-Globale-Variablen
- **Background-Pack** — vier PNGs (Aurora, Dawn, Night, Calm)

## Effekt-Tiers — was das Theme automatisch liefert vs. Opt-in

Das Theme liefert zwei Effekt-Schichten. Tier 1 ist automatisch; Tier 2 ist ein einzeiliger card-mod-Opt-in.

| Karten-Familie | Tier 1 — automatisch (kein Plugin) | Tier 2 — `glass_card_base`-Snippet (card-mod) |
|---|---|---|
| **Tile** | dunkler transparenter Hintergrund, abgerundet, feine Border, Theme-Text | + voller `backdrop-filter`-Blur, Hover-Glow, Glas-Schatten |
| **Thermostat** | dunkler transparenter Hintergrund, abgerundet, Theme-Accent | + voller Blur, Hover-Glow |
| **Area** | dunkler transparenter Hintergrund, Theme-Tokens | + voller Blur, feine Border, Hover-Glow |
| **Entities / Glance / Button** | dunkler transparenter Hintergrund, Theme-Tokens | + voller Blur, Hover-Glow |
| **Mushroom** | dunkler transparenter Hintergrund + eigener Blur via `--mush-*`-Tokens (sieht bereits "full glass" aus) | weitere Feinheiten via `mushroom_glass`-Snippet |
| **Bubble Card** | dunkler transparenter Hintergrund via Theme-Tokens, Pop-ups intakt | nur Per-Card-Snippet — KEINEN globalen `ha-card`-Blur setzen |
| **picture-elements (Floorplan-Variante)** | Heatmap-Glow-Tokens via `--floorplan-*` | Room-Marker- / Heatmap-Snippets in `docs/floorplan-snippets.yaml` |

### Warum Tier 2 Opt-in ist (kein Default)

HA-Theme-YAML kann nur CSS-*Variablen* definieren — keine CSS-*Regeln*. Die Deklaration `backdrop-filter: blur(...)` ist eine Regel, keine Variable, daher kann ein Theme sie nicht global auf `ha-card` anwenden, ohne einen `card-mod-theme`-Override zu verwenden. Wir liefern diesen Override **bewusst nicht** mit, weil wir in früherer Entwicklung beobachtet haben, dass er das Bubble-Card-v3-Pop-up-Rendering bricht (Bubble Card Issue #2347 — global gestylte `ha-card-*`-Properties leaken in die Pop-up-Internals und der Pop-up-Body rendert leer). Tier 2 als Per-Card-Opt-in ist der sicherste Pfad, der die Plugin-Kompatibilität wahrt.

### Copy-Paste — das Tier-2-Snippet

Unter jede Tile-, Thermostat-, Area-, Entities- oder Glance-Karte einfügen, um die Screenshot-Optik zu treffen:

```yaml
type: tile
entity: light.wohnzimmer
card_mod:
  style: |
    ha-card {
      background: var(--glass-bg);
      backdrop-filter: var(--glass-blur);
      -webkit-backdrop-filter: var(--glass-blur);
      border: var(--glass-border);
      border-radius: var(--glass-radius);
      box-shadow: var(--glass-shadow);
    }
```

Das Snippet nutzt Theme-Variablen, passt sich also automatisch an, wenn du zwischen Liquid Glass / Light only / Compact / Sunset wechselst. Volle Snippet-Bibliothek: [`docs/card-mod-snippets.yaml`](docs/card-mod-snippets.yaml).

Voraussetzung: [card-mod](https://github.com/thomasloven/lovelace-card-mod) via HACS installiert.

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

> ℹ️ **Diesen Abschnitt überspringen, wenn du keinen Extra-Polish brauchst.** Das Theme funktioniert vollständig auf Tier 1 ohne card-mod. Die folgenden Dateien sind **Opt-in-Extras** — card-mod nur installieren, wenn du Tier-2-Effekte (voller Blur auf Standard-Karten) oder die unten gelisteten Extras willst.

Für User, die [card-mod](https://github.com/thomasloven/lovelace-card-mod) bereits haben oder installieren wollen:

- [`docs/card-mod-snippets.yaml`](docs/card-mod-snippets.yaml) — zwölf Drop-in-Mods, beginnend mit dem Tier-2-`glass_card_base`-Recipe
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

Nein. Das Theme ist Plug-and-Play auf **Tier 1** — jede vorhandene Lovelace-Karte übernimmt automatisch die Liquid-Glass-Color-Tokens (durchscheinender dunkler Hintergrund, abgerundete Ecken, feine Borders, WCAG-AA-Text). card-mod kommt erst für **Tier 2** ins Spiel — den vollen Backdrop-Blur-Effekt auf Standard-Karten oder die optionalen Polish-Snippets in [`docs/`](docs/). Siehe [Effekt-Tiers](#effekt-tiers--was-das-theme-automatisch-liefert-vs-opt-in) für den exakten Split.

### Warum haben meine Tile- / Thermostat- / Area-Karten nicht den gleichen Blur wie in den Screenshots?

Das ist der bewusste Tier-1-vs.-Tier-2-Split. Tier 1 ist das, was jede Karte automatisch erbt: durchscheinende dunkle Oberfläche, abgerundete Ecken, Theme-Borders, harmonisierte Statusfarben. Tier 2 — der volle `backdrop-filter: blur(...)`-Glaseffekt — ist Opt-in pro Karte via dem `glass_card_base`-Snippet in [`docs/card-mod-snippets.yaml`](docs/card-mod-snippets.yaml). Warum kein Default: Wenn man `backdrop-filter` global auf `ha-card` via `card-mod-theme` setzt, ist bekannt, dass das Bubble-Card-v3-Pop-up-Rendering bricht — deshalb liefern wir es als expliziten Opt-in. Copy-paste das achtzeilige Snippet unter eine beliebige Karte und du hast die Screenshot-Optik. [Snippet](#effekt-tiers--was-das-theme-automatisch-liefert-vs-opt-in) | [Volle Snippet-Bibliothek](docs/card-mod-snippets.yaml).

### Muss ich YAML editieren, um das Theme zu nutzen?

Nein. Der einzige manuelle Schritt ist, die vier Hintergrund-PNGs in `/config/www/liquid_glass/` zu kopieren (einmaliges Setup). Alles andere funktioniert automatisch.

### Welche Dashboard-Karten sind in den Screenshots zu sehen?

Standard- + populäre Community-Karten: Lovelace-Tile, [Mushroom](https://github.com/piitaya/lovelace-mushroom), [mini-graph-card](https://github.com/kalkih/mini-graph-card), [mini-media-player](https://github.com/kalkih/mini-media-player), [vacuum-card](https://github.com/denysdovhan/vacuum-card). Die Mushroom- und mini-graph-Karten bringen ihren eigenen Blur mit und sehen schon auf Tier 1 "full glass" aus. Die in den Screenshots sichtbaren Standard-Tile-Karten nutzen das Tier-2-`glass_card_base`-Snippet. Referenz-Dashboard mit Platzhalter-Entity-IDs: [`docs/demo-dashboard.yaml`](docs/demo-dashboard.yaml).

### Was ist in `themes/liquid_glass.yaml`?

Eine ~1250-zeilige YAML-Datei mit sechs Theme-Varianten. Du musst sie nicht öffnen oder editieren — HACS installiert sie, HA lädt sie automatisch.

### Warum werden die Hintergründe nicht automatisch installiert?

HACS kann Theme-YAML ausliefern, aber nicht in `/config/www/` schreiben. Lovelace referenziert Bilder per URL-Pfad — die vier PNGs müssen also einmalig in den `www/`-Ordner deiner Config.

### Etwas sieht falsch aus / Kontrast stimmt nicht / ein Popup ist Weiß-auf-Weiß

Issue öffnen mit: HA-Core-Version, Browser, betroffenes Element (DevTools-Screenshot der computed CSS-Variable). Der Abschnitt "Issues diagnostizieren" oben führt durch.

## Lizenz

MIT — siehe [LICENSE](LICENSE).
