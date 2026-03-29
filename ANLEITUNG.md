# WUEKC Merch Shop – Einrichtungsanleitung

## 📁 Dateistruktur

```
wuekc-merch/
├── index.html          ← Die gesamte Website (eine Datei!)
└── img/                ← Ordner für deine Produktbilder (selbst erstellen)
    ├── classic.jpg
    ├── statement.jpg
    └── minimal.jpg
```

---

## 1️⃣ PayPal Payment Links einrichten

### Was sind Payment Links?
PayPal Payment Links sind URLs, die direkt zu einer PayPal-Checkout-Seite führen. Der Kunde klickt den Link, bezahlt über PayPal (oder Kreditkarte als Gast), und du erhältst das Geld auf dein PayPal-Geschäftskonto. **Kein Warenkorb, kein Shop-System nötig.**

### Voraussetzung
- Ein **PayPal-Geschäftskonto** (kostenlos umstellbar unter paypal.com/de → Konto upgraden)

### Schritt-für-Schritt: Zahlungslinks erstellen

1. **Gehe zu:** [paypal.com/buttons](https://www.paypal.com/buttons) oder im PayPal-Dashboard → *Bezahlen & Geld erhalten* → *Zahlungslinks und -Buttons erstellen*

2. **Wähle:** "Zahlungslink erstellen"

3. **Produkt anlegen** (für jede Produkt+Größen-Kombination einzeln):
   - **Name:** z.B. `WUEKC Classic Tee – Größe M`
   - **Preis:** z.B. `29,90` EUR
   - **Beschreibung:** z.B. "100% Baumwolle, Regular Fit, Logo-Print"
   - **Bild:** Optional ein Produktfoto hochladen (empfohlen!)
   - **Versand:** Versandkosten hier eintragen oder separat regeln

4. **Link kopieren** – er sieht so aus:
   ```
   https://www.paypal.com/ncp/payment/XXXXXXXXXX
   ```

5. **Wiederhole das für alle 12 Kombinationen:**

   | Produkt        | S | M | L | XL |
   |---------------|---|---|---|-----|
   | Classic Tee    | ✓ | ✓ | ✓ | ✓  |
   | Statement Tee  | ✓ | ✓ | ✓ | ✓  |
   | Minimal Tee    | ✓ | ✓ | ✓ | ✓  |

### Alternative: PayPal "Buy Now" Buttons
Statt Zahlungslinks kannst du auch **Buy-Now-Buttons** erstellen. Dabei bekommst du HTML-Code zum Einbetten. Die Zahlungslinks sind aber einfacher zu verwalten, da du nur URLs in der `index.html` ändern musst.

---

## 2️⃣ Links in die Website eintragen

Öffne `index.html` in einem Texteditor und finde den Abschnitt `PAYPAL_LINKS` (ca. Zeile 380):

```javascript
const PAYPAL_LINKS = {
    "classic": {
        "S":  "https://www.paypal.com/ncp/payment/DEIN_LINK_CLASSIC_S",   // ← hier ersetzen
        "M":  "https://www.paypal.com/ncp/payment/DEIN_LINK_CLASSIC_M",
        // ...
    },
    // ...
};
```

Ersetze jeden `DEIN_LINK_...`-Platzhalter durch den echten PayPal Payment Link.

---

## 3️⃣ Produktbilder einfügen

In der `index.html` findest du bei jedem Produkt einen Kommentar-Block:

```html
<!-- BILD ERSETZEN: -->
<div class="placeholder-img">...</div>
```

Ersetze den gesamten `<div class="placeholder-img">...</div>` Block durch:

```html
<img src="img/classic.jpg" alt="WUEKC Classic Tee">
```

Empfohlene Bildgröße: **800×800 px** (quadratisch), JPG oder WebP.

---

## 4️⃣ Kostenlos hosten & testen

### Option A: Netlify Drop (Empfehlung – am schnellsten)
1. Gehe zu [app.netlify.com/drop](https://app.netlify.com/drop)
2. Ziehe deinen Projektordner per Drag & Drop rein
3. Fertig! Du bekommst eine URL wie `random-name-1234.netlify.app`
4. Optional: Netlify-Account erstellen → Custom Domain, HTTPS, etc.
5. **Zum Aktualisieren:** Einfach erneut den Ordner reinziehen

### Option B: GitHub Pages (langfristig & kostenlos)
1. Erstelle einen Account auf [github.com](https://github.com)
2. Neues Repository anlegen (z.B. `wuekc-merch`)
3. Dateien hochladen (Upload-Button im Browser)
4. Settings → Pages → Branch "main" auswählen → Save
5. Deine Seite ist unter `deinname.github.io/wuekc-merch` erreichbar
6. **Zum Aktualisieren:** Datei im GitHub-Editor bearbeiten oder neu hochladen

### Option C: Lokal testen (ohne Internet)
Doppelklick auf `index.html` → öffnet sich im Browser. Alles funktioniert lokal (PayPal-Links öffnen im Demo-Modus ein Alert-Fenster statt eines echten Links).

---

## 5️⃣ Anpassungen

### Preise ändern
Suche in der HTML-Datei nach `product-price` und ändere den Preis im angezeigten Text. **Wichtig:** Der tatsächliche Zahlungspreis wird durch den PayPal-Link bestimmt, nicht durch die Website!

### Produktnamen / Beschreibungen
Einfach den Text in den entsprechenden `<h3>` und `<p>` Tags ändern.

### Farben
Alle Farben sind oben in der CSS-Datei als Variablen definiert:
```css
--accent: #d4ff2b;        /* Akzentfarbe (Neongrün) */
--bg-primary: #0a0a0a;    /* Hintergrund */
--text-primary: #f0ece4;  /* Textfarbe */
```

### Neues Produkt hinzufügen
1. Kopiere einen `<div class="product-card">...</div>` Block
2. Ändere `data-product="neuer-name"`
3. Füge den neuen Namen in `PAYPAL_LINKS` im JavaScript hinzu

---

## 💡 Tipps

- **PayPal-Gebühren:** Pro Transaktion fallen die üblichen PayPal-Gebühren an (ca. 2,49% + 0,35€ für DE). Keine Monatsgebühren für die Zahlungslinks.
- **Steuern/Versand:** Kannst du direkt im PayPal-Link konfigurieren oder manuell abrechnen.
- **Testen:** PayPal bietet eine Sandbox-Umgebung zum Testen. Für einfache Tests reicht es, die Links zu öffnen und zu prüfen, ob die richtige Checkout-Seite erscheint.
- **Impressum/Datenschutz:** Für den Livebetrieb in Deutschland brauchst du ein Impressum und eine Datenschutzerklärung! Ergänze diese auf der Website.

---

## 🔧 Technische Details

- **Reine HTML/CSS/JS-Seite** – kein Framework, kein Build-Prozess
- **Responsive** – funktioniert auf Handy, Tablet und Desktop
- **Keine Cookies, kein Tracking** – DSGVO-freundlich (solange du kein Analytics einbaust)
- **Demo-Modus:** Wenn ein PayPal-Link noch `DEIN_LINK` enthält, zeigt der Button statt eines Redirects ein Info-Alert
