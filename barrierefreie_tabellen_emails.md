
# 📊 Barrierefreie Datentabellen in HTML-E-Mails

Wenn E-Mails Tabellen mit **echten Daten** enthalten (z. B. Preislisten, Bestellübersichten, Terminpläne), sollten diese **semantisch korrekt** aufgebaut sein, um von Screenreadern sinnvoll vorgelesen zu werden.

---

## ✅ Ziel

Screenreader sollen Zeile für Zeile korrekt erkennen:
- welche Zellen zu welcher Kopfzeile gehören
- was die Bedeutung jeder Zelle ist
- wie viele Spalten/Zeilen es gibt

---

## 📐 Best Practices für Screenreader-kompatible Tabellen

### 1. **Tabellenstruktur semantisch korrekt**

Verwende `<table>` mit:

- `<thead>` für den Tabellenkopf
- `<tbody>` für den Inhalt
- `<th>` für Kopfzellen
- `<td>` für normale Zellen

### Beispiel:

```html
<table>
  <thead>
    <tr>
      <th scope="col">Produkt</th>
      <th scope="col">Menge</th>
      <th scope="col">Preis</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Apfel</td>
      <td>2</td>
      <td>1,00 €</td>
    </tr>
    <tr>
      <td>Banane</td>
      <td>3</td>
      <td>1,50 €</td>
    </tr>
  </tbody>
</table>
```

---

### 2. **`scope`-Attribut verwenden**

Das `scope`-Attribut gibt an, worauf sich eine Kopfzelle bezieht:

| `scope` Wert     | Bedeutung                             |
|------------------|----------------------------------------|
| `col`            | Die `<th>` ist eine **Spaltenüberschrift** |
| `row`            | Die `<th>` ist eine **Zeilenüberschrift**  |
| `colgroup`       | Die `<th>` beschreibt eine **Gruppe von Spalten** |
| `rowgroup`       | Die `<th>` beschreibt eine **Gruppe von Zeilen** |

### 📘 Warum ist das wichtig?

Screenreader nutzen `scope`, um den Zusammenhang zwischen **Datenzellen (`<td>`)** und **Überschriften (`<th>`)** korrekt zu interpretieren.  
Beispiel:  
Wenn ein Screenreader auf eine Zelle mit „1,50 €“ trifft, kann er sagen:  
„Spalte: Preis, Zeile: Banane – Wert: 1,50 €“

Ohne `scope` bleibt diese Zuordnung unklar.

---

### 3. **Tabellenbeschreibung hinzufügen**

Optional mit `aria-label` oder `summary` (nur bei HTML4-kompatiblen Clients):

```html
<table aria-label="Bestellübersicht für Ihre Lieferung">
```

---

### 4. **Kein `role="presentation"` für Datentabellen**

`role="presentation"` sollte nur bei Layout-Tabellen verwendet werden.

> ❌ Nicht verwenden bei echten Daten, sonst ignorieren Screenreader die semantische Struktur.

---

### 5. **Kombinierte Kopfzellen bei komplexeren Tabellen**

Wenn Tabellen verschachtelt oder mehrdimensional sind, nutze zusätzlich `headers`-Attribute oder `id`-Verknüpfungen. In E-Mails aber nur eingeschränkt empfohlen → lieber einfache Tabellen bauen.

---

## ⚠ Einschränkungen in E-Mail-Clients

- Nicht alle Clients unterstützen `<thead>`/`<tbody>` visuell – **aber Screenreader tun es**
- Inline-Styles weiterhin notwendig für Layout (z. B. `border`, `padding`, `font-family`)
- Komplexe Tabellen in mobilen Clients schwer lesbar – **mobile-optimiert gestalten**

---

## 🧪 Testen

- Mit **Screenreader testen** (z. B. NVDA oder VoiceOver)
- Sicherstellen, dass beim Navigieren die Spalten-/Zeilenüberschriften vorgelesen werden
- Tabellen in **verschiedenen E-Mail-Clients** und auf **mobilen Geräten** prüfen

---

## ✅ Fazit

Gut strukturierte Datentabellen ermöglichen Screenreader-Nutzer:innen, Inhalte schnell zu erfassen – besonders in transaktionalen E-Mails wie Rechnungen, Buchungsdetails oder Versandübersichten.

**Einfach, semantisch korrekt, mit klaren Überschriften = barrierefreundlich.**
