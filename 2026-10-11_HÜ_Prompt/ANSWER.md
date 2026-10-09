# ANSWER — „Welche Inhalte der 3. Klasse lassen sich mit R effizienter lösen?"

**Datum:** 2026-10-11
**Fach:** Prozessmanagement (PMM) — Wirtschaftsingenieure
**Prompt:** siehe [`PROMPT.md`](PROMPT.md)

---

## Kurzantwort

Fast der **gesamte** Stoff der 3. Klasse (KM5 + KM6) lässt sich mit R
effizienter lösen. Den **größten** Vorteil bringen jene Themen, die von Hand
**Tabellen, Näherungen oder viele Rechenschritte** erfordern:

- **Verteilungen** (Binomial, hypergeometrisch, Poisson, Normal, Exponential)
- **Vertrauens- und Streubereiche** (t-, χ²-Verteilung)
- **Kennzahlen & Ausreißeranalyse** bei vielen Daten
- **Visualisierung von Prüfergebnissen** (Histogramm, Boxplot, QQ-Plot)
- **Lebensdauerverteilungen** (Weibull/Exponential, MTBF/MTTF)

Weniger großer, aber trotzdem spürbarer Vorteil: das reine **Nachschlagen
einfacher Lage-/Streumaße** (Mittelwert, Median) und die **theoretischen
Grundlagen** (f(x) vs. F(x), Erwartungstreue) — hier hilft R vor allem beim
**Verstehen durch Simulation**, nicht beim „Ausrechnen".

---

## 1. Themenüberblick mit Effizienzvorteil

| Inhalt (Klasse 3) | Effizienzvorteil mit R |
|---|---|
| Binomial-, hypergeometrische, Poisson-Verteilung | **groß** (Tabelle/Formel → 1 Zeile Code) |
| Normalverteilung & z-Transformation | **groß** (`pnorm`/`qnorm` statt Tabelle) |
| Exponentialverteilung | **groß** (`pexp`/`qexp`) |
| Lage- & Streumaße | **mittel** (bei wenigen Werten gleich; bei vielen Daten groß) |
| Parameter vs. Schätzwerte, Gesetz der großen Zahlen | **mittel–groß** (Simulation) |
| Vertrauensbereiche (SE, KI für μ, KI für σ²) | **groß** (`t.test`, `qt`, `qchisq`) |
| Prüfergebnisse darstellen (Histogramm, Boxplot, QQ) | **groß** (`ggplot2`) |
| Kennzahlen & Ausreißer (IQR, 1,5·IQR) | **groß** bei großen Datensätzen |
| Lebensdauerverteilungen (Weibull, MTBF/MTTF) | **groß** (`fitdistrplus`) |
| Verteilungen verstehen (f(x) vs. F(x)) | **mittel** (Simulation als Lernhilfe) |

---

## 2. Vergleich je Thema (von Hand vs. R)

### 2.1 Diskrete Verteilungen (Binomial, hypergeometrisch, Poisson)
- **Von Hand:** Formel + Binomialkoeffizient + Wahrscheinlichkeitstabelle;
  für kumulierte Werte alle Einzelwahrscheinlichkeiten aufsummieren.
- **Mit R:** eine Funktion liefert Dichte (d), Verteilung (p), Quantil (q) oder
  Zufallszahlen (r).

```r
# Binomial: P(X <= 3) bei n = 10, p = 0.4
pbinom(3, size = 10, prob = 0.4)

# Poisson: P(X = 2) bei lambda = 3
dpois(2, lambda = 3)

# Hypergeometrisch: P(X = 1), N = 20, K = 5, n = 4
dhyper(1, m = 5, n = 15, k = 4)
```

### 2.2 Normalverteilung & z-Transformation
- **Von Hand:** z-Wert berechnen, dann die **Tabelle** der Standardnormal-
  verteilung ablesen (Interpolation zwischen Zeilen/Spalten).
- **Mit R:** `pnorm`/`qnorm` liefern exakte Werte ohne Tabelle.

```r
# P(X < 70) bei mu = 60, sigma = 8
pnorm(70, mean = 60, sd = 8)

# 97,5%-Quantil (z = 1,96)
qnorm(0.975)   # -> 1.959964
```

### 2.3 Exponentialverteilung
- **Von Hand:** e-Funktion potenzieren, λ·t geschickt einsetzen.
- **Mit R:** `pexp`/`qexp`.

```r
pexp(2, rate = 0.5)   # P(T <= 2) bei lambda = 0.5
```

### 2.4 Lage- & Streumaße
- **Von Hand:** jede Abweichung quadrieren, summieren, durch n bzw. n−1 teilen.
- **Mit R:** `summary`/`mean`/`sd`/`var`/`median`/`quantile`/`IQR`.

```r
x <- c(12, 15, 9, 22, 17, 15, 30)
summary(x)          # Übersicht inkl. Quartile
sd(x); var(x)       # Standardabweichung, Varianz
IQR(x)              # Interquartilsabstand
```

