
# 🔍 Barrierefreiheit: Farbkontrast-Check im Entwicklungs-Workflow

Dieses Dokument beschreibt einen einfachen Workflow zur Prüfung und Korrektur von Farbkontrasten in HTML-E-Mails oder Webinhalten mithilfe von **axe DevTools** und dem **Color Contrast Analyzer**.

---

## 🛠 Benötigte Tools

- **[axe DevTools (Chrome Extension)](https://www.deque.com/axe/devtools/)**
  - Führt eine automatisierte Barrierefreiheitsprüfung durch
  - Integriert direkt in die Chrome DevTools
- **[Color Contrast Analyzer (TPGi)](https://www.tpgi.com/color-contrast-checker/)**
  - Desktop-Anwendung zur Prüfung von Kontrastverhältnissen auf dem Bildschirm

---

## ✅ Workflow

### 1. E-Mail oder HTML im Browser öffnen
- Öffne die zu prüfende HTML-Datei lokal im Browser (z. B. `file:///...`)
- Alternativ: im Browser gerenderte E-Mail anzeigen

### 2. Barrierefreiheits-Analyse mit axe DevTools
1. Rechtsklick auf die Seite → „Untersuchen“
2. DevTools öffnen und auf den Tab **"axe DevTools"** wechseln
3. Klicke auf **"Analyze"**
4. Unter „Violations“ siehst du alle erkannten Probleme, inkl. Kontrastfehler

### 3. Kontrastwerte visuell mit dem Color Contrast Analyzer prüfen
1. Öffne den **Color Contrast Analyzer**
2. Nutze das Pipetten-Werkzeug, um Text- und Hintergrundfarbe auf dem Bildschirm auszuwählen
3. Das Tool zeigt dir das exakte Kontrastverhältnis und ob es den WCAG-Anforderungen entspricht:
   - ✅ 4.5:1 für normalen Text
   - ✅ 3:1 für großen Text (ab 18pt fett / 24pt normal)
4. Wähle eine passendere Farbe, falls der Kontrast nicht ausreicht

### 4. Farben im Code anpassen
- Ändere Text- oder Hintergrundfarbe im HTML-/CSS-Code
- Wiederhole die Analyse mit axe DevTools zur Verifikation

---

## 💡 Tipp
Nutze Farbtools wie [accessible-colors.com](https://accessible-colors.com/) oder [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) zur Auswahl barrierefreier Farbkombinationen während der Entwicklung.

---

## 📎 Ziel
Stelle sicher, dass alle Textelemente ausreichend Kontrast zum Hintergrund haben und so auch für Menschen mit Sehbeeinträchtigung oder in schwierigen Umgebungen (z. B. grelles Licht) gut lesbar sind.
