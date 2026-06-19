# SECTION_CONSISTENCY_PROMPT

## Input

Du erhältst 5-8 kanonische Seiten als Markdown/JSON.

## Aufgabe

Prüfe Konsistenz über mehrere Seiten. Schreibe keine neue Vorlesung, sondern finde Brüche, Fehler und nützliche Querverbindungen.

## Prüfe

- Kapitelnummern und Reihenfolge.
- Wiederkehrende Begriffe und Definitionen.
- Notation: \(x_j\), \(f_j\), \(h_j\), \(n\), \(m\), \(\Omega\), etc.
- Tabellen, die auf früheren Seiten basieren.
- Diagramme, die aus Tabellen rekonstruiert wurden.
- Widersprüche zwischen Definition und späterer Verwendung.
- Seiten, die vermutlich fehlen oder doppelt sind.

## Ausgabe

```json
{
  "section_id": "{{SECTION_ID}}",
  "pages": ["page_001", "page_002"],
  "section_title": "",
  "consistency_status": "consistent|minor_warnings|major_issues|manual_review_required",
  "notation_glossary_updates": [
    {
      "symbol": "h_j",
      "meaning": "relative Häufigkeit der Ausprägung x_j",
      "source_pages": [],
      "confidence": "high|medium|low"
    }
  ],
  "issues": [
    {
      "location": "",
      "issue": "",
      "suggested_resolution": "",
      "confidence": "low|medium|high",
      "requires_human_review": true
    }
  ],
  "cross_references": [
    {
      "from_page": "",
      "to_page": "",
      "relation": "definition_used|table_used|diagram_derived|example_continued|other",
      "note": ""
    }
  ],
  "section_summary_for_context": ""
}
```
