
# 📧 Barrierefreiheit in HTML-E-Mails – Best Practices & Learnings

Barrierefreie E-Mails sorgen dafür, dass Inhalte auch für Nutzer:innen mit Screenreader oder Tastaturbedienung verständlich und zugänglich sind. Folgende Prinzipien haben sich in der Praxis bewährt:

---

## 🔤 1. Sprache korrekt definieren

Die Sprache des Inhalts hilft Screenreadern, die richtige Aussprache zu wählen.

```html
<html lang="de" xml:lang="de">
```

- `lang="de"` wird von modernen Screenreadern erkannt  
- `xml:lang="de"` sichert Rückwärtskompatibilität, z. B. für ältere Clients

---

## 🧩 2. Strukturrolle für das Dokument setzen

Verwende für den äußeren Container folgende Attribute:

```html
role="article" aria-roledescription="E-Mail" aria-label="Titel der E-Mail"
```

- `role="article"` signalisiert, dass es sich um einen eigenständigen Inhaltsblock handelt  
- `aria-roledescription="E-Mail"` gibt eine benutzerdefinierte Bezeichnung für assistive Technologien  
- `aria-label="..."` beschreibt die E-Mail (z. B. „Newsletter März 2025“, „Ihre Bestellung“)

---

## 📐 3. Tabellen korrekt kennzeichnen

### ✔ Tabellen nur für Layout:

```html
<table role="presentation">
```

- Verhindert, dass Screenreader Tabellen unnötig vorlesen („x Zeilen, y Spalten“)  
- Pflicht für verschachtelte Layouts oder Spaltenraster

### ⚠ Keine komplexe Tabellenstruktur

- Vermeide tief verschachtelte Tabellen  
- Struktur im DOM = visuelle Lesereihenfolge

---

## ⌨ 4. Fokusreihenfolge steuern mit `tabindex`

### 🔢 Feste Reihenfolge mit `tabindex="1"`, `"2"`, …

```html
<a href="#" tabindex="1">Erster Link</a>
<a href="#" tabindex="2">Zweiter Link</a>
```

- Nicht empfohlen, da schwer wartbar  
- Nur verwenden, wenn natürliche Reihenfolge nicht ausreicht

### ✅ Normale Reihenfolge mit `tabindex="0"`

```html
<div role="button" tabindex="0">Klick mich</div>
```

- Ermöglicht Fokus über Tab, in der natürlichen Reihenfolge  
- Wichtig für nicht-interaktive Elemente wie `<div>` oder `<span>`, die interaktiv gestaltet sind

### 🚫 Aus dem Fokus nehmen mit `tabindex="-1"`

```html
<img src="..." alt="..." tabindex="-1">
```

- Element ist nicht per Tab erreichbar  
- Nützlich für dekorative Bilder oder zusätzliche Elemente innerhalb von Buttons

---

## 🔗 5. Links klar und barrierefrei beschreiben

### ✔ Mit `aria-label` und/oder `title`

```html
<a href="..." aria-label="Zur Startseite, externer Link" title="Website besuchen">Startseite</a>
```

- `aria-label` wird von Screenreadern vorgelesen  
- `title` zeigt beim Hover einen Tooltip (hilft sehenden Nutzern)  
- Der Linktext soll verständlich sein, auch außerhalb des Kontexts

### ❗ Gute Linktexte:

- Kein „Hier klicken“  
- Besser: „Mehr zu Versandoptionen lesen“, „Newsletter abonnieren“

### ℹ️ Empfehlung zur Länge:

- `aria-label` sollte nicht länger als **100–120 Zeichen** sein  
- Klarheit und Kürze gehen vor

---

## 🧪 Bonus: Weitere Empfehlungen

- **Alternativtexte (`alt`)** für alle Bilder  
  - Nur leer lassen, wenn rein dekorativ: `alt="" role="presentation"`

- **Keine versteckten Elemente per CSS**, außer mit `aria-hidden="true"`

- **Kein JavaScript in E-Mails verwenden** – wird von fast allen Clients blockiert

- **Responsives Design barrierefrei umsetzen**  
  - Ausreichend Kontrast  
  - Große Touch-Ziele  
  - Skalierbarer Text

---

## ✅ Fazit: Barrierefreie E-Mails sind...

| Gut für...                  | Weil...                                                  |
|----------------------------|-----------------------------------------------------------|
| Screenreader-Nutzer:innen  | Inhalte verständlich strukturiert und lesbar             |
| Tastaturnutzer:innen       | Navigierbare, fokussierbare Inhalte                      |
| Alle Empfänger:innen       | Klare Kommunikation, höhere Conversion, bessere UX       |
