# Hinweise zu Links innerhalb von Fließtexten (insbesondere für Screenreader auf mobilen Geräten)

## Problemstellung

Bei der Verwendung von Inline-Links (`<a>`) innerhalb von längerem Fließtext treten bei mobilen Screenreadern (z.B. VoiceOver auf iOS, TalkBack auf Android) folgende Probleme auf:

- Screenreader behandeln Links als eigenständige fokussierbare Elemente.
- Der Text wird nur bis zum Link vorgelesen.
- Nach dem Link muss erneut interagiert werden, um den Rest des Textes vorgelesen zu bekommen.
- Tippen auf den normalen Text, den Link oder den nachfolgenden Text erzeugt unterschiedliche Vorleseverhalten.

Dieses Verhalten erschwert ein flüssiges und zusammenhängendes Vorlesen des gesamten Textabschnitts.

## Ursachen

- Jedes `<a>`-Tag wird von Screenreadern als separates Navigationselement behandelt.
- Die DOM-Struktur (Text-Node + Link-Node) trennt den Lesefluss technisch.

## Lösungsmöglichkeiten

### 1. Verwendung von `aria-label` für zusammenhängendes Vorlesen

Einen umschließenden Container verwenden und ein `aria-label` setzen, das den gesamten Satz enthält.

```html
<td aria-label="Heute Sonne, morgen Regen, übermorgen Schneesturm mit Saharastaub – das Wetter spielt Wer bin ich? und verliert selbst den Überblick. Jacke an. Jacke aus. Kaffee bleibt.">
  Heute Sonne, morgen Regen, übermorgen <a href="..." target="_blank">Schneesturm mit Saharastaub</a> – das Wetter spielt „Wer bin ich?“ und verliert selbst den Überblick. Jacke an. Jacke aus. Kaffee bleibt.
</td>
```

**Hinweis:**
- Der Link bleibt klickbar.
- Der Screenreader liest den `aria-label`-Text, nicht den sichtbaren Inhalt.
- Aktualisierungen des sichtbaren Texts müssen auch im `aria-label` gepflegt werden.

### 2. Gesamten Satz als Link gestalten

Wenn der gesamte Satz klickbar sein darf, sollte der komplette Text in ein `<a>`-Tag eingebunden werden.

```html
<a href="..." target="_blank" style="text-decoration: none; color: inherit;">
  Heute Sonne, morgen Regen, übermorgen <span style="color: blue;">Schneesturm mit Saharastaub</span> – das Wetter spielt „Wer bin ich?“ und verliert selbst den Überblick. Jacke an. Jacke aus. Kaffee bleibt.
</a>
```

**Hinweis:**
- Der gesamte Text wird als ein Link behandelt.
- Für Screenreader-Nutzer ergibt sich ein einheitliches, flüssiges Leseerlebnis.
- Der gesamte Abschnitt wird klickbar, auch die nicht explizit verlinkten Teile.

### 3. Kontextübergabe mit `aria-describedby`

Erweiterung des Links um eine Beschreibung mit `aria-describedby`, die Screenreader beim Fokussieren des Links zusätzlich vorlesen.

```html
<p id="link-description" hidden>
  Schneesturm mit Saharastaub – das Wetter spielt „Wer bin ich?“ und verliert selbst den Überblick. Jacke an. Jacke aus. Kaffee bleibt.
</p>

<a href="..." target="_blank" aria-describedby="link-description">
  Schneesturm mit Saharastaub
</a>
```

**Hinweis:**
- Der Link bleibt korrekt fokussierbar.
- Der zusätzliche Kontext wird nur beim Fokussieren vorgelesen.
- Kein durchgehendes Vorlesen des gesamten Satzes.

## Empfehlungen (Wenn Mobile Screenreader relavant)

- **Auf Links im Text verzichten**, lieber separat anführen z.B. Linkliste.
- **Für Barrierefreiheit bevorzugt die gesamte Passage verlinken**, wenn es inhaltlich vertretbar ist.
- **`aria-label`-Lösung nur mit Vorsicht einsetzen**, insbesondere bei dynamischen Inhalten.
- **Immer ausgiebig auf unterschiedlichen Geräten und Screenreadern testen.**

## Weitere Hinweise

- Sehr lange `aria-label`-Texte (> 200 Zeichen) können die Performance beeinträchtigen.
- `role="text"` zur Gruppierung von Inline-Inhalten wird nicht von allen Screenreadern zuverlässig unterstützt.
- Links sollten wenn möglich nicht visuell "versteckt" oder als reine "onclick"-Events ohne `<a>`-Element umgesetzt werden.

## Quellen

- [AxessLab: Text Splitting Causes Screen Reader Problems](https://axesslab.com/text-splitting/)
- [UX StackExchange: For Screen Readers - Group of Text Items to be Read as One](https://ux.stackexchange.com/questions/125413/for-screen-readers-how-to-markup-a-group-of-text-items-to-be-read-as-one-item)
- [GitHub W3C ARIA Issue: Clarify use of aria-label](https://github.com/w3c/aria/issues/756)
