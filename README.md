# Sabbatical-Planer

Ein Planungstool für einen Freizeitausgleich (FZA), umgangssprachlich Sabbatical. Du sparst in einer Ansparphase Zeitguthaben an und nimmst es danach am Stück frei. Der Planer rechnet sofort mit und zeigt, ob dein Plan aufgeht.

**Live:** `https://<github-name>.github.io/sabbatical-planer/`

## Was der Planer kann

- **Feste Werte:** Wochenstunden, Stundenlohn und Arbeitstage aus deinem Vertrag bzw. aus Personio
- **Ansparphase planen:** Zeitraum, Urlaubstage und Krankheitspuffer
- **Übergang:** Urlaubstage zwischen Ansparphase und FZA, die die freie Zeit verlängern
- **Freizeitausgleich:** 1 bis 3 Kalendermonate oder ein eigenes Enddatum
- **Stellschraube:** bezahlte Wochenstunden per Schieberegler, mit Anzeige, ab wann der Plan aufgeht und wo die Gehaltsuntergrenze liegt
- **Ausrechnen lassen:** bezahlte Stunden, Beginn der Ansparphase oder Ende des FZA
- **Szenarien:** bis zu drei Varianten nebeneinander vergleichen
- **Kalender und Gehaltsverlauf:** alle Phasen im Monatskalender, Bruttogehalt pro Monat als Diagramm
- **Rechenweg:** jede Berechnung Schritt für Schritt mit den eigenen Zahlen
- **Teilen:** Zusammenfassung kopieren oder die komplette Planung als Link weitergeben

## So wird gerechnet

1. **Benötigtes Guthaben** = (Kalendertage des FZA ÷ 7) × vertragliche Wochenstunden
2. **Guthaben pro Anspartag** = (vertragliche − bezahlte Wochenstunden) ÷ Arbeitstage pro Woche
3. **Anspartage** = Arbeitstage der Ansparphase − Feiertage − 24.12./31.12. − Urlaub − Krankheitspuffer
4. **Angespartes Guthaben** = Anspartage × Guthaben pro Anspartag
5. **Saldo** = angespartes − benötigtes Guthaben
6. **Gehaltsuntergrenze:** bezahlte Wochenstunden × 4,33 × Stundenlohn muss mindestens 633 € pro Monat ergeben

### Annahmen

- Gesetzliche Feiertage in Berlin, berechnet für das aktuelle Jahr und die zehn folgenden Jahre
- Heiligabend und Silvester sind halbe Arbeitstage. Sie werden nicht als Anspartage gezählt, um konservativ zu planen.
- Der FZA dauert höchstens 3 Kalendermonate.
- Beispieldaten werden aus dem aktuellen Datum des Browsers berechnet und liegen immer in der Zukunft.

## Datenschutz

- Der Planer ist eine einzelne statische HTML-Datei. Er schickt keine Eingaben an einen Server.
- Eingaben werden nur im eigenen Browser gespeichert (`localStorage`) und sind für niemanden sonst sichtbar.
- **Teilen per Link:** Die Planung steht im Teil der Adresse hinter dem `#`. Dieser Teil wird nicht an GitHub übertragen. Der Link enthält aber alle Werte, auch den Stundenlohn, und erlaubt damit Rückschlüsse auf das Gehalt. Teile ihn nur mit Personen, die das sehen dürfen.
- Externe Verbindung: Schriftarten werden von Google Fonts geladen. Ohne diese Verbindung greift automatisch eine Systemschrift.

## Veröffentlichen mit GitHub Pages

1. Die Datei `index.html` in das oberste Verzeichnis des Repositorys legen.
2. **Settings** → **Pages** → **Deploy from a branch** wählen, Branch `main`, Ordner `/ (root)`, dann **Save**.
3. Nach ein bis zwei Minuten ist der Planer unter der oben genannten Adresse erreichbar.

**Aktualisieren:** neue `index.html` hochladen und die alte überschreiben. Es gibt keinen Build-Schritt und keine Abhängigkeiten.

## Hinweis

Der Planer ist eine Planungshilfe ohne Gewähr. Verbindlich sind Arbeitsvertrag, Betriebs- oder Dienstvereinbarung und die Abstimmung mit der Personalabteilung.
