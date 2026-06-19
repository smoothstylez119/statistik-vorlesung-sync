# DIAGRAM_SVG_PROMPT

## Input

Du erhältst ein relevantes Diagramm aus einer Statistik-Seite oder die bereits extrahierten Diagrammdaten.

## Aufgabe

Entscheide, ob das Diagramm als SVG rekonstruiert werden soll. Wenn ja, erstelle eine einfache, saubere SVG-Datei, die den statistischen Inhalt transportiert.

## Regeln

- SVG soll didaktisch klar sein, nicht künstlerisch identisch.
- Verwende rekonstruierte Daten nur, wenn sie aus Tabelle, Achsen oder Beschriftungen ausreichend klar sind.
- Wenn Werte nicht klar sind, keine exakten Werte erfinden.
- Farben dürfen vereinfacht werden.
- Beschrifte Achsen und Legenden.
- Füge im SVG-Kommentar Quelle und Unsicherheit ein.

## Wann rekonstruieren?

Rekonstruieren, wenn:

- Tabelle vorhanden ist,
- Balken/Säulen eindeutig Werte zeigen,
- Kreisdiagramm relative Häufigkeiten enthält,
- Achsen und Datenpunkte klar genug sind.

Nicht rekonstruieren, wenn:

- Diagramm nur dekorativ ist,
- Werte grob skizziert und nicht lesbar sind,
- keine Achsen/Labels erkennbar sind.

## Ausgabe

```json
{
  "diagram_id": "{{DIAGRAM_ID}}",
  "decision": "reconstruct_svg|describe_only|ignore_decorative|manual_review_required",
  "reason": "",
  "data_used": [],
  "svg_filename": "assets/diagrams/{{DIAGRAM_ID}}.svg",
  "svg_code": "<svg xmlns=\"http://www.w3.org/2000/svg\" ...>...</svg>",
  "caption_markdown": "",
  "uncertainties": [],
  "confidence": "low|medium|high"
}
```

## SVG-Stil

- Nutze `viewBox`.
- Nutze Textlabels statt eingebetteter Rasterbilder.
- Keine externen Ressourcen.
- Kein JavaScript.
- Halte es PDF-kompatibel.
