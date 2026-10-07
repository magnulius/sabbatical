# Sabbatical-Planer

Ein Planungstool für einen Freizeitausgleich (FZA), umgangssprachlich Sabbatical. Du sparst in einer Ansparphase Zeitguthaben an und nimmst es danach am Stück frei. Der Planer rechnet sofort mit und zeigt, ob dein Plan aufgeht.

**Live:** `https://<github-name>.github.io/sabbatical-planer/`

## Was der Planer kann

- **Feste Werte:** Wochenstunden, Stundenlohn und Arbeitstage aus deinem Vertrag bzw. aus Personio
- **Ansparphase planen:** Zeitraum, Urlaubstage und Krankheitspuffer
- **Übergang:** Urlaubstage zwischen Ansparphase und FZA, die die freie Zeit verlängern
- **Freizeitausgleich:** 1 bis 3 Kalendermonate oder ein eigenes Enddatum
- **Stellschrauben:** bezahlte Wochenstunden in der Ansparphase und im FZA per Schieberegler, mit Anzeige, ab wann der Plan aufgeht und wo die Gehaltsuntergrenze liegt
- **Ausrechnen lassen:** bezahlte Stunden in Ansparphase oder FZA, Beginn der Ansparphase oder Ende des FZA
- **Szenarien:** bis zu drei Varianten nebeneinander vergleichen
- **Kalender und Gehaltsverlauf:** alle Phasen im Monatskalender, Bruttogehalt pro Monat als Diagramm
- **Rechenweg:** jede Berechnung Schritt für Schritt mit den eigenen Zahlen
- **Teilen:** Zusammenfassung kopieren oder die komplette Planung als Link weitergeben

## So wird gerechnet

1. **Benötigtes Guthaben** = (Kalendertage des FZA ÷ 7) × bezahlte Wochenstunden im FZA
2. **Guthaben pro Anspartag** = (vertragliche − bezahlte Wochenstunden) ÷ Arbeitstage pro Woche
3. **Anspartage** = Arbeitstage der Ansparphase − Feiertage − 24.12./31.12. − Urlaub − Krankheitspuffer
4. **Angespartes Guthaben** = Anspartage × Guthaben pro Anspartag
5. **Saldo** = angespartes − benötigtes Guthaben
6. **Gehaltsuntergrenze:** bezahlte Wochenstunden × 4,33 × Stundenlohn muss in der Ansparphase und im FZA jeweils mindestens 633 € pro Monat ergeben

In der Ansparphase wird so weit reduziert, dass ein Guthaben X entsteht. Dieses Guthaben wird im FZA verteilt: Je weniger bezahlte Wochenstunden im FZA, desto mehr Tage reicht X.

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

## Entwicklung

Der Planer bleibt bewusst **eine einzige Datei** (`index.html`), damit das Veröffentlichen einfach bleibt. Innen ist das Skript in Abschnitte gegliedert:

| Abschnitt                  | Inhalt                                                                                                                                                                   |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1. Kern (`#region core`)   | Regeln (`CONFIG`), Datumsfunktionen, Feiertage, Berechnung `compute(plan, heute)`, Ausrechnen, Teilen-Kodierung, Migration. Reine Funktionen ohne Zugriff auf die Seite. |
| 2. Zustand und Verdrahtung | Startwerte, Laden/Speichern, Eingabefelder verbinden, Klick-Router                                                                                                       |
| 3. Zustand                 | Hilfsfunktionen für Planung und Beispielwerte                                                                                                                            |
| 4. Bausteine               | Icons, Datumsfeld, Datumsauswahl                                                                                                                                         |
| 5. Darstellung             | alle `render…`-Funktionen                                                                                                                                                |
| 6. Navigation              | Tabs, Sprünge, Meldungen                                                                                                                                                 |
| 7. Aktionen                | Klick-Handler, über einen zentralen Router verteilt                                                                                                                      |
| 8. Szenarien und Teilen    | Speichern von Varianten, Link-Teilen                                                                                                                                     |

Regeln wie die Gehaltsuntergrenze oder die maximale FZA-Dauer stehen in `CONFIG` am Anfang des Kerns.

### Tests

```bash
npm install
npx playwright install chromium
npm test                # Kern, Rechenergebnisse und Abläufe
npm run test:visual     # Bildvergleich (lokal, braucht Python mit Pillow)
```

- `tests/core.test.mjs`: Unit-Tests für den Kern (Feiertage, Kalenderwochen, Monatsgrenzen, Berechnung, Link-Kodierung, Migration)
- `tests/golden.mjs`: hält die sichtbaren Ergebnisse von 14 Planungsfällen fest (`tests/golden.json`)
- `tests/interaction.mjs`: klickt die wichtigsten Abläufe durch
- `tests/visual.mjs`: vergleicht Bildschirmfotos mit `tests/visual-ref/`

Ändert sich ein Ergebnis gewollt, die Referenz mit `npm run golden:update` bzw. `npm run visual:update` neu schreiben und die Änderung prüfen.

Bei jedem Push laufen die Tests automatisch über GitHub Actions (`.github/workflows/test.yml`).
