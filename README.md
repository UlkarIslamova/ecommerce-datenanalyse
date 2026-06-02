# 📊 E-Commerce Datenanalyse: Logistik, Zufriedenheit und Kundenbindung


Projekt-Status: 🟢 Aktiv (Work in Progress)

Dieses Projekt ist eine explorative Datenanalyse (EDA) basierend auf realen E-Commerce-Daten (Olist Dataset). Das übergeordnete Ziel ist es, die geschäftskritische Kausalkette zu untersuchen: Wie beeinflussen Logistikprobleme die Kundenzufriedenheit und wann führen sie zum direkten Kundenverlust (Churn)?

🛠 Tech Stack Sprache: Python

Data Manipulation: Pandas, NumPy

Datenvisualisierung: Matplotlib, Seaborn

Methodik: Agiles Projektmanagement, Explorative Datenanalyse (EDA)

📈 Projektphasen (Agil & Iterativ)

[x] Phase 1: Das Fundament (Abgeschlossen) Analyse der direkten Korrelation zwischen realer Lieferzeit (in Tagen) und den abgegebenen Sterne-Bewertungen der Kunden. Identifikation des generellen Unzufriedenheits-Trends.
* 👉 [Klicke hier, um den Python-Code und die Daten für Teil 1 zu sehen](e-commerce-datenanalyse-eda.ipynb#Teil-1:-Wie-beeinflusst-die-Lieferzeit-die-Kundenzufriedenheit?)

[x] Phase 2: Hypothesentest Kundenbindung (Abgeschlossen) Untersuchung der Wiederholungskäufer-Rate in Abhängigkeit der Erstbewertung. Ergebnis (Plot Twist): Widerlegung der Ausgangshypothese. Beweis durch Warenkorbanalysen, dass Olist primär langlebige Güter vertreibt und faktisch als Einmalkäufer-Marktplatz agiert.
* 👉 [Klicke hier, um den Python-Code und den Beweis für Teil 2 zu sehen](e-commerce-datenanalyse-eda.ipynb#teil-2-die-beziehung-zwischen-der-kundenzufriedenheit-und-der-kundenbindung)

[ ] Phase 3: Der logistische Kipppunkt (In Arbeit) Da das Geschäftsmodell zu 100 % auf Neukunden basiert, ist der öffentliche Ruf essenziell. Berechnung des exakten "Tipping Points": Ab welchem Liefertag eskaliert die Unzufriedenheit in toxische Bewertungen (1-3 Sterne), die potenzielle Neukunden abschrecken?

[ ] Phase 4: Der Business-Impact & Umsatzrisiko (Geplant) Quantifizierung des finanziellen Risikos. Wie viel Umsatz (Risk-Revenue) generieren die Bestellungen, die den logistischen Kipppunkt überschreiten und somit den Ruf der Plattform gefährden?
