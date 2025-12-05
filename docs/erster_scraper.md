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
  await page.goto('https://quotes.toscrape.com/');

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

**Ausführen:** Tippen Sie im Terminal: node index.js

Die folgenden Dinge sollten passieren (wenn alles funktioniert):

* Ein neuer (anonymer) Chrome-Browser wird gestartet.
* Die Webseite [https://quotes.toscrape.com/](https://quotes.toscrape.com/) wird aufgerufen.
* Puppeteer erstellt einen Screenshot und speichert diesen als startseite.png im gleichen Ordner wie die Datei index.js.
* Daten (Zitat und Autor) werden von der Webseite extrahiert und im Terminal angezeigt.
* Puppeteer klickt auf den "Next"-Button.
* Das Skript wartet 2 Sekunden.
* Der Browser wird automatisch geschlossen.
