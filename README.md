# **📊 E-Commerce Datenanalyse: Logistik, Kundenzufriedenheit und Reputationsrisiken**

Projekt-Status: 🔵 Abgeschlossen (Completed)

### **📌 Projektziel und Forschungsfokus**
Das primäre Ziel dieses Projekts ist eine umfassende, datengestützte Untersuchung der kausalen Zusammenhänge zwischen operativen Kernprozessen (Logistik und Händlerqualität) und der daraus resultierenden Kundenzufriedenheit auf der Olist-Plattform. Die Analyse dient dem Zweck, die mathematischen Dynamiken zwischen betrieblichen Kennzahlen und Nutzerbewertungen zu entschlüsseln, um fundierte Grundlagen für strategische Management-Entscheidungen zu schaffen.

### **🛠 Tech Stack & Tools**
- **Sprache:** Python
- **Data Manipulation:** Pandas, NumPy
- **Datenvisualisierung:** Matplotlib, Seaborn
- **Methodik:** Agiles Projektmanagement, Explorative Datenanalyse (EDA)

---

### 📑 Inhaltsverzeichnis
- Teil 1: Abhängigkeit zwischen Lieferzeit und Kundenzufriedenheit
- Teil 2: Untersuchung der Kundenloyalität und Validierung des Einmalkäufer Modells
- Teil 3: Analyse der Lieferverzögerung und mathematischer Nachweis des Erwartungsbruchs
- Teil 4.1: Asymmetrische Verteilung des Reputationsschadens durch Minderperformer
- Teil 4.2: Korrelationsanalyse und perzentilbasierte Quadranten Gruppierung der Verkäufer
- Teil 4.3: Kausalanalyse der logistischen Engpässe und Zuordnung der Verantwortung zwischen Carrier und Verkäufer
- Teil 4.4: Umsatzrelevanz minderperformanter Großhändler und Bewertung des Reputationsrisikos
- Teil 5: Synthese der Ergebnisse und Strategischer Aktionsplan

---

## Teil 1: Abhängigkeit zwischen Lieferzeit und Kundenzufriedenheit

### **Ziel**
Welchen messbaren Einfluss hat die Lieferzeit auf die vergebenen Sterne-Bewertungen? Wir wollen den exakten Trend Tag für Tag sichtbar machen. Das Ziel ist es, dem Management mit echten Daten zu beweisen, wie schnell Pakete ankommen müssen, um die Zufriedenheit auf einem profitablen Niveau zu halten.

### **Problem & Lösung**
Im Online-Handel ist es sehr teuer, neue Kunden zu gewinnen. Deshalb ist es extrem wichtig, dass bestehende Kunden zufrieden sind und wieder einkaufen. Wenn Kunden wegen langen Lieferzeiten unzufrieden sind und nicht mehr bestellen, verliert das Unternehmen viel Geld.
**Lösung:** Um dies zu analysieren, wurden die Rohdaten geladen, bereinigt und von Textformaten in echte Datumsangaben konvertiert (`order_purchase_timestamp` & `order_delivered_customer_date`). Durch das Zusammenführen der Tabellen über die `customer_id` zu einer Master-Tabelle wurde die exakte Lieferzeit in Tagen (`lieferzeit_tage`) berechnet und mit den Kundenbewertungen verknüpft, um den Durchschnitt der Sterne-Bewertungen pro Liefertag zu ermitteln.

### **Grafik**
<img src="images/einfluss_lieferzeiten.png.png" alt="Einfluss der Lieferzeit auf die Kundenzufriedenheit" width="800"/>

### **Grafikanalyse**
**1. Die generelle Übersicht und der Ergebnis**
Das Diagramm zeigt ein sehr klares Bild: Je länger ein Kunde auf sein Paket wartet, desto schlechter wird die Bewertung. 
* Bei einer sehr schnellen Lieferung (1 bis 4 Tage) sind die Kunden am glücklichsten und geben im Durchschnitt fast 4,5 Sterne. 
* Danach geht die Linie eindeutig und konstant nach unten. Bei 30 Tagen Wartezeit sind wir bereits bei nur noch 3 Sternen angekommen.

**2. Warum ist die Linie nicht perfekt glatt?**
 Die Kunden bewerten nicht *nur* die Lieferzeit. Ein Paket kann super schnell ankommen, aber wenn das Produkt kaputt ist oder der Paketbote unfreundlich war, gibt es trotzdem nur 1 Stern. Das sorgt für die kleinen Schwankungen in unserer Linie.
 
* **Das Rätsel um "Tag 0":** Warum ist eine Lieferzeit von 0 Tagen (4.23 Sterne) schlechter als 1 Tag (4.50 Sterne)? In der Realität bedeutet "0 Tage" oft, dass es Probleme gab. Zum Beispiel hat der Kunde die Bestellung sofort wieder storniert oder das System hatte einen Fehler. Das macht Kunden wütend und drückt den Durchschnitt nach unten.
* Diese Datensätze wurden bewusst nicht aus der Analyse entfernt, um die prozessualen Systemfehler und Stornierungsanomalien der Olist-Plattform transparent aufzuzeigen, anstatt die Datenbasis künstlich zu glätten.

---

## Teil 2: Untersuchung der Kundenloyalität und Validierung des Einmalkäufer Modells

### **Ziel**
Ziel dieses Abschnitts ist es, die wissenschaftliche Korrelation zwischen der ersten Kundenerfahrung (Sterne-Bewertung) und der Wahrscheinlichkeit eines erneuten Kaufs (Retention Rate) zu untersuchen. Die logische Ausgangshypothese lautet: Eine hohe Zufriedenheit führt zu einer höheren Kundenbindung.

### **Problem & Lösung**
Bevor wir die Berechnungen durchführen können, müssen wir die relevanten Tabellen korrekt zusammenführen (Mergen). Dabei gibt es eine strukturelle Besonderheit im Datensatz: Das System generiert für jede einzelne Bestellung eine neue `customer_id`. Um echte Wiederkäufer über einen längeren Zeitraum zu identifizieren, müssen wir stattdessen den übergeordneten Schlüssel `customer_unique_id` nutzen.
**Lösung:** Nach der Qualitätskontrolle der IDs wurden die Tabellen zusammengeführt. Über die `customer_unique_id` wurde ermittelt, wie oft jede Kunden-ID im System vorkommt. Die Kunden wurden in zwei Gruppen aufgeteilt (1 Kauf vs. mehr als 1 Kauf), mit einem entsprechenden Wiederkäufer-Flag markiert, chronologisch sortiert und die erste Sterne-Bewertung isoliert.

### **Grafik 1: Der (fehlende) Einfluss auf den Wiederkauf**
<img src="images/einfluss_erste_bewertung.png.png" alt="Der Einfluss der ersten Bewertung auf den Wiederkauf" width="800"/>

### **Grafikanalyse 1**
Das Diagramm zeigt uns eine harte wissenschaftliche Wahrheit: Die Sterne-Bewertung hat fast keinen Einfluss auf die Wiederkaufrate. Egal ob der Kunde sein erstes Paket liebt (5 Sterne) oder hasst (1 Stern), die Chance auf einen zweiten Kauf bleibt fast gleich niedrig (knapp über 3 %). Der Grund dafür ist das Marktplatz-Geschäftsmodell, bei dem Kunden generell nur für Einzelkäufe kommen.

Die Daten widerlegen unsere Ausgangshypothese eindeutig: Es gibt keine statistische Korrelation zwischen der Erstbewertung und der Kundenbindung. Sowohl bei katastrophalen (1 Stern) als auch bei perfekten (5 Sterne) Erfahrungen liegt die Wiederkaufrate konstant bei nur rund 3 %.

---

### **Grafik 2: Sterne-Verteilung bei Einmalkäufern vs. Wiederkäufern**
<img src="images/sterne_verteilung_einmalkaeufer.png.png" alt="Sterne-Verteilung bei Einmalkäufern vs. Wiederkäufern" width="800"/>

### **Grafikanalyse 2**
Um die Perspektive zu wechseln, vergleichen wir die Verteilung der ersten Sterne-Bewertungen direkt zwischen den beiden Gruppen. Das Ergebnis ist verblüffend: Die Verteilung der abgegebenen Sterne unterscheidet sich zwischen den abgebrochenen Einmalkäufern und den treuen Wiederkäufern fast überhaupt nicht. Über 57 % der Einmalkäufer hinterließen beim ersten Mal ein perfektes 5-Sterne-Feedback, kehrten aber dennoch nie wieder zurück.

**Der wissenschaftliche Beweis:**
Unsere Analyse der Top-5-Kategorien liefert den unwiderlegbaren Beweis für dieses Kundenverhalten. Olist vertreibt primär langlebige Gebrauchsgüter (wie Bettwäsche, Möbel, Sportgeräte und Computerzubehör). Das bedeutet: Olist funktioniert faktisch als reiner Marktplatz für Einmalkäufer. Die Kunden decken einen spezifischen, selten auftretenden Bedarf und haben danach schlichtweg über Jahre hinweg keinen Grund zurückzukehren – völlig unabhängig davon, wie zufrieden sie mit dem Service waren.

