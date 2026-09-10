# HAK English Lab — Setup (GitHub Pages + Firebase)

Diese App läuft jetzt komplett unabhängig von claude.ai. Sie ist eine einzige Datei (`index.html`), gehostet auf GitHub Pages, mit einer kleinen Firebase-Datenbank im Hintergrund für den Fortschritt der Schüler:innen.

> **Für dich:** Die `index.html` in diesem Paket enthält bereits deine Firebase-Config (Projekt `hak-enws-2`) – Schritt 2 unten ist also schon erledigt. Was noch fehlt: die Firestore-Regeln in der Firebase-Konsole einspielen (Schritt 1.4) und die Datei auf GitHub Pages hochladen (Schritt 3).

## 1. Firebase-Projekt einrichten (einmalig, ~5 Min.)

1. Gehe auf **console.firebase.google.com**, melde dich mit einem Google-Konto an.
2. **Projekt hinzufügen** → Namen vergeben, z. B. `hak-english-lab` → Google Analytics kannst du deaktivieren.
3. Im Projekt: **Build → Firestore Database → Datenbank erstellen** → Standort z. B. `eur3 (europe-west)` → Start im **Testmodus** (die Regeln überschreiben wir gleich mit den mitgelieferten, strengeren).
4. Im Reiter **Regeln** (oben in der Firestore-Ansicht): Inhalt der Datei `firestore.rules` (liegt bei diesem Paket) komplett einfügen → **Veröffentlichen**.
5. Zahnrad oben links → **Projekteinstellungen** → unten bei „Meine Apps" auf **„</>" (Web-App hinzufügen)** → Spitznamen vergeben → **Registrieren** (Firebase Hosting NICHT aktivieren).
6. Es erscheint ein Codeblock mit `const firebaseConfig = { apiKey: "...", ... }`. Diesen Block brauchst du im nächsten Schritt.

## 2. Config in `index.html` einfügen

Öffne `index.html` in einem Texteditor, suche nach:

```js
const firebaseConfig = {
  apiKey: "PASTE_YOUR_API_KEY_HERE",
  authDomain: "PASTE_YOUR_PROJECT_ID_HERE.firebaseapp.com",
  projectId: "PASTE_YOUR_PROJECT_ID_HERE",
  storageBucket: "PASTE_YOUR_PROJECT_ID_HERE.appspot.com",
  messagingSenderId: "PASTE_YOUR_SENDER_ID_HERE",
  appId: "PASTE_YOUR_APP_ID_HERE",
};
```

und ersetze die sechs Platzhalterwerte durch die echten Werte aus deinem Firebase-Codeblock (Schritt 1.6). Speichern.

> Diese Werte sind **keine** geheimen Zugangsdaten — sie stehen bei jeder Firebase-Web-App offen im Quellcode. Die eigentliche Zugriffskontrolle übernehmen die Firestore-Regeln aus Schritt 1.4.

## 3. Auf GitHub Pages veröffentlichen

1. Auf **github.com** einloggen (kostenloses Konto reicht) → **New repository** → Namen vergeben, z. B. `hak-english-lab` → **Public** → **Create repository**.
2. Im leeren Repository: **Add file → Upload files** → `index.html` hineinziehen → **Commit changes**.
3. **Settings** (im Repository) → **Pages** (linkes Menü) → bei „Build and deployment": Source = **Deploy from a branch**, Branch = **main** / **/ (root)** → **Save**.
4. Nach 1–2 Minuten ist die Seite live unter:
   `https://<dein-github-name>.github.io/<repo-name>/`
   (GitHub zeigt dir den genauen Link auf der Pages-Einstellungsseite an, sobald der Build fertig ist.)

Diesen Link kannst du jetzt uneingeschränkt mit allen 16 Schüler:innen teilen — kein claude.ai-Konto nötig, kein Freigabe-Limit.

## 4. Später aktualisieren

Wenn du (oder ich für dich) die App später erweitert (z. B. Unit 4–10 ergänzt): einfach die neue `index.html` im selben Repository hochladen (**Add file → Upload files**, überschreibt die alte) — GitHub Pages baut die Seite automatisch neu, der Link bleibt gleich. Der Firebase-Fortschritt der Schüler:innen bleibt davon unberührt, da er in einer separaten Datenbank liegt.

## 5. Sicherheitshinweis (wie bisher)

Die Lehrer-PIN im Dashboard ist weiterhin kein echter Sicherheitsmechanismus (im Quellcode/Browser einsehbar) — ausreichend für ein Klassenzimmer-Tool ohne sensible Daten, nicht für vertrauliche Zwecke. Die Firestore-Regeln verhindern zumindest, dass jemand beliebige andere Daten in die Datenbank schreibt, aber nicht, dass ein technisch versierter Schüler/eine Schülerin fremde Fortschrittsdaten sieht oder überschreibt — genau wie beim bisherigen claude.ai-Artifact.

## Dateien in diesem Paket

- `index.html` — die komplette App (lädt Firebase per CDN, keine weitere Installation nötig)
- `firestore.rules` — die Sicherheitsregeln für Schritt 1.4
- `README.md` — diese Anleitung
