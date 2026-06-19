# FINAL_ASSEMBLY_PROMPT

## Input

Du erhältst alle akzeptierten kanonischen Seiten, Diagramm-SVGs, Tabellen, Formelobjekte, Glossar-Updates und Unsicherheiten.

## Aufgabe

Erstelle ein zusammenhängendes digitales Skript, das aus den Originalseiten nachvollziehbar ist und als PDF gerendert werden kann.

## Regeln

- Reihenfolge der Seiten beibehalten.
- Seitenmarker erhalten: `<!-- source: page_013 -->`.
- Keine neuen Fachinhalte hinzufügen.
- Keine ungeprüften Korrekturen übernehmen.
- Unsicherheiten zentral sammeln.
- Tabellen und Formeln sauber setzen.
- SVGs an passender Stelle einbetten.

## Ausgabe-Dateien

Erzeuge Inhalte für:

1. `final/full_script.md`
2. `final/formelsammlung.md`
3. `final/glossar.md`
4. `final/unsicherheiten.md`
5. `final/manifest.json`

## full_script.md Struktur

```markdown
---
title: "Digitalisiertes Statistik-Skript"
source: "{{SOURCE_COLLECTION_NAME}}"
status: "machine_transcribed_with_review"
---

# Digitalisiertes Statistik-Skript

> Hinweis: Dieses Skript wurde aus handschriftlichen Vorlesungsnotizen transkribiert. Unsichere Stellen sind markiert.

<!-- source: page_001 -->

# ...
```

## manifest.json

```json
{
  "project": "",
  "source_pdfs": [],
  "created_at": "",
  "pages_total": 0,
  "pages_accepted": 0,
  "pages_manual_review_required": 0,
  "diagrams_reconstructed": 0,
  "tables_extracted": 0,
  "formulas_extracted": 0,
  "known_limitations": [],
  "rendering_recommendation": "pandoc/typst/quarto"
}
```
