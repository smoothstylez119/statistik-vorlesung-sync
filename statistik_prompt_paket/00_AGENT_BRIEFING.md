# Agent-Briefing

Du baust/steuerst eine Pipeline zur intelligenten Digitalisierung handschriftlicher Statistik-Vorlesungsnotizen.

## Ziel

Aus handschriftlichen PDF-Seiten sollen entstehen:

- prüfbare Markdown-Transkriptionen pro Seite,
- LaTeX-Formeln,
- Markdown-/CSV-Tabellen,
- relevante Diagramme als Beschreibung oder SVG-Rekonstruktion,
- ein großes zusammenführbares Skript,
- ein Lernskript mit Formelsammlung, Glossar und Zusammenfassung,
- ein finales PDF oder PDF-fähiger Input.

## Nicht-Ziel

- Keine freie inhaltliche Ergänzung.
- Keine erfundenen Formeln.
- Keine stillen mathematischen Korrekturen.
- Keine hübsche Zusammenfassung, die die Originalnotizen ersetzt.

## Goldene Regel

Die Pipeline darf aus Kontext eine wahrscheinlich richtige Lesart ableiten, aber jede Ableitung muss nachvollziehbar sein:

```json
{
  "visible_reading": "h? = f? / n",
  "normalized_reading": "h_j = f_j / n",
  "reason": "Auf derselben Seite wird h_j als relative Häufigkeit definiert und f_j als absolute Häufigkeit; Index j ist konsistent mit der Tabelle.",
  "confidence": "high",
  "requires_human_review": false
}
```

## Empfohlene Calls pro Seite

1. Render page as image, ideally 300 DPI or high enough for handwriting.
2. Run `PAGE_EXTRACTION_PROMPT`.
3. Optional: run independent `PAGE_EXTRACTION_PROMPT_VARIANT_B`.
4. Run `PAGE_REVIEW_PROMPT` with image + extracted page output.
5. Run `PAGE_ADJUDICATION_PROMPT` if there are multiple candidates.
6. Run `TABLE_VALIDATION_PROMPT` for each table.
7. Run `DIAGRAM_SVG_PROMPT` for each relevant diagram.
8. Save canonical `.md` and `.json`.

## Temperature / Sampling

- Extraction: low temperature, e.g. 0-0.2.
- Independent second extraction: 0.2-0.4 is okay to expose alternative readings.
- Review/adjudication: 0-0.1.
- Learning summary: 0.2-0.5, but only from validated canonical sources.

## Quality Gates

A page is `accepted` only when:

- all visible headings and main text blocks are represented,
- all formulas are either transcribed or marked unclear,
- all relevant tables are represented,
- relevant diagrams are described or reconstructed,
- all uncertain symbols/numbers are listed,
- review has no unresolved high-severity issue.
