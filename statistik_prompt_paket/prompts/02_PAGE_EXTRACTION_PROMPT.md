# PAGE_EXTRACTION_PROMPT

## Input

Du erhältst genau eine Seitenabbildung aus einem handschriftlichen Statistik-Skript.

Metadaten:

```yaml
source_pdf: "{{SOURCE_PDF}}"
page_index: {{PAGE_INDEX_ZERO_BASED}}
page_number_human: {{PAGE_NUMBER_HUMAN}}
previous_page_summary: "{{PREVIOUS_PAGE_SUMMARY}}"
current_section_hint: "{{CURRENT_SECTION_HINT}}"
known_notation_glossary: {{KNOWN_NOTATION_GLOSSARY_JSON}}
```

## Aufgabe

Transkribiere die Seite in eine robuste digitale Fassung, die später mit anderen Seiten zu einem großen Skript zusammengeführt werden kann.

## Vorgehen

1. Erfasse zuerst Überschriften, Nummerierungen und die Reihenfolge der Inhalte.
2. Transkribiere Fließtext sichtnah, aber mit normalisierter Rechtschreibung nur dort, wo eindeutig.
3. Setze Formeln in LaTeX.
4. Setze Tabellen als Markdown-Tabellen und zusätzlich als strukturierte `tables`-Objekte.
5. Beschreibe relevante statistische Diagramme. Extrahiere Achsen, Labels, erkennbare Werte und Aussage.
6. Markiere alles Unklare explizit.
7. Erstelle zusätzlich eine `clean_study_version`, die lesbarer ist, aber keine neuen Inhalte erfindet.

## Kritische Statistik-Symbole

Achte besonders auf diese Verwechslungsgefahren:

- \(h_j\) vs. \(n_j\) vs. \(k_j\)
- \(f_j\) vs. \(t_j\)
- \(x_j\) vs. \(x_i\)
- \(n\) vs. \(m\) vs. \(N\)
- \(\sum\) Grenzen: \(j=1\), \(i=1\), \(m\), \(n\)
- \(\sigma\) vs. \(s\), \(\mu\) vs. \(u\), \(\Omega\) vs. O
- \(\cap\) vs. \(\cup\), \(<\) vs. \(\le\), \(=\) vs. \(:=\)
- Dezimalkomma vs. Punkt: deutsche Notation bevorzugt Dezimalkomma in Text/Tabellen; LaTeX darf `1{,}7` nutzen.

## Ausgabe

Gib **zuerst** eine Markdown-Seitenfassung aus und danach ein JSON-Objekt. Keine zusätzlichen Erklärungen außerhalb dieser beiden Blöcke.

### Markdown-Block

```markdown
---
source_pdf: "{{SOURCE_PDF}}"
page_number: {{PAGE_NUMBER_HUMAN}}
page_id: "page_{{PAGE_NUMBER_PADDED}}"
status: "draft_extracted"
overall_confidence: "high|medium|low"
requires_human_review: true|false
---

# Seite {{PAGE_NUMBER_HUMAN}}

## Sichtnahe Transkription

...

## Formeln

...

## Tabellen

...

## Relevante Diagramme / Grafiken

...

## Bereinigte Studienfassung

...

## Unsicherheiten / Prüfbedarf

...
```

### JSON-Block

```json
{
  "page_id": "page_{{PAGE_NUMBER_PADDED}}",
  "source_pdf": "{{SOURCE_PDF}}",
  "page_number": {{PAGE_NUMBER_HUMAN}},
  "detected_section": "",
  "overall_confidence": "high|medium|low",
  "requires_human_review": true,
  "headings": [],
  "raw_transcription": "",
  "clean_study_version": "",
  "formulas": [
    {
      "formula_id": "page_{{PAGE_NUMBER_PADDED}}_formula_001",
      "latex": "",
      "visible_reading": "",
      "meaning_if_stated": "",
      "confidence": "high|medium|low",
      "uncertainties": []
    }
  ],
  "tables": [
    {
      "table_id": "page_{{PAGE_NUMBER_PADDED}}_table_001",
      "title": "",
      "markdown": "",
      "columns": [],
      "rows": [],
      "validation_checks_suggested": [],
      "confidence": "high|medium|low",
      "uncertainties": []
    }
  ],
  "diagrams": [
    {
      "diagram_id": "page_{{PAGE_NUMBER_PADDED}}_diagram_001",
      "type": "bar|column|pie|scatter|line|concept_map|flowchart|other",
      "is_statistically_relevant": true,
      "description": "",
      "axes": {"x": "", "y": ""},
      "data_points_or_values": [],
      "reconstruct_as_svg": true,
      "svg_data_confidence": "high|medium|low",
      "uncertainties": []
    }
  ],
  "inferred_corrections": [
    {
      "visible_reading": "",
      "normalized_reading": "",
      "reason": "",
      "confidence": "high|medium|low",
      "requires_human_review": true
    }
  ],
  "uncertainties": [
    {
      "location": "",
      "issue": "",
      "candidates": [],
      "severity": "low|medium|high",
      "requires_human_review": true
    }
  ]
}
```
