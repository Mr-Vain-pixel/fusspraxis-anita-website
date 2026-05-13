# Deployment-Anleitung — Fusspraxis Anita

Schritt-für-Schritt-Anleitung, um die Website über GitHub und Vercel online zu bringen.

**Zeitaufwand:** ca. 30 Minuten beim ersten Mal, danach Updates in 1–2 Minuten.

---

## Übersicht

```
┌─────────────────┐    git push    ┌─────────────────┐   automatisch   ┌─────────────────┐
│                 │ ──────────────►│                 │ ────────────────►│                 │
│  Dein Computer  │                │     GitHub      │                  │     Vercel      │
│  (Quellcode)    │                │  (Repository)   │                  │   (Live-Site)   │
└─────────────────┘                └─────────────────┘                  └─────────────────┘
```

---

## Schritt 1: GitHub-Account & Repository

### 1.1 Account erstellen (falls noch nicht vorhanden)

1. Gehe auf <https://github.com/signup>
2. Erstelle ein kostenloses Konto mit deiner E-Mail-Adresse
3. Wähle den **Free Plan** — reicht für dieses Projekt vollständig

### 1.2 Neues Repository anlegen

1. Auf GitHub oben rechts auf das **+** klicken → "**New repository**"
2. Felder ausfüllen:
   - **Repository name:** `fusspraxis-anita-website`
   - **Description:** `Website für die Podologie-Praxis Anita Hofer-Küng in Luzern`
   - **Visibility:** `Private` *(empfohlen — Inhalte und Fotos sind nicht öffentlich)*
   - **NICHT** anhaken: "Add a README file", "Add .gitignore", "Choose a license"
     *(haben wir alles schon im Paket)*
3. Auf **Create repository** klicken

GitHub zeigt dir nun eine Seite mit verschiedenen Optionen. Wir nutzen den Weg "**…push an existing repository from the command line**" — kommt im nächsten Schritt.

---

## Schritt 2: Code auf GitHub hochladen

### Variante A: Mit Drag & Drop (einfacher, ohne Terminal)

1. Auf der eben angelegten Repository-Seite klickst du auf **uploading an existing file**
2. Ziehe **alle Dateien und Ordner** aus dem entpackten ZIP in den Browser-Bereich
   - `index.html`, `impressum.html`, `README.md`, `.gitignore`, `vercel.json`
   - Ordner `bilder/`, `fonts/`
3. Unten Feld "**Commit changes**" — Titel z. B. `Initial commit: Fusspraxis Anita website`
4. Auf **Commit changes** klicken

Fertig — die Dateien sind jetzt auf GitHub.

### Variante B: Mit Terminal/Git (für Fortgeschrittene)

```bash
cd Pfad/zum/entpackten/fusspraxis-anita-website
git init
git add .
git commit -m "Initial commit: Fusspraxis Anita website"
git branch -M main
git remote add origin https://github.com/DEIN-USERNAME/fusspraxis-anita-website.git
git push -u origin main
```

*DEIN-USERNAME* durch deinen GitHub-Benutzernamen ersetzen.

---

## Schritt 3: Vercel-Account & Deployment

### 3.1 Account erstellen

1. Gehe auf <https://vercel.com/signup>
2. Klicke auf **Continue with GitHub** — verbindet Vercel direkt mit deinem GitHub-Account (empfohlen)
3. Vercel fragt nach Zugriffsrechten — bestätige das

### 3.2 Projekt importieren

1. Im Vercel-Dashboard auf **Add New…** → **Project** klicken
2. Vercel zeigt deine GitHub-Repositories — falls `fusspraxis-anita-website` nicht erscheint:
   - Klick auf **Adjust GitHub App Permissions** und gewähre Vercel Zugriff auf das neue Repo
3. Beim richtigen Repository auf **Import** klicken
4. Auf der Konfigurationsseite **alle Felder unverändert lassen** — Vercel erkennt es automatisch als statische Seite:
   - Framework Preset: `Other`
   - Build Command: leer lassen
   - Output Directory: leer lassen
5. Auf **Deploy** klicken

In etwa 30 Sekunden ist die Seite live unter einer URL wie:
`https://fusspraxis-anita-website.vercel.app`

---

## Schritt 4: Eigene Domain verbinden (fusspraxis-anita.ch)

### 4.1 Domain bei Vercel hinzufügen

