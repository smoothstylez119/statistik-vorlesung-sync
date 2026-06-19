# Beispiel: Häufigkeitstabelle aus einer handschriftlichen Statistik-Seite

Dieses Beispiel zeigt, wie eine Seite mit diskreten Merkmalen und Häufigkeitstabelle digitalisiert werden sollte.

## Sichtnahe Transkription

Bei der Untersuchung von Häufigkeitsverteilungen unterscheidet man zwischen diskreten und stetigen Merkmalen.

### 1 Diskrete Merkmale

Betrachte das Merkmal \(X\) aus Beispiel 2: \(j = 1, \ldots, m\).

| \(j\) | \(x_j\) (Ausprägung) | \(f_j\) (abs. Häufigk.) | \(h_j\) (rel. H.) |
|---:|---:|---:|---:|
| 1 | 1,0 | 4 | 0,2 |
| 2 | 1,3 | 3 | 0,15 |
| 3 | 1,7 | 6 | 0,3 |
| 4 | 2,0 | 3 | 0,15 |
| 5 | 2,3 | 2 | 0,1 |
| 6 | 2,7 | 1 | 0,05 |
| 7 | 3,0 | 1 | 0,05 |
| Σ | — | 20 | 1 |

\(f_j\): absolute Häufigkeit von \(x_j\)

\[
\sum_{j=1}^{m} f_j = n
\]

\(h_j\): relative Häufigkeit von \(x_j\)

\[
h_j := \frac{f_j}{n}
\]

mit

\[
\sum_{j=1}^{m} h_j = 1
\]

Anteile summieren sich zu 1 \(\hat{=}\) 100 %.

## Validierung

- \(\sum f_j = 4+3+6+3+2+1+1 = 20\) ✓
- \(h_j = f_j/20\) für alle Zeilen ✓
- \(\sum h_j = 1\) ✓

## Unsicherheiten

- Keine, sofern die Werte im Seitenbild klar lesbar sind.