### 2.5 Parameter vs. Schätzwerte / Gesetz der großen Zahlen
- **Von Hand:** nicht praktikabel (bräuchte sehr viele Stichproben).
- **Mit R:** Simulation macht Erwartungstreue und Bessel-Korrektur sichtbar.

```r
set.seed(1)
mittel <- replicate(10000, mean(rnorm(20, mean = 100, sd = 15)))
mean(mittel)   # nahe 100 -> Erwartungstreue
```

### 2.6 Vertrauens- und Streubereiche (KM6)
- **Von Hand:** t- bzw. χ²-Tabelle ablesen, dann CI-Formel einsetzen.
- **Mit R:** `t.test` gibt das CI direkt aus; `qt`/`qchisq` liefern Quantile.

```r
x <- c(98, 102, 97, 105, 101, 99)
t.test(x)$conf.int          # KI für mu (t-Verteilung)

qchisq(c(0.025, 0.975), df = 5)   # Quantile für das KI von sigma^2
```

### 2.7 Prüfergebnisse darstellen & Ausreißer
- **Von Hand:** Excel-Diagramme klicken, QQ-Plot kaum möglich.
- **Mit R:** `ggplot2` erzeugt reproduzierbare Grafiken; Ausreißer via IQR-Regel.

```r
library(ggplot2)
ggplot(daten, aes(x = wert)) +
  geom_histogram(bins = 15) +
  geom_boxplot() +
  theme_minimal()
```

```r
q1 <- quantile(x, 0.25); q3 <- quantile(x, 0.75); iqr <- IQR(x)
x[x < q1 - 1.5 * iqr | x > q3 + 1.5 * iqr]   # Ausreißer (1,5·IQR-Regel)
```

### 2.8 Lebensdauerverteilungen
- **Von Hand:** Weibull-Ausfallwahrscheinlichkeit nur über Formel/Näherung.
- **Mit R:** `pweibull`/`dweibull` und Parameterschätzung mit `fitdistrplus`.

```r
pweibull(1000, shape = 2, scale = 1200)   # F(t) der Weibull-Verteilung

library(fitdistrplus)
fitdist(x, "weibull")                     # beta/eta schätzen -> MTBF ableiten
```

---

## 3. Warum ist R effizienter?

1. **Kein Tabellen-Nachschlagen / keine Interpolation** — `pnorm`, `qt`,
   `qchisq` liefern exakte Werte.
2. **Reproduzierbarkeit** — Skripte statt Klicks: gleiche Daten → gleiches
   Ergebnis, jederzeit nachvollziehbar.
3. **Skalierung** — dieselbe Zeile Code rechnet für 10 oder 100.000 Werte.
4. **Methoden, die von Hand nicht machbar sind** — Simulation (Gesetz der
   großen Zahlen, Erwartungstreue), Parameterschätzung (fitdistrplus).
5. **Visualisierung** — Histogramm, Boxplot, QQ-Plot, Streudiagramm mit
   `ggplot2` in wenigen Zeilen.
6. **Weniger Rechenfehler** — kein manuelles Quadrieren/Summieren von Hand.
7. **Automatisierung** — wiederkehrende Auswertungen laufen per Skript,
   z. B. für Prüfreihen oder Produktionsdaten (`read.csv` + Pipeline).

---

## 4. Fazit — Übersichtstabelle

| Thema (Klasse 3) | Aufwand von Hand | Aufwand mit R | Effizienzvorteil |
|---|---|---|---|
| Binomial / hypergeom. / Poisson | hoch (Tabelle) | 1 Zeile (`dbinom`, `dhyper`, `dpois`) | **groß** |
| Normalverteilung / z-Transformation | mittel–hoch (Tabelle) | 1 Zeile (`pnorm`, `qnorm`) | **groß** |
| Exponentialverteilung | mittel | 1 Zeile (`pexp`) | **groß** |
| Lage- & Streumaße | mittel | 1 Zeile (`mean`, `sd`, `var`) | mittel–groß |
| Schätzwerte / Gesetz d. großen Zahlen | praktisch unmöglich | Simulation (`replicate`) | **groß** |
| Vertrauensbereiche (μ, σ²) | hoch (Tabellen) | `t.test`, `qt`, `qchisq` | **groß** |
| Prüfergebnisse darstellen | mittel (Excel-Klicks) | `ggplot2` | **groß** |
| Kennzahlen & Ausreißer | hoch bei vielen Werten | `IQR`, Vektorlogik | **groß** |
| Lebensdauerverteilungen | hoch (Formeln) | `pweibull`, `fitdistrplus` | **groß** |
| Verteilungen verstehen (f(x)/F(x)) | — (Theorie) | Simulation + Plot | mittel |

**Fazit:** Alles, was in Klasse 3 mit **Tabellen, vielen Rechenschritten oder
vielen Daten** zu tun hat — also Verteilungen, Inferenz und Auswertung — ist
mit R **klar effizienter**. Die theoretischen Grundlagen bleiben Denkarbeit;
R macht sie aber durch **Simulation und Grafiken** deutlich greifbarer.
