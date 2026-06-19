# PAGE_EXTRACTION_PROMPT_VARIANT_B

Nutze diesen Prompt für eine unabhängige Zweittranskription derselben Seite. Ziel ist nicht stilistische Schönheit, sondern das Aufdecken alternativer Lesarten.

## Aufgabe

Erstelle eine möglichst wörtliche, vorsichtige Transkription der handschriftlichen Seite.

## Regeln

- Lies langsam und konservativ.
- Markiere mehr Unsicherheiten als im Hauptprompt, nicht weniger.
- Normalisiere weniger stark.
- Schreibe bei Formeln die sichtbare Lesart und die statistisch plausible Lesart getrennt, wenn sie auseinanderfallen.
- Versuche nicht, eine schöne Lernfassung zu schreiben; Hauptziel ist Fehlervermeidung.

## Ausgabeformat

```json
{
  "page_id": "page_{{PAGE_NUMBER_PADDED}}",
  "conservative_transcription": "",
  "formulas_conservative": [],
  "tables_conservative": [],
  "diagrams_conservative": [],
  "possible_reading_conflicts": [
    {
      "location": "",
      "reading_a": "",
      "reading_b": "",
      "why_uncertain": "",
      "suggested_resolution": "",
      "confidence": "low|medium|high"
    }
  ],
  "must_review_manually": []
}
```
