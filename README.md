# 📊 E-Commerce Datenanalyse: Logistik, Kundenzufriedenheit & Reputationsrisiken

![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2.x-150458?logo=pandas&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualisierung-4C72B0)
![Kaggle](https://img.shields.io/badge/Kaggle-Notebook-20BEFF?logo=kaggle&logoColor=white)
![Status](https://img.shields.io/badge/Status-Work%20in%20Progress-orange)

---

## 🧭 Die Ausgangslage: Warum dieses Projekt?

Im Online-Handel ist Neukundengewinnung teuer. Wenn Bestandskunden wegen schlechter Erfahrungen nicht wiederkommen, verliert eine Plattform stille, aber reale Umsätze.

Olist ist ein brasilianischer E-Commerce-Marktplatz mit über 100.000 Bestellungen zwischen 2016 und 2018. Die Plattform verbindet Tausende Verkäufer mit Millionen Kunden. Genau deshalb stellt sich eine kritische Frage:

> **Was zerstört Kundenzufriedenheit — und wer ist dafür verantwortlich?**

Dieses Projekt versucht, diese Frage mit echten Daten, statistischen Methoden und klaren Visualisierungen zu beantworten.

---

## 📦 Datensatz

- **Quelle:** [Olist Brazilian E-Commerce Public Dataset (Kaggle)](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
- **Umfang:** ~100.000 Bestellungen, 9 CSV-Dateien, Zeitraum 2016–2018
- **Analysierte Datenpunkte:** Lieferzeiten, Kundenbewertungen (1–5 Sterne), Verkäuferleistung, Umsatzdaten, Retentionsverhalten

---

## 🛠️ Tech Stack

| Bereich | Tool |
|---------|------|
| Sprache | Python 3 |
| Datenverarbeitung | Pandas, NumPy |
| Visualisierung | Matplotlib, Seaborn |
| Methodik | EDA, Pearson-Korrelation, Perzentil-Analyse, Quadranten-Gruppierung |
| Umgebung | Kaggle Notebook |

---

## 🔬 Analyse-Struktur & Erkenntnisse

Die Analyse ist in 5 aufeinander aufbauende Teile gegliedert, die jeweils eine konkrete Forschungsfrage mit echten Datenwerten beantworten.

---

### Teil 1 — Lieferzeit vs. Kundenzufriedenheit

**Forschungsfrage:** Ab welchem Liefertag kippt die Bewertung ins Negative?

**Methodik:** Für jeden einzelnen Liefertag wurde der Durchschnitt der Sternebewertungen berechnet (GroupBy + mean). Das Ergebnis wurde als Liniendiagramm über die ersten 30 Tage visualisiert.

**Ergebnis:**

| Lieferzeit | Ø Bewertung |
|-----------|-------------|
| 1 Tag | ⭐ 4.50 |
| 5 Tage | ⭐ 4.39 |
| 10 Tage | ⭐ 4.20 |
| 20 Tage | ⭐ ~3.00 |
| 30+ Tage | ⭐ < 2.50 |

📉 **Kernaussage:** Die Zufriedenheit fällt nicht plötzlich — sie erodiert systematisch mit jedem zusätzlichen Tag. Das gibt dem Management einen klaren, messbaren Schwellenwert an die Hand.

---

### Teil 2 — Kundenloyalität & das Einmalkäufer-Modell

**Forschungsfrage:** Kaufen Kunden wirklich nur einmal — oder beeinflusst eine gute erste Erfahrung die Rückkehrrate?

**Methodik:** Segmentierung aller Kunden nach Kaufhäufigkeit. Anschließender Vergleich der Bewertungsverteilung zwischen Einmalkäufern und Wiederkäufern.

**Ergebnis:**

| Bewertung | Einmalkäufer | Wiederkäufer |
|-----------|-------------|--------------|
| ⭐⭐⭐⭐⭐ (5) | 57.59% | 59.36% |
| ⭐⭐⭐⭐ (4) | 19.45% | 17.85% |
| ⭐⭐⭐ (3) | 8.25% | 8.09% |
| ⭐⭐ (2) | 3.19% | 3.08% |
| ⭐ (1) | 11.53% | 11.61% |

🔍 **Kernaussage:** Die Bewertungsverteilung zwischen Einmal- und Wiederkäufern ist nahezu identisch. Das beweist: Olist operiert **strukturell als Einmalkäufer-Plattform**. Retention wird nicht durch Ersterfahrung gesteuert — die Ursache liegt tiefer im Geschäftsmodell.

---

### Teil 3 — Erwartungsbruch: Das gebrochene Lieferversprechen

**Forschungsfrage:** Was schadet mehr — ein langsames Paket oder ein gebrochenes Versprechen?

**Methodik:** Berechnung der Differenz zwischen dem versprochenen Lieferdatum (`order_estimated_delivery_date`) und dem tatsächlichen Lieferdatum. Vergleich der Bewertungen bei: (a) pünktlicher Lieferung, (b) verspäteter, aber schneller Lieferung, (c) gebrochenen Versprechen.

**Kernaussage:** Ein gebrochenes Lieferversprechen erzeugt **toxischere Bewertungen** als absolute Langsamkeit. Der Kunde bestraft nicht die Dauer — er bestraft den **Vertrauensbruch**.

---

### Teil 4 — Verkäuferqualität & Reputationsrisiko

**Forschungsfrage:** Welche Verkäufer gefährden das gesamte Plattform-Ökosystem?

#### 4.1 — Asymmetrische Schadensverteilung

Wenige Minderperformer verzerren das algorithmische Gesamtbild der Plattform unverhältnismäßig stark.

#### 4.2 — Pearson-Korrelation & Quadranten-Analyse

**Methodik:** Pearson-Korrelation zwischen Verspätungsquote und Kritikerquote pro Verkäufer. 75.-Perzentil-Grenze als Trennlinie für Quadranten-Gruppierung.

**Ergebnis:** Die Quadranten-Analyse trennt sauber: **Logistikversager** (hohe Verspätung, hohe Kritiker) vs. **Produktversager** (geringe Verspätung, aber trotzdem hohe Kritiker).

#### 4.3 — Carrier vs. Verkäufer: Wer trägt die Schuld?

**Kernaussage:** Der primäre Engpass liegt bei der **internen Bearbeitungszeit des Händlers** — nicht beim externen Carrier.

#### 4.4 — Umsatzrelevanz der Risiko-Großhändler

| Seller ID (gekürzt) | Bestellungen | Umsatz (BRL) | Kritikerquote |
|--------------------|-------------|--------------|---------------|
| 4a3ca9...884 | 1.949 | 197.225 | 32.1% |
| 7c67e1...fab | 1.358 | 186.664 | 44.0% |
| 1025f0...ffa | 1.422 | 138.691 | 28.6% |
| 2eb702...378 | 195 | 37.750 | 61.5% |
| 8846...930 | 308 | 32.108 | 41.6% |

📌 **Kernaussage:** Ein Verkäufer mit 61.5% Kritikerquote ist kein Qualitätsproblem — er ist ein **systemisches Risiko**.

---

### Teil 5 — Synthese & Strategischer Aktionsplan

- **Lieferzeitgarantie:** Harte SLA-Grenze bei max. 10 Tagen einführen
- **Erwartungsmanagement:** Lieferversprechen nur setzen, wenn Einhaltung statistisch gesichert ist
- **Händler-Monitoring:** Automatisches Flagging bei Kritiker- oder Verspätungsquote > 75. Perzentil
- **Carrier-Optimierung:** Fokus auf Händler-Bearbeitungszeit, nicht auf Carrier-Geschwindigkeit
- **Umsatz-Risiko-Matrix:** Großhändler mit hohem Umsatz + hoher Kritikerquote priorisiert behandeln

---

## 🚀 Notebook öffnen

👉 [Kaggle Notebook](DEIN_KAGGLE_LINK_HIER)

Oder lokal:

