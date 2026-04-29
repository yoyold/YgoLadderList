# Duel Ladder

Statische Webseite zum Verwalten eines Yu-Gi-Oh Deck-Ladders (Crosstable). Daten werden in `data.json` im Repo gehalten und können direkt aus der Seite heraus von angemeldeten Nutzern bearbeitet und zurück ins Repo geschrieben werden.

## Features

- Rangliste sortiert nach Wins (Tiebreaker: Winrate, weniger Niederlagen, Name)
- Crosstable mit Klick-zum-Ergebnis (leer → Sieg → Niederlage → leer); Spiegelzelle wird automatisch konsistent gesetzt
- Direktduell-Anzeige
- Decks hinzufügen / umbenennen / löschen
- xlsx-Import & -Export im Originalformat
- GitHub-Sync für Multi-Device-Bearbeitung
- Login per Personal Access Token (PAT) — nur angemeldete Nutzer können speichern
- Lokaler Offline-Modus mit localStorage-Cache und „Ungespeichert"-Indikator

## Setup

### 1. Repo auf GitHub anlegen
1. Erstelle ein neues GitHub-Repo, z. B. `YgoLadderList` (öffentlich, damit GitHub Pages ohne Pro-Account funktioniert).
2. Lade `index.html` und `data.json` ins Repo (z. B. via `git push` oder Web-Upload).

### 2. GitHub Pages aktivieren
1. Im Repo: **Settings → Pages**.
2. **Source** = `Deploy from a branch`, Branch = `main`, Folder = `/ (root)`.
3. Nach ~1 Minute ist die Seite unter `https://<USER>.github.io/YgoLadderList/` erreichbar.

### 3. Personal Access Token erstellen (nur für Editoren)
1. Gehe zu https://github.com/settings/personal-access-tokens und klicke **Fine-grained token → Generate new token**.
2. **Repository access** = `Only select repositories` → wähle `YgoLadderList`.
3. **Repository permissions → Contents** = `Read and write`.
4. Token erzeugen und kopieren (er wird nur einmal angezeigt).

### 4. Auf der Webseite anmelden
1. Öffne die Seite, klicke oben rechts auf **Anmelden**.
2. Owner, Repo, Branch, Pfad sind ggf. schon vorausgefüllt; Token einfügen → **Speichern**.
3. Token bleibt im localStorage des Browsers — pro Gerät einmal anmelden.

## Bedienung

- **Lokal arbeiten**: Alle Änderungen werden sofort lokal gespeichert. Status-Badge zeigt „Ungespeichert" (Goldener Punkt).
- **Speichern**: Button **⤒ Speichern** (oben rechts) schreibt nach GitHub. Der Status wird auf „Synchronisiert" gesetzt.
- **Sync**: Button **⤓ Sync** holt den aktuellsten Stand von GitHub und überschreibt lokale Änderungen (mit Bestätigung).
- **Konflikt**: Wenn jemand anders zwischenzeitlich gespeichert hat, fragt die Seite vor dem Überschreiben nach.

## Sicherheitshinweise

- **Lese-Zugriff**: Bei einem öffentlichen Repo kann jeder die Daten lesen. Wer **nicht angemeldet** ist, sieht aber nur „Schreibgeschützt" — er kann lokal herumspielen, aber nichts ins Repo schreiben.
- **Token**: Liegt im localStorage des Browsers. Logout-Button im Anmelde-Dialog entfernt ihn wieder. Token mit minimalen Rechten verwenden (nur dieses Repo, nur Contents).
- **Privates Repo**: Funktioniert auch, aber dann brauchen auch Lesezugriffe einen Token. GitHub Pages für private Repos erfordert GitHub Pro.

## Dateien

- `index.html` — die App
- `data.json` — der aktuelle Stand (Decks + Crosstable-Matrix)
- `assets/fonts.css` + `assets/fonts/*.woff2` — selbst gehostete Schriftarten Cinzel und Inter (SIL Open Font License)
- `assets/xlsx.full.min.js` — selbst gehostete SheetJS-Bibliothek (Apache 2.0)
- `README.md` — diese Datei

## DSGVO

Die Seite ist bewusst tracker- und drittanbieterfrei aufgebaut:

- **Keine externen Requests beim Laden.** Schriftarten und JavaScript-Bibliothek liegen lokal im Repo und werden vom selben Origin (GitHub Pages) ausgeliefert. Keine Verbindung zu Google Fonts, jsDelivr, Analytics o.ä.
- **Keine Cookies.** Es wird ausschließlich `localStorage` verwendet, um deine Eingaben offline zu cachen und (optional) deinen GitHub-Token zu speichern. Diese Daten verlassen dein Gerät nicht ohne explizite Aktion.
- **Externe Verbindungen nur auf Knopfdruck.** Erst beim Klick auf `Sync` oder `Speichern` wird `api.github.com` kontaktiert.
- **Hosting via GitHub Pages.** GitHub speichert technische Server-Logs (IP, User-Agent, Zeitstempel). Wer das vermeiden möchte, hostet die statischen Dateien auf eigenem Webspace im EU-Raum — die App selbst funktioniert unverändert.
- **Datenschutzerklärung** ist im Footer der Seite verlinkt. Sie sollte vor Live-Schaltung um deine Kontaktdaten ergänzt werden, falls die Seite öffentlich zugänglich ist.
