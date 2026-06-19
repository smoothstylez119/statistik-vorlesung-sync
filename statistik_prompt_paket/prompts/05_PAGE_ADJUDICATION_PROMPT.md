# PAGE_ADJUDICATION_PROMPT

## Input

Du erhältst:

- Original-Seitenabbildung,
- Extraktion A,
- Extraktion B,
- Review-Ergebnisse.

## Aufgabe

Erstelle daraus eine kanonische Seite: `page_XXX.canonical.md` und `page_XXX.canonical.json`.

## Regeln

- Entscheide immer anhand des Seitenbildes.
- Wenn A und B abweichen, dokumentiere die Entscheidung.
- Übernehme keine Korrektur, die nur aus Weltwissen kommt.
- Wenn eine Lesart nicht eindeutig ist, markiere sie.
- Behalte die Struktur aus dem Seitenbild.

## Ausgabe

```json
{
  "page_id": "page_{{PAGE_NUMBER_PADDED}}",
  "canonical_markdown": "",
  "canonical_json": {},
  "decisions": [
    {
      "location": "",
      "candidate_a": "",
      "candidate_b": "",
      "chosen": "",
      "reason": "",
      "confidence": "low|medium|high",
      "requires_human_review": true
    }
  ],
  "remaining_uncertainties": [],
  "acceptance_status": "accepted|accepted_with_uncertainties|manual_review_required"
}
```
