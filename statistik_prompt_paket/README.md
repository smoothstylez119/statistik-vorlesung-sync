# Prompt-Paket: Intelligente Digitalisierung handschriftlicher Statistik-Vorlesungen

Ziel dieses Pakets ist eine robuste Pipeline für handschriftliche Statistik-PDFs: aus Seitenbildern entstehen prüfbare Markdown-/LaTeX-Transkriptionen, validierte Tabellen, rekonstruierbare Diagramme/SVGs, ein zusammenführbares Skript und daraus ein finales PDF.

Die Prompts sind bewusst **source-first** formuliert: Das Modell soll den sichtbaren Inhalt digitalisieren, aber statistischen Kontext nutzen, um wahrscheinliche OCR-/Lesefehler zu erkennen. Korrekturen dürfen nicht heimlich passieren, sondern werden als `inferred_corrections` und `uncertainties` dokumentiert.

## Empfohlene Modellarchitektur

### Minimalvariante
1. **Vision-Extractor**: transkribiert je eine Seite als Markdown/JSON.
2. **Vision-Reviewer**: sieht dieselbe Seite plus Transkription und gibt nur Fehler/Unsicherheiten aus.
3. **Assembler**: merged geprüfte Seiten in ein Gesamtskript.

### Qualitätsvariante mit viel Budget / kaum Rate Limits
1. **Extractor A**: unabhängige Seitentranskription.
2. **Extractor B**: unabhängige Seitentranskription mit leicht anderem Prompt.
3. **Vision-Adjudicator**: vergleicht A/B gegen das Seitenbild und erstellt die kanonische Version.
4. **Math/Table Validator**: prüft Formeln, Tabellen, Summen, relative Häufigkeiten, Achsenbeschriftungen.
5. **Diagram-Reconstructor**: baut relevante Diagramme als SVG, wenn die Daten rekonstruierbar sind.
6. **Section Consistency Checker**: prüft 5-8 Seiten zusammen auf Notation, Kapitelstruktur und Widersprüche.
7. **Final Assembler**: erstellt `full_script.md`, `formelsammlung.md`, `glossar.md`, `unsicherheiten.md` und optional PDF-Input.

## Chunking

- **Transkription:** 1 Seite pro Call.
- **Review:** 1 Seite pro Call.
- **Diagramm-/Tabellen-Sonderfall:** Tabelle oder Diagramm zusätzlich als Crop analysieren, wenn wichtig oder unklar.
- **Konsistenzprüfung:** 5-8 Seiten pro Call.
- **Kapitelzusammenfassung:** 20-40 Seiten pro Call, aber nur aus bereits validierten Seiten.

## Empfohlenes Ausgabeformat

```text
statistik_digitalisiert/
  input/
  pages_png/
    page_001.png
  page_outputs/
    page_001.canonical.md
    page_001.canonical.json
  reviews/
    page_001.review.json
  assets/
    diagrams/
      page_016_diagram_001.svg
  sections/
    section_001_consistency.md
  final/
    full_script.md
    full_script.pdf
    formelsammlung.md
    glossar.md
    unsicherheiten.md
    manifest.json
```

## Zentrale Prinzipien

1. **Keine Erfindungen.** Fehlende oder unleserliche Inhalte bleiben markiert.
2. **Sichtbare Quelle schlägt mathematische Erwartung.** Wenn die Seite etwas zeigt, was mathematisch komisch wirkt, wird es erhalten und geflaggt.
3. **Kontext darf helfen, aber nicht verdecken.** Kontextkorrekturen müssen dokumentiert werden.
4. **Formeln nicht umformen.** Digitalisierung ja, mathematische Neudarstellung nur in `clean_study_version` und nur transparent.
5. **Tabellen validieren.** Summen, relative Häufigkeiten und offensichtliche Rechenchecks durchführen, aber Werte nicht still ändern.
6. **Diagramme rekonstruieren, wenn möglich.** Wenn Tabelle vorhanden, Diagramm aus Tabelle generieren. Wenn nur Skizze vorhanden, beschreiben und Unsicherheit markieren.