---

## Teil 3: Analyse der Lieferverzögerung und mathematischer Nachweis des Erwartungsbruchs

### **Ziel**
In diesem Abschnitt führen wir eine Sentiment-Analyse durch, um das Risiko einer toxischen Bewertung zu quantifizieren. Ab welchem exakten Liefertag kippt die Stimmung der Kunden statistisch ins Negative? Wir suchen den Punkt, an dem das Risiko einer 1-bis-3-Sterne-Bewertung die 50 %-Marke überschreitet.

### **Problem & Lösung**
Da wir in Teil 2 bewiesen haben, dass Olist fast ausschließlich von Neukunden lebt, ist der öffentliche Ruf (Reviews) die wichtigste Währung des Unternehmens. Wenn zu lange Lieferzeiten zu schlechten Bewertungen führen, schreckt das potenzielle Neukunden ab und gefährdet das gesamte Geschäftsmodell.
**Lösung:** Zur Umsetzung wurde eine Segmentierung vorgenommen: Bewertungen mit 4 & 5 Sternen wurden als "Fan" (False) klassifiziert, während 1, 2 & 3 Sterne als "Kritiker" (True) definiert wurden. Nach dem Zusammenführen mit den Bestelldaten und dem Filtern ungültiger Werte wurde der prozentuale Kritiker-Anteil in Abhängigkeit von den Lieferminuten berechnet, um den exakten Tipping Point zu bestimmen.

---

### **Grafik 1: Eskalation der Kundenunzufriedenheit (Fokus: Erste 30 Tage)**
<img src="images/eskalation_kundenzufriedenheit.png.png" alt="Eskalation der Kundenzufriedenheit" width="800"/>

### **Grafikanalyse 1 (Der logistische Kipppunkt / Tipping Point)**
**Die Ausgangslage (Baseline):** 
Betrachten wir die erste Woche nach der Bestellung (Tag 1 bis 7), sehen wir eine grundlegende Unzufriedenheitsquote (Kritiker) zwischen 12,0 % und 15,0 %. Dies ist die natürliche Basis-Fehlerquote. Selbst wenn die Logistik sehr schnell funktioniert, wird es aufgrund von beschädigten Produkten, falscher Verpackung oder völlig subjektiven Kundenerwartungen immer eine gewisse Basis an negativen Bewertungen geben.

**Der drastische Bruch (Inflection Point):** 
Die Daten zeigen sehr klare und harte Brüche. Ab dem 16. Tag überschreitet der Anteil der toxischen Bewertungen erstmals die 20-%-Marke (21,1 %). Ein noch dramatischerer Sprung erfolgt am 22. Tag, an dem die Quote abrupt auf 31,9 % hochschnellt.

*Warum nennen wir das einen "scharfen Bruch"?* 
Weil sich der Anteil der Kritiker im Vergleich zur Baseline hier faktisch verdoppelt hat. Genau ab diesem Punkt dominieren die logistischen Verzögerungen alle anderen Faktoren, werden zum Hauptproblem und spiegeln sich schonungslos in den Bewertungen wider.

---

### **Grafik 2: Erwartung vs. Realität: Der wahre Einfluss von Verspätungen auf toxische Bewertungen**
<img src="images/einfluss_verspaetungen.png.png" alt="Der wahre Einfluss von Verspätungen auf toxische Bewertungen" width="800"/>

### **Grafikanalyse 2 (Die katastrophale Eskalation der Delta-Analyse)**
Wenn wir die Daten jedoch mit brutaler Ehrlichkeit betrachten, stellen wir eine Anomalie fest: Obwohl es ab Tag 16 einen Anstieg gibt, ist die Kluft zwischen einer 5-Tage-Lieferung und einer 15-Tage-Lieferung geschäftlich gesehen viel geringer als erwartet.

Diese Situation zwingt uns, unsere Hypothese kritisch zu überdenken. Wir müssen die Kausalität wissenschaftlich untersuchen und folgende Frage stellen: **Was treibt die Unzufriedenheit der Kunden wirklich an – die absolute Lieferzeit oder der Bruch eines Versprechens?**

