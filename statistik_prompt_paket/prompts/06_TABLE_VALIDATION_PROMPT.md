# TABLE_VALIDATION_PROMPT

## Input

Du erhältst eine aus einer Statistik-Seite extrahierte Tabelle plus optional das Seitenbild oder den Tabellencrop.

## Aufgabe

Prüfe die Tabelle fachlich und rechnerisch, ohne sichtbare Werte stillschweigend zu ändern.

## Typische Statistik-Checks

Für Häufigkeitstabellen:

- \(\sum_{j=1}^{m} f_j = n\)
- \(h_j = \frac{f_j}{n}\)
- \(\sum_{j=1}^{m} h_j = 1\)
- relative Häufigkeiten in Prozent: Summe ca. 100 %
- Anzahl unterschiedlicher Ausprägungen \(m\)
- Stichprobenumfang \(n\)

Für Kontingenztabellen:

- Zeilensummen und Spaltensummen prüfen.
- Gesamtsumme prüfen.
- Relative Häufigkeiten eindeutig als zeilen-, spalten- oder gesamtbezogen markieren.

## Konfliktregel

Wenn ein Wert sichtbar anders aussieht als der rechnerisch erwartete Wert:

- sichtbaren Wert behalten,
- Plausibilitätskonflikt melden,
- vorgeschlagene Korrektur nur als Vorschlag markieren.

## Ausgabe

```json
{
  "table_id": "{{TABLE_ID}}",
  "validation_status": "valid|valid_with_warnings|invalid|manual_review_required",
  "checks": [
    {
      "check": "sum_f_j_equals_n",
      "expected": "",
      "observed": "",
      "result": "pass|fail|not_applicable|uncertain",
      "notes": ""
    }
  ],
  "suggested_corrections": [
    {
      "cell": "",
      "visible_value": "",
      "mathematically_expected_value": "",
      "recommendation": "keep_visible|correct_if_human_confirms|correct_auto_high_confidence",
      "reason": "",
      "confidence": "low|medium|high"
    }
  ],
  "canonical_table_markdown": "",
  "canonical_table_csv": ""
}
```
