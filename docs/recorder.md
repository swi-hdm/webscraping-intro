# Nutzung des Recorders in den Chrome Dev Tools

Diese Anleitung beschreibt, wie Sie Benutzerinteraktionen direkt im Browser aufnehmen und sie anschließend programmatisch mit Puppeteer abspielen. Dies ist ideal für End-to-End (E2E) Tests und Automatisierung.

## 1. Aufnahme erstellen (Chrome DevTools)

Der erste Schritt ist das Aufzeichnen des Flows direkt in Google Chrome.

1.  Öffnen Sie die Website, die Sie testen möchten.
2.  Öffnen Sie die Entwicklertools (**F12** oder Rechtsklick -> *Untersuchen*).
3.  Navigieren Sie zum Tab **Recorder** (falls nicht sichtbar: Klicken Sie auf die drei Punkte `...` rechts oben im DevTools-Menü -> *Weitere Tools* -> *Recorder*).
4.  Klicken Sie auf **Create a new recording**.
5.  Geben Sie der Aufnahme einen Namen (z.B. "Login Test") und klicken Sie auf **Start recording**.
6.  Führen Sie die Aktionen auf der Website durch (Klicken, Tippen, Scrollen).
7.  Klicken Sie im Recorder-Panel auf **End recording**.

---

## 2. Export als Puppeteer-Skript
Dies generiert eine fertige `.js` Datei mit Puppeteer-Code.

1.  Klicken Sie oben im Recorder auf das **Download-Icon** (Pfeil nach unten).
2.  Wählen Sie **Export as** -> **Puppeteer script**.
3.  Speichern Sie die Datei (z.B. `flow.js`).


## 3. Abspielen mit Puppeteer

Kopieren Sie die Datei in den vorher erstellten Ordner und starten Sie das Script (z.B. `flow.js`) mit

```bash
node flow.js
```