Die Daten beweisen: Wenn einem Kunden von Anfang an 15 Tage zugesagt wurden und das Paket in 15 Tagen ankommt, bleibt der Kunde zufrieden. Kommt ein Paket jedoch nach 7 Tagen an, obwohl 3 Tage versprochen waren, sorgt dieser mathematische Bruch des Lieferversprechens (das "Delta") für massive Frustration. Der Erwartungsbruch wiegt psychologisch schwerer als die absolute Langsamkeit. Ein genauer Blick auf unser Diagramm zeigt eine harte geschäftliche Realität: Die Unzufriedenheit steigt bei einer Verspätung nicht langsam, sondern sie explodiert ab der Deadline (Tag 0).

---

### **Grafik 3: Der ultimative Beweis: Warum Unzuverlässigkeit gefährlicher ist als Langsamkeit**
<img src="images/risiko_unzuverlaessigkeit.png.png" alt="Warum Unzuverlässigkeit gefährlicher ist als Langsamkeit" width="800"/>

### **Grafikanalyse 3 (Die Synthese – Visueller Beweis für die Relevanz des Expectation Managements)**
Die direkte Gegenüberstellung beider Modelle auf derselben Y-Achse (Schlechte Bewertung in %) liefert den ultimativen, datengestützten Beweis für das Kundenverhalten. Wir betrachten hier den Kontrast zwischen zwei völlig unterschiedlichen psychologischen und logistischen Metriken:

**1. Modell A (Links): Die Toleranz gegenüber Langsamkeit**
Die blaue Kurve zeigt die Entwicklung der Unzufriedenheit gemessen in absoluten Liefertagen (ab dem Kaufmoment). Der Anstieg der Unzufriedenheit verläuft hier moderat. Selbst nach 15 Tagen Wartezeit befindet sich die Quote noch im kontrollierbaren Bereich (~20 %). Es dauert **beachtliche 28 Tage**, bis die kritische 50-%-Marke (Risikozone) erreicht wird.
*(Anmerkung: Die Anomalie an Tag 0 ist in der Regel auf systembedingte Sofortstornierungen oder schwere Fehler im Bestellprozess zurückzuführen und spiegelt keine echte Lieferzeit wider.)*

**2. Modell B (Rechts): Der fatale Effekt der Unzuverlässigkeit**
Die rote Kurve misst die Unzufriedenheit ausgehend vom Versprechen (Deadline). Hier sehen wir keine flache Kurve, sondern eine vertikale Wand. Frühzeitige Lieferungen (links der schwarzen Linie) senken die natürliche Basis-Unzufriedenheit nicht wesentlich. Sobald die Deadline jedoch überschritten wird, eskaliert die Situation katastrophal. Was im Modell A volle 28 Tage dauert, passiert hier in **nur 2 Tagen (+48 Stunden)**: Die Unzufriedenheit durchbricht die 50-%-Risikozone.

**Das finale analytische Urteil:**
Das Diagramm beweist unmissverständlich den psychologischen Kipppunkt unserer Kunden. Unzuverlässigkeit ist weitaus gefährlicher als Langsamkeit. Kunden sind bereit, lange Lieferzeiten zu akzeptieren, solange diese transparent kommuniziert und eingehalten werden. Ein gebrochenes Lieferversprechen wird hingegen sofort und gnadenlos abgestraft.

---

## Teil 4: Wirtschaftliche Relevanz der Verkäuferqualität und Identifikation operativer Risikoträger

In diesem umfassenden Kapitel wird der finanzielle und reputative Einfluss von qualitativen Minderperformern auf das Gesamtökosystem der Olist-Plattform datengestützt analysiert. Da die Plattform existenziell von Neukunden abhängt, spielen Händler, die systematisch schlechte Bewertungen verursachen, eine kritische Rolle für das wirtschaftliche Überleben des Unternehmens.

Um diese Dynamiken präzise zu entschlüsseln, ist die Untersuchung in vier spezialisierte Teilbereiche unterteilt:
- **Teil 4.1:** Asymmetrische Verteilung des Reputationsschadens durch Minderperformer
- **Teil 4.2:** Korrelationsanalyse und perzentilbasierte Quadranten-Gruppierung der Verkäufer
- **Teil 4.3:** Kausalanalyse der logistischen Engpässe und Zuordnung der Verantwortung zwischen Carrier und Verkäufer
- **Teil 4.4:** Umsatzrelevanz minderperformanter Großhändler und Bewertung des Reputationsrisikos

---

## Teil 4.1: Asymmetrische Verteilung des Reputationsschadens durch Minderperformer

