# Fusspraxis Anita — Website

Eine elegante, statisch ausgelieferte Website für die Podologie-Praxis Anita Hofer-Küng in Luzern.

**Ziel:** Besucher zum Anrufen bewegen, um einen Behandlungstermin zu vereinbaren.

## Tech Stack

- **Pure HTML, CSS, vanilla JavaScript** — kein Framework, keine Build-Tools, keine externen Abhängigkeiten zur Laufzeit
- **Self-hosted Fonts** (Fraunces & Manrope als Variable Fonts) — keine Verbindung zu Google-Servern, kein Cookie-Banner nötig
- **Inline SVG** für Icons, Logo und Karte — bleibt bei jeder Auflösung scharf
- **Komprimierte JPEGs** für Foto-Inhalte (≈1 MB Gesamtbilder)

## Lokal anschauen

Einfach die `index.html` im Browser öffnen — die Website funktioniert ohne Server.

Für eine realitätsnahe Vorschau mit lokalem Webserver:

```bash
# Option 1: Mit Python (auf macOS/Linux meist vorinstalliert)
python3 -m http.server 8000

# Option 2: Mit Node.js
npx serve .

# dann im Browser: http://localhost:8000
```

## Struktur

```
fusspraxis-anita-website/
├── index.html                 # Startseite (One-Page)
├── impressum.html             # Impressum & rechtliche Hinweise
├── bilder/                    # Komprimierte Fotos (Team, Praxis, Hero)
├── fonts/                     # Self-hosted Variable Fonts + Lizenzen
└── vercel.json                # Vercel Deployment-Konfiguration
```

## Deployment

Die Website wird automatisch über **Vercel** deployt, sobald Änderungen auf den `main`-Branch gepusht werden.

Produktion: <https://www.fusspraxis-anita.ch>

## Inhalte ändern

Texte, Bilder und Inhalte liegen direkt in den HTML-Dateien.

- **Texte:** In `index.html` bzw. `impressum.html` editieren
- **Team-Fotos:** Im Ordner `bilder/` mit gleichem Dateinamen ersetzen
- **Telefonnummer:** Globale Suche nach `+41 41 240 84 84` und `tel:+41412408484`
- **Adresse:** Globale Suche nach `Kasimir-Pfyffer-Strasse`

## Lizenzen

- **Fraunces** und **Manrope**: SIL Open Font License 1.1 — siehe `fonts/LICENSE-*.txt`
- **SPV-Logo**: Mit Genehmigung des Schweizerischen Podologen-Verbands verwendet
- **Inhalte und Bilder**: © Fusspraxis Anita Hofer-Küng

## Datenschutz

Die Website lädt **keine** externen Ressourcen zur Laufzeit:

- Keine Analytics, kein Tracking
- Keine Cookies (kein Cookie-Banner nötig)
- Keine externen Schriften, keine externen Scripts
- Eingebundene Google-Maps-Verlinkung erfolgt erst beim aktiven Klick des Nutzers

---

**Kontakt:** +41 41 240 84 84 · Kasimir-Pfyffer-Strasse 13 · 6003 Luzern
