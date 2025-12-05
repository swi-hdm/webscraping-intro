# Einführung in Webscraping mit Puppeteer

Willkommen! In diesem Modul lernen wir, wie wir die Datenbeschaffung im Web automatisieren können. Wir nutzen dafür **Puppeteer**, ein Werkzeug, mit dem wir den Chrome-Browser fernsteuern können – als würde ein unsichtbarer Roboter für uns klicken und lesen.

---

## Teil 1: Die Installation (Vorbereitung)

Bevor wir starten, müssen wir unseren "Roboter" auf Ihrem Computer einrichten.

### Schritt 1: Node.js installieren
Wir benötigen eine Laufzeitumgebung für JavaScript außerhalb des Browsers.
1.  Gehen Sie auf [nodejs.org](https://nodejs.org).
2.  Laden Sie die **LTS-Version** (Long Term Support) herunter und installieren Sie sie.
3.  *Test:* Öffnen Sie Ihr Terminal (Mac) oder die Eingabeaufforderung/PowerShell (Windows) und tippen Sie: `node -v`. Es sollte eine Versionsnummer erscheinen (z.B. v18.x.x).

### Schritt 2: Projektordner erstellen
1.  Erstellen Sie einen neuen Ordner auf Ihrem Desktop, nennen Sie ihn z.B. `mein-scraper`.
2.  Öffnen Sie diesen Ordner in Ihrem Code-Editor (z.B. Visual Studio Code).

### Schritt 3: Puppeteer installieren
1.  Öffnen Sie im Editor das integrierte Terminal (`Strg + ö` oder `Ctrl + J` in VS Code).
2.  Tippen Sie: `npm init -y` (Erstellt eine `package.json` Verwaltungsdatei).
3.  Tippen Sie: `npm install puppeteer` (Lädt den Browser-Roboter herunter. Das dauert einen Moment).

---

## Teil 2: Der erste Scraper

Erstellen Sie in Ihrem Ordner eine neue Datei namens `index.js` und kopieren Sie folgenden Code hinein.

**Wichtig:** Lesen Sie die Kommentare im Code, um zu verstehen, was passiert!

```javascript
const puppeteer = require('puppeteer');

(async () => {
  // 1. Browser starten
  // 'headless: false' bedeutet: Wir sehen dem Browser zu.
  // 'slowMo': Bremst den Roboter um 50ms pro Aktion, damit wir menschlicher wirken.
  const browser = await puppeteer.launch({ 
      headless: false, 
      slowMo: 50 
  });

  const page = await browser.newPage();

  // 2. Zur Webseite navigieren
  await page.goto('[https://quotes.toscrape.com/](https://quotes.toscrape.com/)');

  // 3. Interaktion: Screenshot machen
  await page.screenshot({ path: 'startseite.png' });

  // 4. Daten extrahieren (Scraping)
  // Wir suchen das Element mit der Klasse ".text" innerhalb von ".quote"
  // und holen uns den inneren Text (innerText).
  const text = await page.$eval('.quote .text', el => el.innerText);
  const author = await page.$eval('.quote .author', el => el.innerText);

  console.log(`Gefundenes Zitat: "${text}" von ${author}`);

  // 5. Interaktion: Klicken
  // WICHTIG: Wir warten erst auf den "Next" Button, dann klicken wir.
  await page.waitForSelector('.next > a'); 
  await page.click('.next > a');
  
  // Kurz warten, um das Ergebnis zu sehen
  await new Promise(r => setTimeout(r, 2000));

  // 6. Browser schließen
  await browser.close();
})();
```