### **Ziel**
Wie ungleich ist der Reputationsschaden auf der Plattform verteilt und in welchem Maße verzerren wenige qualitative Ausreißer (Minderperformer) das algorithmische Gesamtbild der Kundenzufriedenheit? Das Ziel ist es, mathematisch zu beweisen, ob eine kleine Gruppe von schlechten Verkäufern für den Großteil der negativen Bewertungen verantwortlich ist.

### **Problem & Lösung**
Wenn man nur den Durchschnitt aller Bewertungen betrachtet, sieht die Plattform stabil aus. Das Problem ist aber, dass das Management dadurch die echten operativen Risikoträger nicht sieht. Wenn wenige Verkäufer massiven Schaden anrichten, zieht das den Ruf der gesamten Plattform nach unten, ohne dass man die genauen Verursacher kennt.
**Lösung:** Um dies zu lösen, wurden die Verkäufer-IDs gefiltert und analysiert. Es wurde berechnet, wie hoch der Anteil der 1-Sterne-Bewertungen (Kritiker) pro Verkäufer ist. Die Verteilung des Reputationsschadens wurde mathematisch über eine statistische Auswertung isoliert, um die Konzentration der negative Bewertungen exakt zu belegen.

### **Ergebnis-Tabelle**
Da für diesen Abschnitt keine Grafik vorliegt, sind hier die bereinigten statistischen Ergebnisse der Verteilung kurz zusammengefasst:

| Perzentil der Verkäufer | Anteil an den gesamten 1-Sterne-Bewertungen |
| :--- | :--- |
| **Top 10%** (Schlechteste Verkäufer) | ~ 45 % aller 1-Sterne-Bewertungen |
| **Top 20%** (Minderperformer) | ~ 70 % aller 1-Sterne-Bewertungen |
| **Restliche 80%** (Gute Performer) | ~ 30 % aller 1-Sterne-Bewertungen |

### **Grafikanalyse (Analytisches Urteil)**
Die statistische Verteilung des Reputationsschadens ist extrem asymmetrisch. Eine kleine Gruppe von qualitativ minderwertigen Verkäufern (Minderperformer) verursacht überproportional viele 1-Sterne-Bewertungen. Diese Ausreißer verzerren das algorithmische Gesamtbild der Kundenzufriedenheit massiv. Während die Mehrheit der Händler eine solide Performance zeigt, ruinieren wenige Risikoträger den Ruf des gesamten Ökosystems.

---

## Teil 5: Synthese der Ergebnisse und Strategischer Aktionsplan

Wie lassen sich die in den vorherigen Phasen empirisch nachgewiesenen Datenwerte strategisch nutzen, um den Plattformumsatz nachhaltig zu sichern, und welche datenbasierten Maßnahmen müssen ergriffen werden, um die Neukundenakquise vor Qualitätsdefiziten zu schützen?

### Fazit zu Frage 1: Was uns das Diagramm zeigt

**1. Die generelle Übersicht und der Ergebnis**
Das Diagramm zeigt ein sehr klares Bild: Je länger ein Kunde auf sein Paket wartet, desto schlechter wird die Bewertung. 
* Bei einer sehr schnellen Lieferung (1 bis 4 Tage) sind die Kunden am glücklichsten und geben im Durchschnitt fast 4,5 Sterne. 
* Danach geht die Linie eindeutig und konstant nach unten. Bei 30 Tagen Wartezeit sind wir bereits bei nur noch 3 Sternen angekommen.

**2. Warum ist die Linie nicht perfekt glatt?**
 Die Kunden bewerten nicht *nur* die Lieferzeit. Ein Paket kann super schnell ankommen, aber wenn das Produkt kaputt ist oder der Paketbote unfreundlich war, gibt es trotzdem nur 1 Stern. Das sorgt für die kleinen Schwankungen in unserer Linie.
 
* **Das Rätsel um "Tag 0":** Warum ist eine Lieferzeit von 0 Tagen (4.23 Sterne) schlechter als 1 Tag (4.50 Sterne)? In der Realität bedeutet "0 Tage" oft, dass es Probleme gab. Zum Beispiel hat der Kunde die Bestellung sofort wieder storniert oder das System hatte einen Fehler. Das macht Kunden wütend und drückt den Durchschnitt nach unten.
* Diese Datensätze wurden bewusst nicht aus der Analyse entfernt, um die prozessualen Systemfehler und Stornierungsanomalien der Olist-Plattform transparent aufzuzeigen, anstatt die Datenbasis künstlich zu glätten.
