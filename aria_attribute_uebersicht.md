
# ♿ Übersicht: ARIA-Attribute & Barrierefreiheit in HTML

ARIA (Accessible Rich Internet Applications) erweitert HTML um Attribute, die Webinhalte für Screenreader und andere assistive Technologien zugänglicher machen. Dieses Dokument gibt einen kompakten Überblick über die wichtigsten ARIA-Attribute und deren sinnvollen Einsatz.

---

## 📌 Grundregeln für ARIA

- **Nutze native HTML-Elemente zuerst** (z. B. `<button>`, `<a>`, `<nav>`, `<header>`)
- **Setze ARIA nur ein, wenn HTML allein nicht ausreicht**
- **Falsch eingesetztes ARIA kann Barrieren schaffen**

---

## 🧩 Rollen (`role`)

ARIA-Rollen beschreiben die Funktion eines Elements für assistive Technologien.

| Rolle             | Zweck                                               |
|------------------|------------------------------------------------------|
| `role="button"`   | Element wie ein Button (z. B. auf einem `<div>`)     |
| `role="link"`     | Element als Link kennzeichnen                        |
| `role="navigation"` | Navigationselement, z. B. für Menüs                 |
| `role="banner"`   | Oberer Bereich (Header) einer Seite                  |
| `role="main"`     | Hauptinhalt einer Seite                              |
| `role="contentinfo"` | Footer bzw. Impressum-Bereich                     |
| `role="article"`  | Selbstständiger Inhaltsblock                         |
| `role="presentation"` / `role="none"` | Deko-Element, für Screenreader ignorieren |

---

## 🔤 Zustände & Eigenschaften (ARIA States & Properties)

Diese Attribute ergänzen Rollen oder HTML-Elemente mit mehr Bedeutung.

| Attribut              | Bedeutung / Beispiel                                  |
|------------------------|-------------------------------------------------------|
| `aria-label="..."`     | Beschriftung für das Element (wird vorgelesen)       |
| `aria-labelledby="id"`| Verweist auf ein anderes Element zur Beschriftung     |
| `aria-describedby="id"`| Zusätzliche Beschreibung (z. B. Tooltip, Hinweis)     |
| `aria-hidden="true"`   | Element für Screenreader ausblenden                  |
| `aria-pressed="true"`  | Zustand eines Toggle-Buttons                         |
| `aria-expanded="false"`| Zeigt, ob ein Akkordeon geöffnet ist                |
| `aria-current="page"`  | Aktiver Link in Navigation markieren                 |
| `aria-live="polite"`   | Dynamische Inhalte werden vorgelesen (z. B. Alerts)  |
| `aria-disabled="true"` | Element ist deaktiviert (visuell und für SR)        |
| `aria-roledescription="..."` | Benutzerdefinierte Rollenbeschreibung         |

---

## 📏 Empfohlene Kombinationen

### ✔ Interaktives `<div>` als Button

```html
<div role="button" tabindex="0" aria-label="Suche öffnen"></div>
```

### ✔ Beschreibung durch benachbartes Element

```html
<label id="emailLabel">E-Mail-Adresse</label>
<input type="email" aria-labelledby="emailLabel">
```

### ✔ Ignorierbare Layout-Tabelle

```html
<table role="presentation">
```

---

## ❗ Häufige Fehler vermeiden

- Kein `aria-hidden="true"` auf sichtbaren, wichtigen Inhalten
- Nicht auf Links/Buttons verzichten (z. B. `<span role="button">` statt `<button>`)
- Nicht zwei widersprüchliche Rollen oder Labels auf ein Element setzen
- ARIA ersetzt **nicht** die semantische Struktur (Überschriften, Listen, Formulare)

---

## ✅ Ziel

Durch korrekte Nutzung von ARIA-Attributen können auch komplexere Layouts, dynamische Inhalte oder nicht-standardmäßige Interaktionen **barrierefrei gestaltet** werden.

Weitere Infos: [WAI-ARIA Authoring Practices](https://www.w3.org/WAI/ARIA/apg/)
