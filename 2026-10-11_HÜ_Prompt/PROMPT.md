# PROMPT — „Welche Inhalte der 3. Klasse lassen sich mit R effizienter lösen?"

**Datum:** 2026-10-11
**Fach:** Prozessmanagement (PMM), HTL Spengergasse — Wirtschaftsingenieure

---

## Prompt (der eigentliche Auftrag an die KI)

**Rolle:** Du bist erfahrener Statistik- und R-Dozent an einer HTL für
Wirtschaftsingenieure und erklärst anschaulich, praxisnah und auf Deutsch.

**Kontext:**
Ich bin Schüler im PMM-Unterricht und arbeite dort mit **R / RStudio**. In
der **3. Klasse** hatten wir folgende Inhalte (Kompetenzmodule **KM5** und
**KM6**):

- **KM5 (Wintersemester):**
  - Zufallsvariablen & Wahrscheinlichkeit (diskret/stetig, f(x) vs. F(x))
  - Diskrete Verteilungen: Binomial-, hypergeometrische und Poisson-Verteilung
  - Normalverteilung & Standardisierung (μ/σ, 68-95-99,7-Regel, z-Transformation)
  - Exponentialverteilung (Rate λ)
  - Lage- & Streumaße (Mittelwert, Median, Modus, Varianz, Standardabweichung, Spannweite)
  - Parameter vs. Schätzwerte (Erwartungstreue, Bessel-Korrektur n−1, Gesetz der großen Zahlen)
- **KM6 (Sommersemester):**
  - Zufallsstreu- & Vertrauensbereiche (Standardfehler, KI für μ und σ², t-Verteilung, χ²-Verteilung)
  - Auswertung & Darstellung von Prüfergebnissen (Histogramm, Boxplot, QQ-Plot, Streudiagramm)
  - Kennzahlen & Ausreißer (IQR, 1,5·IQR-Regel, Schiefe/Wölbung)
  - Lebensdauerverteilungen (Ausfallrate, Badewannenkurve, Weibull- & Exponentialverteilung, MTBF/MTTF)

**Aufgabe:**
Analysiere, **welche dieser Inhalte sich mit R deutlich effizienter lösen
lassen** als „zu Fuß" (Formelsammlung, Taschenrechner, Excel) — und welche
eher gleichwertig bleiben. Beantworte dabei die Frage: *Welche Inhalte der
3. Klasse lassen sich mit R effizienter lösen?*

**Anforderungen an die Antwort:**

1. **Rollen-/Themenüberblick:** Liste die Inhalte auf und markiere je Thema,
   ob R einen **großen**, **mittleren** oder **keinen** Effizienzvorteil bringt.
2. **Vergleich je Thema:** Stelle kurz *klassische Lösung (von Hand)* vs.
   *R-Lösung* gegenüber.
3. **Konkrete R-Funktionen:** Nenne die passenden Funktionen/Pakete
   (z. B. `dbinom`/`pbinom`, `pnorm`/`qnorm`, `dpois`, `phyper`, `pexp`,
   `dt`/`qt`, `qchisq`, `mean`/`sd`/`var`/`median`/`quantile`/`IQR`/`summary`,
   `t.test`, `ggplot2`, `fitdistrplus`, …).
4. **Ein lauffähiges Minimalbeispiel** pro großem Effizienzvorteil (2–4 Zeilen
   R-Code, das reproduzierbar ist).
5. **Begründung:** *Warum* ist R effizienter? (Reproduzierbarkeit, keine
   Rechen-/Tabellenfehler, Skalierung auf viele Daten, Visualisierung,
   Automatisierung.)
6. **Fazit:** eine kompakte Übersichtstabelle (Thema · Aufwand von Hand ·
   Aufwand mit R · Effizienzvorteil).
7. **Sprache:** Deutsch; Fachbegriffe mit R-Funktionsnamen ergänzen.

**Format der Ausgabe:** Markdown mit Überschriften, kurzen Absätzen,
Code-Blöcken (```r) und einer Tabelle am Ende.