1. Im Vercel-Projekt → Tab **Settings** → **Domains**
2. Eingeben: `fusspraxis-anita.ch` → **Add**
3. Wiederholen mit: `www.fusspraxis-anita.ch` → **Add**
4. Vercel zeigt dir nun die nötigen DNS-Einträge an. Notiere dir:
   - Einen **A-Record** mit IP-Adresse (für die Hauptdomain)
   - Einen **CNAME-Record** (für die www-Variante)

### 4.2 DNS-Einträge beim Domain-Anbieter setzen

Die aktuelle Domain wird bei einem Schweizer Hoster liegen (vermutlich Hostpoint, Cyon, Infomaniak, Switchplus oder ähnlich).

1. Beim aktuellen Anbieter ins DNS-Management einloggen
2. **Vor dem Umstellen sichern:** Mache Screenshots der bestehenden DNS-Einträge — falls etwas mit dem E-Mail-Versand schiefläuft, kannst du zurückkehren
3. **A-Record für die Hauptdomain ändern/hinzufügen:**
   - Name: `@` (oder leer, je nach Anbieter)
   - Wert: die IP von Vercel (z. B. `76.76.21.21`)
4. **CNAME-Record für www:**
   - Name: `www`
   - Wert: `cname.vercel-dns.com`
5. **MX-Records (E-Mail) NICHT ändern** — die regeln, wohin E-Mails an `@fusspraxis-anita.ch` gehen
6. Speichern

### 4.3 Warten und prüfen

- DNS-Änderungen brauchen meist **15 Minuten bis 4 Stunden**, in seltenen Fällen bis zu 48 Stunden
- Vercel zeigt im Domain-Tab grüne Häkchen, sobald alles funktioniert
- HTTPS-Zertifikat wird automatisch eingerichtet (Let's Encrypt)

---

## Schritt 5: Spätere Änderungen vornehmen

Sobald alles läuft, sind Updates einfach:

1. Datei lokal ändern (z. B. neuer Text in `index.html`)
2. Auf GitHub im Browser zur Datei navigieren → Stift-Icon klicken → bearbeiten → **Commit changes**
   *(oder via Terminal: `git add . && git commit -m "Beschreibung" && git push`)*
3. Vercel deployt automatisch in ~10 Sekunden — fertig

**Tipp:** Jeder Push erzeugt einen Preview-Link, sodass du Änderungen vor der Live-Schaltung testen kannst.

---

## Wichtige Hinweise

### E-Mail bleibt unberührt

Falls Anita E-Mails an `@fusspraxis-anita.ch` empfängt, läuft die über separate MX-DNS-Records, die wir **nicht ändern**. Die A- und CNAME-Records sind nur für die Website zuständig.

### Privater Modus

Da das Repo `Private` ist, kann nur dein GitHub-Account es sehen. Wenn du Anita oder einer anderen Person Zugriff geben willst:

GitHub-Repo → **Settings** → **Collaborators** → Person einladen.

### Kostenüberblick

| Dienst | Kosten | Limit |
|---|---|---|
| GitHub Free | 0 CHF | Unbegrenzte private Repositories |
| Vercel Hobby | 0 CHF | 100 GB Traffic / Monat — für eine Praxis-Website astronomisch viel |
| Domain | bestehende Kosten ändern sich nicht | bleibt beim aktuellen Anbieter |

Insgesamt: **0 CHF/Monat zusätzlich**.

### Was tun, wenn die alte Website abgeschaltet werden soll?

Erst nachdem die neue Website live ist und du sie geprüft hast:

1. Vom aktuellen Hoster (wo `fusspraxis-anita.ch` läuft) das Webhosting-Paket kündigen
2. **Wichtig:** Domain-Registration und E-Mail-Service ggf. behalten, falls Anita die nutzt
3. Manche Hoster bieten "nur Domain" als günstigere Option (CHF 15–25/Jahr)

---

## Hilfe bei Problemen

- **DNS funktioniert nicht** — meist hilft 24 Stunden warten, oder Tool wie <https://dnschecker.org/> nutzen
- **Vercel-Deploy schlägt fehl** — Vercel zeigt Logs an, meist tippfehler in `vercel.json` oder fehlende Datei
- **HTTPS-Zertifikat hängt** — kann bis 24 Stunden dauern; Vercel-Dashboard zeigt Status

Bei Fragen jederzeit melden.
