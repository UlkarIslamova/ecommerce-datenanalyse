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

---

### Teil 1 — Lieferzeit vs. Kundenzufriedenheit

**Forschungsfrage:** Ab welchem Liefertag kippt die Bewertung ins Negative?

**Methodik:** Für jeden einzelnen Liefertag wurde der Durchschnitt der Sternebewertungen berechnet (GroupBy + mean). Visualisiert als Liniendiagramm über die ersten 30 Tage.

| Lieferzeit | Ø Bewertung |
|-----------|-------------|
| 1 Tag | ⭐ 4.50 |
| 5 Tage | ⭐ 4.39 |
| 10 Tage | ⭐ 4.20 |
| 20 Tage | ⭐ ~3.00 |
| 30+ Tage | ⭐ < 2.50 |

![Einfluss der Lieferzeiten](Einfluss%20der%20Lieferzeiten%20auf%20die%20Kundenzufriedenheit.png)

![Eskalation der Kundenzufriedenheit](Eskalation%20der%20Kundenzufriedenheit.png)

📉 **Kernaussage:** Die Zufriedenheit erodiert systematisch mit jedem zusätzlichen Tag — kein plötzlicher Absturz, sondern ein messbarer, linearer Verfall.

---

### Teil 2 — Kundenloyalität & das Einmalkäufer-Modell

**Forschungsfrage:** Beeinflusst eine gute erste Erfahrung die Rückkehrrate?

| Bewertung | Einmalkäufer | Wiederkäufer |
|-----------|-------------|--------------|
| ⭐⭐⭐⭐⭐ (5) | 57.59% | 59.36% |
| ⭐⭐⭐⭐ (4) | 19.45% | 17.85% |
| ⭐⭐⭐ (3) | 8.25% | 8.09% |
| ⭐⭐ (2) | 3.19% | 3.08% |
| ⭐ (1) | 11.53% | 11.61% |

![Sterne-Verteilung bei Einmalkäufern und Wiederkäufern](Sterne-Verteilung%20bei%20Einmalk%C3%A4ufern%20und%20Wiederk%C3%A4ufern.png)

![Einfluss der ersten Bewertung auf den Wiederkauf](Einfluss%20der%20ersten%20Bewertung%20auf%20den%20Wiederkauf.png)

🔍 **Kernaussage:** Die Bewertungsverteilung ist nahezu identisch. Olist operiert **strukturell als Einmalkäufer-Plattform** — Retention wird nicht durch Ersterfahrung gesteuert.

---

### Teil 3 — Erwartungsbruch: Das gebrochene Lieferversprechen

**Forschungsfrage:** Was schadet mehr — ein langsames Paket oder ein gebrochenes Versprechen?

![Warum Unzuverlässigkeit gefährlicher ist als Lansamkeit](Warum%20Unzuverl%C3%A4ssigkeit%20gef%C3%A4hrlicher%20ist%20als%20Lansamkeit.png)

![Der wahre Einfluss von Verspätungen auf toxische Bewertungen](Der%20wahre%20Einfluss%20von%20Versp%C3%A4tungen%20auf%20toxische%20Bewertungen.png)

⚠️ **Kernaussage:** Ein gebrochenes Lieferversprechen erzeugt **toxischere Bewertungen** als absolute Langsamkeit. Der Kunde bestraft nicht die Dauer — er bestraft den **Vertrauensbruch**.

---

### Teil 4 — Verkäuferqualität & Reputationsrisiko

**Forschungsfrage:** Welche Verkäufer gefährden das gesamte Plattform-Ökosystem?

**Pearson-Korrelation & Quadranten-Analyse:** 75.-Perzentil-Grenze als Trennlinie — trennt **Logistikversager** von **Produktversagern**.

![Kausalanalyse Logistikversagen und Produktmängel](Kausalanalyse-%20Logistikversagen%20und%20Produktm%C3%A4ngel.png)

**Carrier vs. Verkäufer:** Der primäre Engpass liegt bei der **internen Bearbeitungszeit des Händlers** — nicht beim externen Carrier.

![Wer verursacht die Lieferverspätungen bei Olist](Wer%20verursacht%20die%20Lieferversp%C3%A4tungen%20bei%20Olist.png)

