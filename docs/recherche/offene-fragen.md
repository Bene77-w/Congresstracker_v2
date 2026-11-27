# Offene Fragen für den Neubau v2

**Stand:** 2026-11-27. Grundlage für die Planungsinterviews.
**Abrufdatum:** Alle Weblinks wurden am 2026-11-27 abgerufen. **unbelegt** heißt: an keiner Primärquelle bestätigt.
**Kurzformen für Fundstellen:**
- `v1:` = `/home/bene/Nextcloud/Projekte/bmb_trdprg/congress_tracker/` (nur gelesen)
- `GB:` = `git -C <v1> show 4f2dfa9^:organisation/rebuild_audit/00_GESAMTBERICHT.md`, Zeilen dieser Ausgabe
- `README:` und `submapper.md:` = Dateien in diesem Repo
- Die Entscheidungen E1–E5 und O1–O19 aus `v1:docs/sanierung/audit.md` galten der Reparatur von v1. Hier sind sie wieder offen.
- Die Trade-Quelle wird nicht hier, sondern in `docs/recherche/trade-datenquellen.md` recherchiert.

**Typ:** *Owner* = nur der Owner kann entscheiden (Nutzung, Vorliebe, Budget). *recherchiert* = Sachfrage, hier an Quellen geklärt; der Owner bestätigt nur die Empfehlung. *offen recherchierbar* = Sachfrage, die erst nach einer anderen Entscheidung oder mit einem Konto prüfbar ist.

## Übersicht in Entscheidungsreihenfolge

| Nr. | Frage | Typ | hängt ab von | blockiert | Empfehlung |
|---|---|---|---|---|---|
| **A** | **Sofort und Rahmen** | | | | |
| F01 | Was passiert bis zum Start von v2 mit der v1-Live-Seite? | Owner | – | – | Offline nehmen oder deutlich als fehlerhaft kennzeichnen |
| F02 | Für wen ist das Dashboard gedacht? | Owner | – | F09, F41, F43, F53 | Öffentlichkeit; Analysewerkzeuge nur lokal |
| F03 | Welches Budget gibt es für Daten und Betrieb? | Owner | – | F06, F10, F11 | Bis ca. 40 $/Monat für Kurse einplanen |
| F04 | Wird „nicht kommerziell“ als harte Regel festgeschrieben? | recherchiert | README:7 | F05, F10, F53 | Ja: keine Werbung, keine Spenden, keine Bezahlfunktion |
| F05 | Wird vor dem Livegang ein Anwalt gefragt? | Owner | F04 | Livegang | Ja, mit fester Fragenliste |
| **B** | **Datenquellen** | | | | |
| F06 | Trade-Quelle (README #1) | Abhängigkeit | F03, F04 | fast alles | siehe `trade-datenquellen.md` |
| F07 | Wird der v1-Bestand (114.347 Quiver-Zeilen) übernommen? | Owner | F06 | F08, F21, F58 | Nur wenn die Lizenz es erlaubt, sonst neu aufbauen |
| F08 | Welchen Zeitraum deckt v2 ab? | Owner | F06, F07 | F10, F13, F16 | Ab 2012, Lücken je Jahr ausweisen |
| F09 | Zeigt das Dashboard Kursverläufe oder nur eigene Kennzahlen? | Owner | F02 | F10 | Nur Kennzahlen (Rendite, AR) |
| F10 | Kursquelle (README #2) | recherchiert | F03, F08, F09 | F11, F12, F28 | Sharadar Prices Full History; Lizenz schriftlich bestätigen lassen |
| F11 | Wie wird ein Ticker zum Handelsdatum aufgelöst? | recherchiert | F10 | F20, F28 | Sharadar `permaticker` plus PTR-Asset-Name und Assetcode |
| F12 | Woher kommen Sektor und Industry? | recherchiert | F10 | F29 | Mit der Kursquelle entscheiden, Taxonomie als eigenen Snapshot führen |
| F13 | Welche Kongresse bekommen Ausschuss-Mitgliedschaften? (README #3) | recherchiert | F08 | F14, F29, F37 | 113–119 aus der Git-Historie von congress-legislators, 112 nur eingeschränkt |
| F14 | Mitgliedschaft je Kongress oder tagesgenau? | recherchiert | F13 | F27, F36 | Tagesgenau mit Intervallen und Unschärfeangabe |
| F15 | Wie wird der 120. Kongress (ab 2027-01-03) gepflegt? | Owner | F13, F29 | Betrieb ab 2027 | Eigener Pflegeablauf, bis dahin laut scheitern |
| F16 | Woher kommen Votes und Bill-Actions? | recherchiert | F08, F38 | F38 | GovInfo-BILLSTATUS-Bulk plus Clerk-XML, Senat über Voteview |
| F17 | Werden PTR-Rohdokumente gesichert? | recherchiert | F06 | F46 | Ja, Reports werden 6 Jahre nach dem Ausscheiden vernichtet |
| **C** | **Fachregeln für den Import** | | | | |
| F18 | Wie werden Trades mit Mitgliedern (bioguide) verknüpft? | offen recherchierbar | F06 | F19, F41 | `bioguide_id` als einziger Schlüssel |
| F19 | Wie werden Sonderfälle der Mitgliedschaft behandelt? | Owner | F14, F18 | F36 | Ausdrücklicher Status je Fall |
| F20 | Welche Assetklassen gibt es, was wird ausgeschlossen? (O9, O10) | Owner | F11 | F37, F40 | Nur Aktien, ADRs, REITs; Rest sichtbar, aber unbewertet |
| F21 | Sind identische Zeilen echte Lots? (O3) | offen recherchierbar | F06 | F37, F39 | Stichprobe gegen PTRs, dann `lot_index` |
| F22 | Wie werden Korrekturen und Amendments gespeichert? | Owner | F06 | F45 | Versionieren statt überschreiben |
| F23 | Wie zählt das Owner-Feld (Self, Spouse, Joint, Child)? | Owner | F06 | F37, F39 | Speichern, anzeigen, in der Event-Study schichten |
| F24 | Wie werden Betragsspannen modelliert? | Owner | F06 | F37, F39 | Unter- und Obergrenze speichern, NULL statt 0 |
| F25 | Wie werden Transaktionstypen in Richtungen übersetzt? | Owner | F06 | F28, F39 | Feste Tabelle, Exchange ohne Richtung |
| F26 | Datums-Fallback und späte Meldungen | Owner | F06 | F37 | Fallback mit Flag, „late“ nach STOCK-Act-Frist |
| F27 | Zeitzonen, Kongressgrenzen, Kalender | Owner | – | F28, F38 | Kalenderdaten ohne Uhrzeit, Votes in America/New_York |
| F28 | Wie sind Rendite und Abnormal Return definiert? | Owner | F10, F27 | F40 | AR gegen SPY, Handelstage, NULL bei Lücke |
| **D** | **Ausschuss→Industry-Mapping** | | | | |
| F29 | Mapping übernehmen oder Submapper neu bauen? (README #5) | Owner | F12, F13 | F30–F32 | Übernehmen; Submapper erst für den 120. Kongress |
| F30 | Werden fragwürdige Zuordnungen vorher nachgeprüft? | Owner | F29 | F37 | Ja, die 123 reinen Recherche-Zuordnungen |
| F31 | Overrides und Ausschüsse ohne Unit | Owner | F29 | F47 | SSEV15 bestätigen, die fünf ohne Unit lassen |
| F32 | Bleiben Unit-IDs über Kongresse stabil? | Owner | F13, F29 | F15 | Eigene Nachfolger-Tabelle |
| F33 | Rollen und Vererbung vom Elternausschuss (E4) | Owner | F13 | F36 | E4 übernehmen, Rollen normalisieren |
| **E** | **Analyse und Produkt** | | | | |
| F34 | Braucht v2 einen Score oder nur Markierungen? (README #4) | Owner | F02 | F35, F37, F41 | Nur erklärbare Markierungen |
| F35 | Wie werden Markierungen öffentlich formuliert? | Owner | F05, F34 | F41, F53 | Neutral, Methode offen, kein Vorwurf |
| F36 | Ein Committee-Signal ohne Halbtreffer (E2)? | Owner | F14, F33 | F37 | Ja |
| F37 | Welche Signale baut v2? (README #6, O6) | Owner | F34, F40 | F41 | Klein anfangen, Rest nach der Event-Study |
| F38 | Wird Vote-Timing gebaut? (O8) | Owner | F16, F37 | F16 | Später, als Hypothese testen |
| F39 | Braucht v2 eine Exit-Erkennung? | Owner | F21, F23, F24 | F41 | Zunächst nein |
| F40 | Welche Methodik hat die Event-Study? | Owner | F28 | F37 | Feste Hypothesen, Richtung geschichtet, zweifach geclustert |
| F41 | Welche Funktionen hat das Dashboard? | Owner | F02, F34 | F44 | Schlanker Satz, keine Entwicklerwerkzeuge öffentlich |
| F42 | Wie werden Datenlücken für Besucher sichtbar? | Owner | F13, F28 | F41 | Abdeckung je Jahr und Datenstand immer anzeigen |
| F43 | Sprache, Mobilansicht, Barrierefreiheit | Owner | F02 | F41, F53 | Englische Oberfläche, deutsche Rechtstexte |
| **F** | **Architektur** | | | | |
| F44 | Stack: Sprache, Dashboard-Technik, Bibliotheken | Owner | F41 | F45, F52 | Python; vorberechnete Daten, Technik nach Prototyp |
| F45 | Speicherformat, Datenmodell, Schreibweg (O14) | Owner | F22, F44 | F46 | DuckDB/Parquet, ein Schreibweg mit Datenvertrag |
| F46 | Rohdaten-Archiv und Laufmanifest | Owner | F10, F17 | F51, F58 | Ja, mit Lizenzgrenzen |
| F47 | Was wird aus den v1-Referenzdaten übernommen? | recherchiert | F13, F29 | F58 | Mapping und Overrides übernehmen, Rest neu erzeugen |
| **G** | **Betrieb** | | | | |
| F48 | Wo läuft die Pipeline? | offen recherchierbar | F06, F16 | F49, F52 | Lokal; Senate-Zugriff vom VPS testen |
| F49 | Rhythmus und automatischer Lauf (O14) | Owner | F06, F48 | F50 | Täglich Dry-Run, Speichern nach Prüfung |
| F50 | Monitoring und Alarm | Owner | F49 | – | Alarm bei fehlenden neuen Trades |
| F51 | Backups | Owner | F46 | – | Rohdaten und Referenz sichern, VPS reproduzierbar |
| F52 | Deployment und Secrets | Owner | F44, F48 | – | v1-Ablauf (Compose, Caddy) beibehalten |
| **H** | **Recht in der Umsetzung** | | | | |
| F53 | Impressum, Datenschutz, Information für Politiker | recherchiert | F04, F05, F35 | Livegang | v1-Texte anpassen, Art.-14-Info ergänzen |
| F54 | Umgang mit Auskunfts- und Widerspruchsanfragen | Owner | F05 | F45 | Einfacher Prozess plus Sperrvermerk im Datenmodell |
| **I** | **Qualität und Arbeitsweise** | | | | |
| F55 | Qualitätsvertrag (README #7, E5, O16) | Owner | F44 | Bau | Grundregeln, Architekturgrenzen, Zeilenbudget |
| F56 | Testkonzept mit aufgezeichneten Fixtures | Owner | F10, F59 | Bau | Gekürzte Aufzeichnungen, Live-Tests nur manuell |
| F57 | Wissensinventur der v1-Sonderfälle und Defekt-Fixtures | offen recherchierbar | – | F56 | Vor dem Bau als Tabelle anlegen |
| F58 | Abnahmekriterien, Datengates und erster Release | Owner | F10, F13 | Livegang | Gates relativ zur erreichbaren Abdeckung |
| F59 | Repo-, Branch- und Review-Konventionen | Owner | – | erstes Ticket | Branch je Feature, Review vor Merge |

**Zählung:** 59 Fragen: 44 Owner, 10 recherchiert, 4 offen recherchierbar (F18, F21, F48, F57), 1 Abhängigkeit (F06).

---

## A. Sofort und Rahmen

### F01 Was passiert bis zum Start von v2 mit der v1-Live-Seite?
- **Herkunft:** `v1:organisation/DEPLOYMENT.md:318-328` (live seit 2026-08-30, Stand 2026-07-21), `v1:docs/sanierung/audit.md:148` (ES-2: 43,3 % künstliche Renditen von 0, „sehr wahrscheinlich auch im Dashboard“).
- **Warum jetzt:** Die öffentliche Seite zeigt bekannt falsche Zahlen. Laut `DEPLOYMENT.md:333` war auch das Ausrollen von Impressum und Datenschutz noch offen.
- **Optionen:**
  1. Offline nehmen, Hinweisseite mit Impressum. Kein Risiko durch falsche Zahlen.
  2. Weiterlaufen lassen mit Banner „Datenstand 2026-07-21, Renditen fehlerhaft“. Sichtbarkeit bleibt, Risiko sinkt.
  3. Unverändert lassen. Falsche Zahlen bleiben namentlich zu Politikern öffentlich.
- **Empfehlung:** 1. Option 2 nur, wenn die Domain sichtbar bleiben soll.

### F02 Für wen ist das Dashboard gedacht?
- **Herkunft:** `README:7` (öffentlich, nicht kommerziell); `v1:organisation/DEPLOYMENT.md:308` (`APP_PUBLIC_MODE`); `v1:deploy/legal/impressum.html:46-49` („journalistische Zwecke“).
- **Folge:** Bestimmt Umfang (F41), Sprache (F43), Rechtstexte (F53) und ob Analysewerkzeuge öffentlich sind.
- **Optionen:**
  1. Öffentlichkeit und Journalismus. Kleine, verständliche Oberfläche; Analyse läuft lokal.
  2. Eigenes Analysewerkzeug, öffentlich nur nebenbei. Mehr Funktionen, aber Score-Editor und Statistik sind für Besucher irreführend (v1: `audit.md:164` ES-7).
- **Empfehlung:** 1. Analysewerkzeuge (Event-Study, Gewichte) als lokales Skript.

### F03 Welches Budget gibt es für Daten und Betrieb?
- **Herkunft:** Neubau-Bedarf; Preise siehe F10, F06.
- **Belegte Preisspanne für Kurse:** Sharadar Prices Full History „$39“/Monat oder „$299“/Jahr (Personal Use); Tiingo Power „$30/month (or $300/year)“, Anzeige-Lizenz „$250/Month for Start-ups“; Massive Stocks Business $2,499/Monat. Details in F10.
- **Optionen:**
  1. 0 €: nur kostenlose Quellen. Für Kurse gibt es keine lizenzkonforme kostenlose Quelle mit Delistings (F10).
  2. Bis ca. 40 $/Monat: reicht für Sharadar Prices Full History oder Tiingo Power.
  3. 250 $/Monat und mehr: Tiingo-Anzeige-Lizenz, Kursverläufe öffentlich möglich.
- **Empfehlung:** 2, dazu das Budget der Trade-Quelle aus F06. Ein Anwalt (F05) kommt einmalig hinzu.

### F04 Wird „nicht kommerziell“ als harte Regel festgeschrieben?
- **Herkunft:** `README:7`; Recherche Recht.
- **Befund:**
  - 5 U.S.C. § 13107(c)(1) verbietet „any person“, einen Report „for any commercial purpose“ zu nutzen. Ausnahme: „news and communications media for dissemination to the general public“. Ebenso verboten: Nutzung „directly or indirectly, in the solicitation of money for any political, charitable, or other purpose“. Strafe nominell bis 10.000 USD ([LII](https://www.law.cornell.edu/uscode/text/5/13107)). Der heute geltende inflationsbereinigte Betrag ist **unbelegt** ([28 CFR 85](https://www.ecfr.gov/current/title-28/chapter-I/part-85) nennt früher 11.000 USD).
  - Das House-Portal zeigt den Hinweis wörtlich ([disclosures-clerk.house.gov](https://disclosures-clerk.house.gov/FinancialDisclosure/ViewSearch)), Senate eFD verlangt eine Bestätigung vor der Suche ([Wayback 2026-11-26](http://web.archive.org/web/20261126181641/https://efdsearch.senate.gov/search/home/)).
  - Günstige Datenlizenzen gelten nur nicht kommerziell (Sharadar, Tiingo Power, siehe F10).
  - Daten von Stewart/Woon: „may not be used commercially“ ([MIT](https://web.mit.edu/17.251/www/data_page.html)).
- **Empfehlung:** Ja. Keine Werbung, keine Bezahlfunktion, keine Affiliate-Links, kein Datenverkauf und vorerst kein Spendenlink. Ob ein Spendenlink schon unter lit. D fällt, klärt der Anwalt (F05).

### F05 Wird vor dem Livegang ein Anwalt gefragt?
- **Herkunft:** Recherche Recht (offene Punkte).
- **Offene Rechtsfragen (nicht recherchierbar):**
  1. Reichweite von „commercial purpose“ und „solicitation“ in § 13107, Durchsetzbarkeit gegenüber einem Betreiber in Deutschland.
  2. Gilt das Dashboard als „journalistisch-redaktionell“ (§ 18 Abs. 2 MStV) oder als „geschäftsmäßig“ (§ 5 DDG, § 19 MStV)?
  3. Trägt Art. 6 Abs. 1 lit. f DSGVO die namentliche Anzeige mit Markierungen? Gibt es für Private eine Umsetzung von Art. 85 DSGVO im Landesrecht?
  4. Äußerungsrechtliches Risiko bei Markierungen, die man als Insider-Vorwurf lesen kann.
- **Optionen:** (1) Erstberatung vor dem Livegang, (2) ohne Beratung mit vorsichtiger Formulierung starten.
- **Empfehlung:** 1. Das Bußgeld für ein fehlendes Impressum liegt bei bis zu 50.000 EUR, auch bei Fahrlässigkeit (§ 33 Abs. 2 Nr. 1, Abs. 6 Nr. 3 DDG, [gesetze-im-internet.de](https://www.gesetze-im-internet.de/ddg/__33.html)).

---

## B. Datenquellen

### F06 Trade-Quelle (README #1)
- **Herkunft:** `README:29`; `v1:docs/sanierung/audit.md:147` (SCR-1), `:465` (O1); `v1:docs/sanierung/plan-stufe2-verworfen.md:40`; `GB:530`.
- **Stand:** Wird separat recherchiert in `docs/recherche/trade-datenquellen.md`. Hier nur als Abhängigkeit.
- **Wovon hier vieles abhängt:** Liefert die Quelle eine BioGuideID (F18), Asset-Typcodes (F20), Lots (F21), Amendments (F22), Owner-Feld (F23), Betragsspannen (F24)? Welche Lizenz gilt für öffentliche Anzeige und Speicherung (F07, F46)?

### F07 Wird der v1-Bestand übernommen?
- **Herkunft:** `v1:docs/sanierung/audit.md:311` (114.347 Zeilen, 2012-02 bis 2026-07, Quelle Quiver).
- **Befund:** Laut `trade-datenquellen.md` erlauben die Quiver-Tarife Hobbyist und Trader nur nicht kommerzielle Nutzung; Weitergabe nur mit Vertrag. Ob die Nutzung des alten Exports nach Abo-Ende erlaubt ist, ist **unbelegt**.
- **Optionen:**
  1. Bestand übernehmen. Schneller Start mit Historie, aber Lizenzrisiko und bekannte Defekte (Duplikate, Typcodes).
  2. Historie aus der neuen Quelle neu aufbauen, v1 nur zum Abgleich. Saubere Herkunft.
- **Empfehlung:** 2, sofern die neue Quelle ab 2012 liefert. v1-Daten nur intern als Vergleich für die Abnahme (F58).

### F08 Welchen Zeitraum deckt v2 ab?
- **Herkunft:** `v1:docs/sanierung/audit.md:156` (TICK-5: Kursabdeckung 2013–2019 unter 80 %), `:340` (nur ein Marktregime ab 2021).
- **Fakten:** Senate eFD enthält Reports „filed from 2012 to present“; das House-Auswahlfeld reicht von 2008 bis 2026 (Recherche Recht, Wayback-Link oben). Reports werden 6 Jahre nach dem Ausscheiden vernichtet (§ 13107(d)).
- **Optionen:**
  1. Ab 2012. Mehrere Marktphasen, höherer Aufwand für Ausschüsse (F13) und Kurse.
  2. Ab 2021. Einfacher, aber nur ein Marktregime; Ergebnisse kaum übertragbar.
- **Empfehlung:** 1, mit Abdeckung je Jahr im Bericht und im Dashboard (F42).

### F09 Zeigt das Dashboard Kursverläufe oder nur eigene Kennzahlen?
- **Herkunft:** `v1:app/streamlit_app.py:1512-1559` (Kurschart aus dem Cache), `v1:deploy/README_deployment.md:24` (`price_history.parquet` liegt auf dem öffentlichen Server).
- **Befund:** Fast alle bezahlbaren Lizenzen verbieten die Anzeige von Rohkursen, erlauben aber abgeleitete Kennzahlen, die keine Rückrechnung erlauben (F10).
- **Optionen:**
  1. Nur Kennzahlen (Rendite je Trade, Abnormal Return, Aggregate). Günstige Lizenz reicht.
  2. Kursverläufe einzelner Aktien. Braucht Anzeige-Lizenz (Tiingo ab 250 $/Monat) oder schriftliche Freigabe.
- **Empfehlung:** 1. Für den Kursverlauf auf eine externe Seite verlinken (v1 verlinkt bereits auf Google, `streamlit_app.py:1182`).

### F10 Kursquelle (README #2)
- **Herkunft:** `README:30`; `GB:532`; `v1:docs/sanierung/audit.md:156` (TICK-5), `:157` (ES-12, Splices), `:491` (11.3).
- **Bedarf:** EOD-Kurse bereinigt und unbereinigt, delistete Titel ab 2012, Symbolhistorie, SPY, ca. 5.000–6.000 Ticker, öffentliche Anzeige abgeleiteter Werte.

| Anbieter | Preis (wörtlich) | Historie, Delistings | Symbolhistorie | Öffentliche Anzeige | Kündigung |
|---|---|---|---|---|---|
| yfinance/Yahoo | kostenlos | Delistings fehlen laut v1-Erfahrung (an Primärquelle **unbelegt**) | nein | **verboten**: Yahoo-ToS untersagen automatisierte Erfassung und Verbreitung ([Yahoo ToS](https://legal.yahoo.com/us/en/yahoo/terms/otos/index.html)); yfinance-README: „intended for personal use only“ ([Repo](https://github.com/ranaroussi/yfinance)) | – |
| **Sharadar** (direkt bei sharadar.com) | Prices Full History „$39“/Monat, „$299“/Jahr; enthält tickers, actions, stocks, funds ([Preise](https://www.sharadar.com/pricing)) | ab 1998, „more than 21,000 active and delisted tickers“ ([SEP](https://data.nasdaq.com/databases/SEP)); Fonds/ETFs über SFP ([SFP](https://data.nasdaq.com/databases/SFP)) | ja: `permaticker`, ACTIONS mit Ticker-Wechseln ([Docs](https://www.sharadar.com/docs/actions)) | Personal Use einer natürlichen Person. § 6: öffentliche Anzeige mit „Data from Sharadar.com“; keine Attribution nötig für „research outputs, backtest results, models, summary statistics, trade logs“. Aber § 4: „may not publish, disseminate, re-distribute or share the Services Data“ ([Terms](https://sharadar.com/terms)) | zum Periodenende; Löschung binnen 30 Tagen |
| Tiingo | Power „$30/month (or $300/year)“; intern kommerziell „$50/month (or $499/year)“; „Business Display Redistribution“ „$250/Month for Start-ups“ ([Preise](https://www.tiingo.com/about/pricing), [EOD](https://www.tiingo.com/products/end-of-day-stock-price-data)) | ab 1962; 8.475 US-Aktien mit Enddatum 2012–2026 in `supported_tickers.zip` (eigene Zählung) | keine permanente ID; alte FB-Aktie fehlt, ANSS-Enddatum falsch ([zip](https://apimedia.tiingo.com/docs/tiingo/daily/supported_tickers.zip)) | Power/Commercial „Internal Use Only“; Dashboards und Charts mit Tiingo-Daten ausdrücklich verboten; abgeleitete Werte nur, wenn nicht rückrechenbar, „nach Ermessen“ von Tiingo ([ToS](https://www.tiingo.com/tos)) | jederzeit; danach alle Tiingo-Daten löschen, bei Power ohne Ausnahme |
| Massive (früher Polygon.io) | Advanced $199/Monat (personal); Stocks Business $2,499/Monat, $19,188/Jahr ([Preise](https://massive.com/pricing), [Business](https://massive.com/business)) | ab 2003-09-10; Developer nur 10 Jahre | Ticker Events, `date`-Parameter | Individual verboten (§ 5(c)); Business erlaubt Anzeige ([ToS](https://massive.com/legal/businesses-terms-of-service)) | Business nicht „for convenience“ kündbar |
| EODHD | Personal „€ 19.99 /mo.“; Internal „€ 399.00 /mo.“; Enterprise „€ 2499.00 /mo.“ ([Preise](https://eodhd.com/commercial-pricing)) | ab 1962, delistete behalten Historie | Umbenennungen erst ab 2022-07-22 ([Doku](https://eodhd.com/financial-apis/us-stock-symbol-rename-history-api)) | Personal und Internal verboten | 1 Monat Mindestlaufzeit |
| FMP | Premium $69, Ultimate $139 ([Preise](https://site.financialmodelingprep.com/pricing-plans)) | Kurse delisteter Titel **unbelegt** | Symbol-Changes-Liste | Anzeige nur mit eigenem Vertrag, Preis nicht genannt | **unbelegt** |
| Norgate, Stooq, Alpha Vantage | siehe Recherche | – | – | Norgate und Stooq nur persönlich; Norgate nur Windows ([norgatedata.com](https://norgatedata.com/)) | – |

- **Widersprüche:** Über Nasdaq Data Link gilt für Sharadar „internal business purposes only“ ([T&C](https://data.nasdaq.com/termsandconditions)). Die Direktlizenz bei sharadar.com ist eine andere Lizenz. Ihre §§ 4 und 6 widersprechen sich bei der öffentlichen Anzeige. Abgeleitete Kennzahlen sind dort aber ausdrücklich vorgesehen.
- **Empfehlung:** Sharadar Prices Full History (299 $/Jahr). Begründung: delistete Titel und Symbolhistorie in einem Paket, dazu Sektorfelder (F12). Die Lizenz deckt abgeleitete Kennzahlen am klarsten ab. Vor dem Kauf per E-Mail bestätigen lassen: öffentliches, nicht kommerzielles Dashboard einer Privatperson mit Renditen und AR je Trade, ohne Rohkurse. Fallback: Tiingo Power, mit derselben schriftlichen Bestätigung. Abdeckung der v1-Ticker gegen Sharadar TICKERS offline messen, bevor gekauft wird. Bei jeder Quelle gilt: v2 bleibt an das Abo gebunden, weil nach der Kündigung gelöscht werden muss.

### F11 Wie wird ein Ticker zum Handelsdatum aufgelöst? (O11, O12)
- **Herkunft:** `v1:docs/sanierung/audit.md:152` (TICK-1: 1.120 Aktienzeilen falsch als ETF), `:475-476`; `GB:260`.
- **Befund:**
  - **OpenFIGI** hat keinen Datumsparameter. Ein Live-Test mit `includeUnlistedEquities=true` liefert für FB und PCLN nur die heutigen ETPs ([Doku](https://www.openfigi.com/api/documentation)). Limits: 25 Anfragen/Minute ohne Key, 250 mit Key.
  - **SEC:** `tickers` nur aktuell, aber `formerNames` mit Datum, z. B. „Facebook Inc“ 2005-05-06 bis 2021-10-27 ([submissions](https://data.sec.gov/submissions/CIK0001326801.json)). Höchstens 10 Anfragen/Sekunde, User-Agent Pflicht ([SEC](https://www.sec.gov/about/developer-resources)).
  - **Sharadar TICKERS:** recycelte Ticker haben eigene `permaticker`: ANSS1 = ANSYS (Kurse 1997-12-31 bis 2025-07-17), ANSS = ETF ab 2026-11-23. Live mit Test-Key geprüft ([Docs](https://www.sharadar.com/docs/tickers)). `firstpricedate` ist der Beginn der Kursdaten, nicht das Listing. Ob ACTIONS FB→META datiert enthält: **unbelegt** (Test-Key gesperrt).
  - **Massive:** echter `date`-Parameter in Ticker Overview ([Doku](https://massive.com/docs/rest/stocks/tickers/ticker-overview.md)).
  - **Tiingo, EODHD:** keine verlässliche Historie (siehe F10).
  - **House-PTR:** Der volle Asset-Name ist Pflicht: „Providing only a ticker symbol is not permitted“ ([Formular](https://ethics.house.gov/wp-content/uploads/2026/02/Final-CY-2025-PTR-Form-1.pdf)). Die offizielle Liste der Asset-Codes steht auf [fd.house.gov](https://fd.house.gov/reference/asset-type-codes.aspx), etwa ST Aktien, OP Optionen, EF ETF, CS Anleihen, MF Mutual Funds, CT Krypto.
- **Empfehlung:** Wertpapier-ID ist `permaticker`, nie der Ticker. Ablauf: Assetcode filtern, dann Ticker und Datum gegen das Gültigkeitsintervall prüfen, dann Namensabgleich mit dem PTR-Asset-Namen (SEC `formerNames` als Hilfe). Bei Widerspruch `unresolved`. Pseudo-Ticker und Trades ohne Ticker (in v1 rund 49 %, `v1:organisation/tool_specific_md/Trade_scraper_status.md:81`) laufen über denselben Namensabgleich, sonst `unresolved`.

### F12 Woher kommen Sektor und Industry?
- **Herkunft:** `submapper.md:16` (145 Industries, an yfinance 1.3.0 gebunden); `GB:285` (rund 20 % ohne Sektor); `v1:docs/sanierung/audit.md:175` (TICK-7).
- **Befund:** Sharadar TICKERS führt die Felder `sector`, `industry`, `sicsector`, `sicindustry` und `famaindustry`, auch für delistete Firmen ([Docs](https://www.sharadar.com/docs/tickers)). Ob `sector`/`industry` der yfinance-Taxonomie entsprechen, ist **unbelegt**.
- **Folge:** Ein Wechsel der Kursquelle trifft auch das Mapping (F29). Die 522 Zuordnungen verweisen auf yfinance-Industry-IDs.
- **Optionen:**
  1. Sektoren aus der neuen Kursquelle, einmalige Übersetzungstabelle zur Mapping-Taxonomie. Lücken bei delisteten Titeln schließen sich.
  2. yfinance nur für Sektoren weiter nutzen. Lizenzproblem (F10) und Lücken bleiben.
- **Empfehlung:** 1. Die Taxonomie als eigenen, versionierten Snapshot führen, unabhängig von der Quelle.

### F13 Welche Kongresse bekommen Ausschuss-Mitgliedschaften? (README #3)
- **Herkunft:** `README:31`; `v1:docs/sanierung/audit.md:149-151`, `:457` (E3); `GB:531`; `v1:docs/sanierung/plan-stufe2-verworfen.md:48`.
- **Befund:**

| Quelle | Abdeckung | Unterausschüsse, Rollen | Format, Lizenz |
|---|---|---|---|
| Git-Historie von `committee-membership-current.yaml` ([GitHub-API](https://api.github.com/repos/unitedstates/congress-legislators/commits?path=committee-membership-current.yaml&per_page=100)) | 211 Commits von 2012-11-09 bis 2026-11-04; Median-Abstand ca. 13 Tage, Lücken bis 177 Tage; 112. Kongress nur als Stand Ende 2012 | ja; `rank`, `title` (nicht normalisiert) | YAML, bioguide, CC0 ([README](https://github.com/unitedstates/congress-legislators/blob/main/README.md)) |
| Stewart/Woon ([House](https://dataverse.harvard.edu/api/datasets/:persistentId/?persistentId=doi:10.7910/DVN/XLIHUC), [Senate](https://dataverse.harvard.edu/api/datasets/:persistentId/?persistentId=doi:10.7910/DVN/EQ6KC7)) | 103.–117. Kongress, Stand 12.05.2021 | nur Hauptausschüsse; exakte Ein- und Austrittsdaten | Tabellen, ICPSR-ID; Dataverse CC0, MIT-Seite „may not be used commercially“ |
| GovInfo Congressional Directory ([MODS](https://www.govinfo.gov/metadata/pkg/CDIR-2022-10-26/mods.xml)) | eine bis zwei Ausgaben je Kongress seit 2011 | ja, als Text | PDF/Text, bioguide in MODS; als Stichtagsprobe |
| House Clerk `MemberData.xml` ([XML](https://clerk.house.gov/xml/lists/MemberData.xml)) | nur aktuell | ja; kein Wert „Ranking Member“ | XML, bioguide |
| senate.gov Mitgliedschafts-XML | nur aktuell | ja | HTTP 403 für Skripte |
| Congress.gov API | keine Mitgliederlisten ([Doku](https://github.com/LibraryOfCongress/api.congress.gov/blob/main/Documentation/CommitteeEndpoint.md), Issue #51 offen seit 2022) | – | – |
| ProPublica | eingestellt ([Hinweis](https://projects.propublica.org/represent/)) | – | – |

- **Optionen:**
  1. Nur ab 119. Kongress (wie v1). In v1 waren damit 69,3 % der Trades ohne Ausschussbezug (`audit.md:149`).
  2. 113.–119. aus den Git-Snapshots, 112. nur eingeschränkt. Deckt fast alle Trades ab, mit bekannter Unschärfe.
  3. Wie 2, zusätzlich Stewart/Woon für den 112. und zur Prüfung. Bei öffentlicher Nutzung erst den Lizenzwiderspruch klären.
- **Empfehlung:** 2. Stewart/Woon nur intern zur Prüfung. Das Mapping gilt bisher nur für den 119. Kongress (F29, F32).

### F14 Mitgliedschaft je Kongress oder tagesgenau?
- **Herkunft:** `v1:docs/reviews/t3-1b43496c/entscheidungen.md:8` (Vereinigung von 31 Ständen: 97,40 % gegenüber 99,84 % Abdeckung), `:25`; `v1:docs/sanierung/audit.md:172` (CM-15); `GB:396`.
- **Befund:** Aus den Git-Snapshots entstehen Intervalle von „erstmals gesehen“ bis „erstmals fehlend“. Die Unschärfe liegt meist bei rund 2 Wochen, in Lücken bei bis zu 6 Monaten (F13).
- **Empfehlung:** Tagesgenau mit `valid_from`, `valid_to` und einer Unschärfespalte. Kein Treffer, wenn der Trade in die Unschärfe fällt, sondern Status „nicht bewertbar“.

### F15 Wie wird der 120. Kongress gepflegt?
- **Herkunft:** `v1:docs/sanierung/audit.md:151` (CM-2), `:296`; `v1:docs/sanierung/plan-stufe2-verworfen.md:47`; `submapper.md:28`.
- **Warum dringend:** Beginn am 2027-01-03. Die Ausschüsse werden erst danach besetzt; Unterausschüsse können neu geschnitten werden.
- **Befund:** congress-legislators ist aktiv (letzter Commit 2026-11-22), eine Pflege im 120. ist aber nicht zugesagt. Ob der Senate-Teil trotz 403 noch aktualisiert wird, ist **unbelegt**.
- **Optionen:**
  1. congress-legislators nutzen, eigener Snapshot-Job (Clerk-XML, Senat per Browser) als Ersatz. Neue Units gezielt mappen (F29).
  2. Nur congress-legislators, ohne Ersatz.
- **Empfehlung:** 1. Bis ein freigegebenes Mapping vorliegt: Committee-Signal für Trades im 120. „nicht bewertbar“, laut melden statt still null (E3, CM-2).

### F16 Woher kommen Votes und Bill-Actions?
- **Herkunft:** `v1:docs/sanierung/audit.md:141`, `:158-160` (SCR-2/3/4), `:472` (O8: „~7–8 h je Kongress“).
- **Befund:**
  - **GovInfo BILLSTATUS-Bulk:** ab 108. Kongress, mit Actions, Ausschuss-Überweisungen, Vote-Links ([usgpo/bill-status](https://github.com/usgpo/bill-status)). Gemeinfrei nach 17 U.S.C. § 105 ([GovInfo](https://www.govinfo.gov/about/policies)). Ersetzt die vielen API-Abrufe aus v1. Alte ZIPs werden nicht neu gebaut (112-hr Stand 10.01.2024); Änderungen laufen über die Einzel-XMLs.
  - **House Clerk Roll-Call-XML:** ab 1990, Datum und Uhrzeit in ET, bioguide als `name-id` ab 2003, vereinzelt `000000` ([Beispiel](https://clerk.house.gov/evs/2012/roll001.xml)).
  - **Congress.gov API `house-vote`:** im Live-Test 115.–119. Kongress, für 112–114 leer ([ChangeLog](https://github.com/LibraryOfCongress/api.congress.gov/blob/main/ChangeLog.md)); kein Senate-Vote-Endpunkt. Key Pflicht, 5.000 Anfragen/Stunde ([README](https://github.com/LibraryOfCongress/api.congress.gov/blob/main/README.md)).
  - **Senate LIS XML:** HTTP 403, auch mit Browser-Kennung. Inhalt nur über fremden Parser-Code belegt.
  - **Voteview:** beide Kammern, alle Kongresse, live gepflegt, nur Datum ohne Uhrzeit ([Daten](https://voteview.com/data)). Eine Datenlizenz fehlt (**unbelegt**).
- **Empfehlung:** BILLSTATUS-Bulk für Bills und Actions, Clerk-XML für House-Votes, Senat über LIS (falls vom Pipeline-Rechner erreichbar) oder Voteview. ID-Abgleich über congress-legislators (`lis`, `icpsr`). Voteview vor öffentlicher Anzeige anfragen.

### F17 Werden PTR-Rohdokumente gesichert?
- **Herkunft:** Recherche Recht.
- **Befund:** Reports werden 6 Jahre nach dem Ausscheiden vernichtet (§ 13107(d), [LII](https://www.law.cornell.edu/uscode/text/5/13107)).
- **Empfehlung:** Je Trade die amtliche URL bzw. DocID speichern und das Dokument lokal archivieren, soweit die Trade-Quelle das zulässt (F06, F46).

---

## C. Fachregeln für den Import

### F18 Wie werden Trades mit Mitgliedern verknüpft?
- **Herkunft:** `v1:docs/sanierung/audit.md:176` (DASH-1: 419 statt 342 Personen); `GB:166`, `:258`; `v1:docs/reviews/t3-1b43496c/entscheidungen.md:15`.
- **Befund:** House-Index und Senate eFD liefern keine BioGuideID, nur Namen (`trade-datenquellen.md`). congress-legislators führt `bioguide`, `lis`, `icpsr` (CC0).
- **Empfehlung:** `bioguide_id` als einziger Personenschlüssel in Pipeline und Dashboard. Ohne ID aus der Quelle: Abgleich über Name, Staat, Kammer und Amtszeit, Rest als „nicht zugeordnet“ melden. Partei und Staat aus congress-legislators, nicht aus der Trade-Quelle (`entscheidungen.md:15`).

### F19 Wie werden Sonderfälle der Mitgliedschaft behandelt?
- **Herkunft:** `v1:docs/sanierung/audit.md:150` (CM-3: 575 Trades `no_membership`, 108 Kammerwechsler-Trades).
- **Fälle:** Kammerwechsel, ausgeschiedene Mitglieder mit späten Meldungen, Delegierte und Resident Commissioner, Nachrücker.
- **Optionen:** (1) Ein Status je Fall, Signale nur bei klarer Zuordnung. (2) Sonderfälle ignorieren wie in v1.
- **Empfehlung:** 1.

### F20 Welche Assetklassen gibt es, was wird ausgeschlossen? (O9, O10)
- **Herkunft:** `README:37`; `v1:docs/sanierung/audit.md:153-155` (TICK-2/3/4), `:246`, `:473-474`.
- **Befund:** Die House-Codes unterscheiden Aktien, Optionen, ETFs, ETNs, Anleihen, Fonds, REITs, nicht börsennotierte Aktien, Hedgefonds, Krypto und Sonstiges ([fd.house.gov](https://fd.house.gov/reference/asset-type-codes.aspx)). Für BDCs und Closed-End-Fonds gibt es weder bei House, OpenFIGI noch Sharadar einen eigenen Code (Sharadar führt die BDC MAIN als „Domestic Common Stock Primary Class“).
- **Optionen:**
  1. Bewertet werden nur Aktien, ADRs und REITs. Alles andere bleibt sichtbar, aber ohne Rendite und Signal.
  2. Zusätzlich Optionen als eigene Klasse mit Call/Put-Vorzeichen. Mehr Abdeckung, aber 371 PUT-Fälle mit falschem Vorzeichen in v1 zeigen das Risiko.
- **Empfehlung:** 1. BDCs als Aktie, Closed-End-Fonds ausschließen. Senate-Typen sind **unbelegt** und mit der Trade-Quelle zu prüfen.

### F21 Sind identische Zeilen echte Lots? (O3)
- **Herkunft:** `v1:docs/sanierung/audit.md:162` (PIPE-3: 10,8 % überzählige Zeilen), `:467`; `GB:261`.
- **Stand:** Die Stichprobe von ~20 Gruppen gegen die PTRs wurde nie gemacht. Sie braucht die Originaldokumente (F06).
- **Empfehlung:** Stichprobe als erste Aufgabe nach F06. Bis dahin `lot_index` in der Zeilen-ID und beide Varianten in der Event-Study.

### F22 Wie werden Korrekturen und Amendments gespeichert?
- **Herkunft:** `GB:163`, `:393`; `v1:organisation/tool_specific_md/Trade_scraper_status.md:31`.
- **Optionen:** (1) Versionieren mit „erstmals gesehen“, „zuletzt gesehen“ und „ersetzt durch“. (2) Alte Fassung überschreiben.
- **Empfehlung:** 1. Nur so bleiben Meldeverzug und Korrekturen nachvollziehbar.

### F23 Wie zählt das Owner-Feld?
- **Herkunft:** `v1:organisation/tool_specific_md/Senate_website_structure.md:55`; `Trade_scraper_status.md:30`. v1 nutzt das Feld außerhalb der Scraper nicht.
- **Optionen:** (1) Speichern, anzeigen und in der Event-Study schichten. (2) Nur Self-Trades bewerten. (3) Ignorieren wie in v1.
- **Empfehlung:** 1. Bei Spouse- und Child-Trades zurückhaltend formulieren (F35).

### F24 Wie werden Betragsspannen modelliert?
- **Herkunft:** `v1:organisation/DATA_STRUCTURE.md` (Modul 8: leere Spanne wird 0); `Trade_scraper_status.md:39`.
- **Empfehlung:** Unter- und Obergrenze als Zahl, Code der Spanne mitführen, fehlend = NULL. Anzeige als Spanne. Aggregate standardmäßig über die Untergrenze, mit Hinweis.

### F25 Wie werden Transaktionstypen in Richtungen übersetzt?
- **Herkunft:** `v1:docs/sanierung/audit.md:245` (Spalte `direction` statt 39 Importe einer privaten Funktion).
- **Empfehlung:** Eine feste Tabelle im Import: Purchase = Kauf, Sale (Full/Partial) = Verkauf, Exchange und Schenkung ohne Richtung. „Sale (Full)“ als Information speichern.

### F26 Datums-Fallback und späte Meldungen
- **Herkunft:** `v1:docs/sanierung/audit.md:173` (SIG-4: 49 Fallback-Artefakte); `GB:165`; `v1:docs/sanierung/plan-stufe2-verworfen.md:252`.
- **Empfehlung:** Fehlendes Transaktionsdatum = Meldedatum mit Flag `date_fallback`. Zeilen mit Fallback nicht in Signale zum Meldeverzug. „Late“ anhand der gesetzlichen Frist messen; „fast“ als eigenes Merkmal oder streichen (F37). Die genaue Frist mit der Trade-Quelle belegen (**unbelegt** hier).

### F27 Zeitzonen, Kongressgrenzen, Kalender
- **Herkunft:** `v1:tags/vote_timing_tag.py:250-251` (UTC, dann ohne Zeitzone); `v1:docs/sanierung/audit.md:249` („ein gemeinsamer Kongressbegriff“).
- **Befund:** BILLSTATUS speichert Vote-Zeiten in UTC, das Clerk-XML in ET (Recherche Votes, Beispiel H.R. 3606).
- **Empfehlung:** Trade- und Meldedaten als Kalenderdaten ohne Uhrzeit. Votes in America/New_York. Eine Kongresstabelle mit Start und Ende als einzige Quelle für Kongressgrenzen.

### F28 Wie sind Rendite und Abnormal Return definiert?
- **Herkunft:** `v1:docs/sanierung/audit.md:148` (ES-2), `:234`, `:248`; `GB:216-218`, `:400`; `v1:config/settings.py:529`, `:618` (Horizonte 30–365 Tage, SPY).
- **Zu entscheiden:** Anker (Transaktions- oder Meldedatum), Horizonte, Handelstage oder Kalendertage, Kurs „am oder nach“ t0, größte erlaubte Lücke, Vorzeichen bei Verkäufen, SPY mit oder ohne Dividenden.
- **Empfehlung:** Anker Transaktionsdatum (Konstrukt A), Horizonte in Handelstagen, AR gegen SPY mit Dividenden, NULL statt 0 bei Lücken über 5 Handelstagen. Die Werte als Konstanten an einer Stelle festschreiben.

---

## D. Ausschuss→Industry-Mapping

### F29 Mapping übernehmen oder Submapper neu bauen? (README #5)
- **Herkunft:** `README:33`; `submapper.md:125-129`; `v1:docs/sanierung/audit.md:273-276`, `:455` (E1).
- **Fakten:** 225 Units, 522 Zuordnungen, nur 119. Kongress. Neubau des Submappers geschätzt 970–1.450 Produktionszeilen plus 310–500 Testzeilen (`submapper.md:129`). Die Abhängigkeit von Claude-Code- und Codex-CLIs ist offen (`README:33`).
- **Optionen:**
  1. Übernehmen und von Hand pflegen. Kein Code, aber neue Units im 120. Kongress manuell.
  2. Übernehmen, Submapper kompakt neu bauen, sobald der 120. Kongress neue Units bringt.
  3. Sofort neu bauen und alles neu mappen.
- **Empfehlung:** 2. Für ältere Kongresse (F13) prüfen, ob die 119er-Zuordnungen über eine Nachfolger-Tabelle (F32) reichen.

### F30 Werden fragwürdige Zuordnungen vorher nachgeprüft?
- **Herkunft:** `submapper.md:48` (123 von 522 Zuordnungen nur mit Beleg „Recherche“, 252 aus Broad-Scope-Units); `GB:227`, `:275`; `v1:data/reference/committee_industries.csv` (Confidence 1: 1 Zeile, 2: 56 Zeilen).
- **Optionen:** (1) Die 123 Recherche-Zuordnungen und Confidence ≤ 2 einmal durchsehen. (2) Unverändert übernehmen. (3) Confidence ≤ 2 einfach herausfiltern.
- **Empfehlung:** 1, in einer Arbeitstabelle mit Beleg und Begründung.

### F31 Overrides und Ausschüsse ohne Unit
- **Herkunft:** `v1:docs/reviews/t3-1b43496c/entscheidungen.md:9-10`; `v1:data/reference/unit_overrides.csv:2-3`.
- **Fakten:** Bestätigt ist nur HSWM05. SSEV15 hat keinen Vermerk. HSQJ, JCSE, SCNC, SSCM39, SSJU27 haben keine Industries.
- **Empfehlung:** SSEV15 bestätigen. Die fünf Ausschüsse ohne Industries lassen; ihr Status lautet „kein Mapping“, nicht „kein Treffer“.

### F32 Bleiben Unit-IDs über Kongresse stabil?
- **Herkunft:** `submapper.md:15`, `:28`; Recherche Ausschüsse.
- **Befund:** `committees-historical.yaml` enthält nur Ausschüsse, an die Bills überwiesen wurden. Als Übersetzung über Kongresse taugt sie nur eingeschränkt ([README](https://github.com/unitedstates/congress-legislators/blob/main/README.md)).
- **Optionen:** (1) Eigene Nachfolger-Tabelle „Unit alt → Unit neu“ je Kongress. (2) Jeder Kongress bekommt eigene Units und eine eigene Mappingrevision.
- **Empfehlung:** 1. Sie ist die Voraussetzung, um das 119er-Mapping auf 113–118 und 120 anzuwenden.

### F33 Rollen und Vererbung vom Elternausschuss (E4)
- **Herkunft:** `README:37`; `v1:docs/sanierung/audit.md:170` (CM-5), `:458`; `GB:179`.
- **Befund:** Rollen sind in keiner Quelle normalisiert. Im Clerk-XML kommen Chair, Chairman, Chairwoman und Vice-Varianten vor, „Ranking Member“ fehlt (Recherche Ausschüsse).
- **Empfehlung:** E4 übernehmen (nur Chair und Ranking Member erben). Eine eigene Rollen-Liste (chair, ranking, vice, member, ex_officio).

---

## E. Analyse und Produkt

### F34 Braucht v2 einen Score oder nur Markierungen? (README #4)
- **Herkunft:** `README:32`; `GB:532`; `v1:docs/sanierung/audit.md:164` (ES-7: marktbereinigt kippt das Vorzeichen), `:169` (SCORE-1), `:469` (O5).
- **Optionen:**
  1. Nur erklärbare Markierungen je Trade. Einfach zu begründen, rechtlich vorsichtiger.
  2. Ein linearer Score aus geprüften Signalen. Braucht eine Event-Study als Beleg.
  3. Rendite-Vorhersage. In v1 nicht belegbar (Spearman ≈ −0,016).
- **Empfehlung:** 1. Ein Score erst, wenn die Event-Study (F40) ihn trägt.

### F35 Wie werden Markierungen öffentlich formuliert?
- **Herkunft:** Recherche Recht; v1 hatte einen „Suspicious“-Export (`audit.md:191`).
- **Empfehlung:** Neutrale Namen wie „Ausschussbezug“ statt „auffällig“. Methode und Grenzen auf der Seite erklären, kein Vorwurf eines Rechtsverstoßes, Korrekturweg angeben. Formulierungen dem Anwalt vorlegen (F05).

### F36 Ein Committee-Signal ohne Halbtreffer (E2)?
- **Herkunft:** `README:37`; `v1:docs/sanierung/audit.md:171` (CM-6: 5.474 doppelte Events), `:456`.
- **Empfehlung:** Ja. Ein Treffer nur bei passender Industry, nicht bei bloß gleichem Sektor.

### F37 Welche Signale baut v2? (README #6, O6)
- **Herkunft:** `README:34`; `v1:docs/sanierung/audit.md:470`; `v1:docs/sanierung/plan-stufe2-verworfen.md:41`; `GB:206`, `:273`.
- **Kandidaten:** committee_full, swarm_buy, contrarian, accumulative, late_report, floor_action. Streichkandidaten aus v1: trade_volume, swarm_conflict/paradox, extreme_report „fast“.
- **Optionen:** (1) Mit 2–3 Signalen starten (Ausschussbezug, Schwarmkauf, späte Meldung), weitere nur nach Test. (2) Alle v1-Signale nachbauen.
- **Empfehlung:** 1. Jedes Signal liefert „Treffer“, „kein Treffer“ oder „nicht bewertbar“ mit Grund.

### F38 Wird Vote-Timing gebaut? (O8)
- **Herkunft:** `README:34`; `GB:534`; `v1:docs/sanierung/audit.md:158`, `:174` (SIG-6), `:472`; `v1:organisation/tool_specific_md/vote_timing_audit.md:130-139`.
- **Befund:** Die Datenlage ist besser als in v1 angenommen (F16).
- **Optionen:** (1) Später, als vorab festgelegte Hypothese mit Kammerfilter. (2) Streichen. (3) Gleich mitbauen.
- **Empfehlung:** 1. Erst nach F40 mit sauberen Daten entscheiden.

### F39 Braucht v2 eine Exit-Erkennung?
- **Herkunft:** `v1:docs/sanierung/audit.md:489` (11.3: FIFO-Logik ungeprüft); `v1:docs/sanierung/plan-stufe2-verworfen.md:42`; `v1:organisation/DATA_STRUCTURE.md:1295-1302`.
- **Optionen:** (1) Zunächst nicht bauen; Renditen nur je Trade. (2) Bauen, vorher per Hand gegen eine Stichprobe prüfen.
- **Empfehlung:** 1. Nur mit Betragsspannen ist eine FIFO-Paarung ungenau.

### F40 Welche Methodik hat die Event-Study?
- **Herkunft:** `v1:docs/sanierung/audit.md:163` (ES-4), `:166` (ES-5), `:167` (ES-6), `:375-379`; `v1:docs/sanierung/plan-stufe2-verworfen.md:43`.
- **Empfehlung:** Höchstens 6 vorab festgelegte Hypothesen, A90/A120 primär, nach Richtung geschichtet, zweifach geclustert (Mitglied, Ticker-Monat), Holm-Korrektur. Sensitivitäten: ohne Top-Mitglied, mitgliedergewichtet, 2013–2020 gegen ab 2021, Lot-Varianten. Konstrukt B (Meldedatum) nur mit `knowable_date`. Läuft als lokales Skript; im Dashboard höchstens das Ergebnis.

### F41 Welche Funktionen hat das Dashboard?
- **Herkunft:** `v1:docs/sanierung/audit.md:209-214`, `:469-483` (O5, O7, O19); `v1:app/streamlit_app.py:1804-1807` (Tabs Trades, Assets, Members, Post Trade Performance, Recent, Score-Analyse).
- **Optionen:** (1) Trades (mit „Neu“-Filter), Mitglieder, Wertpapiere, Methodik. (2) Alles aus v1 inklusive Score-Editor und Score-Analyse.
- **Empfehlung:** 1. Kein öffentlicher Daten-Download, solange die Lizenzen ihn nicht erlauben.

### F42 Wie werden Datenlücken für Besucher sichtbar?
- **Herkunft:** `v1:docs/sanierung/audit.md:149` (Quote mit Nenner aller Trades), `:158`.
- **Empfehlung:** Datenstand, Abdeckung je Jahr und Anzahl nicht bewertbarer Trades immer anzeigen. Quoten je Mitglied nur über bewertbare Trades.

### F43 Sprache, Mobilansicht, Barrierefreiheit
- **Herkunft:** Neubau-Bedarf.
- **Optionen:** (1) Oberfläche Englisch, Rechtstexte Deutsch. (2) Alles Deutsch. (3) Zweisprachig.
- **Empfehlung:** 1, mit Mobilansicht als Muss.

---

## F. Architektur

### F44 Stack: Sprache, Dashboard-Technik, Bibliotheken
- **Herkunft:** `v1:deploy/README_deployment.md:7` (ca. 800 MB RAM je Sitzung), `v1:deploy/docker-compose.prod.yml:30-37` (Abbruch bei 2 GB); `v1:docs/sanierung/audit.md:88` (SCR-12); `v1:requirements.txt`.
- **Optionen:**
  1. Python-Pipeline, Streamlit mit vorberechneten schmalen Tabellen. Bekannte Technik, Speicherbedarf beherrschbar.
  2. Python-Pipeline, statische Seite aus vorberechneten Dateien. Minimaler Server, aber weniger Interaktion.
- **Empfehlung:** Python 3.12 mit getrennten Abhängigkeiten für Pipeline und App. Die Dashboard-Technik nach einem kleinen Prototyp mit echten Datenmengen wählen. Für Statistik eine geprüfte Bibliothek statt eigenem Bootstrap (`audit.md:417`).

### F45 Speicherformat, Datenmodell, Schreibweg (O14)
- **Herkunft:** `GB:389-404`; `v1:docs/sanierung/audit.md:238`, `:251`, `:478`; `v1:config/settings.py:464-466` (CSV-Master 645 MB).
- **Optionen:** (1) DuckDB oder Parquet mit normalisierten Tabellen und einer schmalen Sicht fürs Dashboard. (2) SQLite. (3) CSV-Master wie v1.
- **Empfehlung:** 1. Ein einziger Schreibweg, Datenvertrag vor dem Speichern, atomar. Signale als lange Tabelle (Trade, Signal, Status, Grund). Ein Sperrvermerk je Person (F54).

### F46 Rohdaten-Archiv und Laufmanifest
- **Herkunft:** `v1:docs/sanierung/audit.md:251`, `:357`.
- **Befund:** Tiingo und Sharadar verlangen nach Kündigung das Löschen der Rohdaten (F10).
- **Empfehlung:** Rohantworten der Quellen mit Abrufzeit archivieren; Manifest je Lauf mit Code-Revision, Quellständen, Mapping- und Taxonomie-Revision. Lizenzierte Kursdaten nur lokal und nicht im Git-Repo.

### F47 Was wird aus den v1-Referenzdaten übernommen?
- **Herkunft:** `README:16`; `v1:data/reference/`; `v1:data/reference/raw/119/manifest.json`; `v1:config/settings.py:404-421`.
- **Fakten:** `committee_industries.csv` 522 Zeilen, `unit_committee_map.csv` 225, `unit_overrides.csv` 2, `committees.csv` 230 (nur 119), `committee_memberships.csv` 4.110 (nur 119; `member_chamber` bei 4.045 Zeilen leer), `members.csv` 1.146. Das Manifest verweist auf Pfade des Matchers, die es in v2 nicht gibt. Der v1-Kurs-Cache beginnt erst 2021-05-28 und enthält Splices (`audit.md:156-157`).
- **Empfehlung:** Mapping, Unit-Zuordnung, Overrides und Taxonomie-Snapshot übernehmen (mit Prüfung F30, F31). Mitglieder, Ausschüsse und Mitgliedschaften neu aus congress-legislators erzeugen. Den Kurs-Cache nicht übernehmen. Die Test-Ausschnitte unter `v1:tests/fixtures/reference/` sind wiederverwendbar.

---

## G. Betrieb

### F48 Wo läuft die Pipeline?
- **Herkunft:** `v1:deploy/systemd/quiver-import.timer:5-8`; `v1:deploy/README_deployment.md:3`, `:143-151` (Pipeline lokal, Server ohne Keys).
- **Befund:** senate.gov und Senate eFD antworten auf Skripte mit 403 (F13, F16). Ob das vom VPS anders ist, ist **unbelegt**; das zeigt nur ein Test.
- **Optionen:** (1) Lokal wie v1, Upload eines Snapshots. Keine Keys auf dem Server. (2) Auf dem VPS. Automatischer, aber Keys und lizenzierte Daten liegen öffentlich erreichbar.
- **Empfehlung:** 1. Den Senate-Zugriff trotzdem einmal vom VPS testen.

### F49 Rhythmus und automatischer Lauf (O14)
- **Herkunft:** `v1:docs/sanierung/audit.md:392`, `:478`; `GB:262`.
- **Optionen:** (1) Täglicher Dry-Run, Speichern und Deploy nach Prüfung. (2) Voll automatisch mit Datenvertrag als Sperre. (3) Wöchentlich manuell.
- **Empfehlung:** 1. Wenn der Datenvertrag zuverlässig ist, später 2.

### F50 Monitoring und Alarm
- **Herkunft:** `v1:deploy/Dockerfile.app:43-46` (nur Healthcheck); `v1:notifications/__init__.py` (leer); `v1:docs/sanierung/audit.md:147` (Ausfall seit 2026-08 blieb unbemerkt).
- **Empfehlung:** Alarm, wenn das neueste Transaktionsdatum älter als 60 Tage ist (`audit.md:354`), ein Lauf scheitert oder ein Gate fällt. Kanal nach Wahl des Owners (E-Mail oder Push). Dazu ein externer Uptime-Check.

### F51 Backups
- **Herkunft:** `v1:organisation/DATA_STRUCTURE.md:1686-1701`; `v1:deploy/README_deployment.md:27`.
- **Empfehlung:** Rohdaten-Archiv und Referenzdaten sichern; der VPS bleibt reproduzierbar und braucht kein Backup.

### F52 Deployment und Secrets
- **Herkunft:** `v1:deploy/README_deployment.md:97-163`; `v1:deploy/docker-compose.prod.yml:9-75`; `v1:deploy/Caddyfile:13-50`; `v1:config/settings.py:58`, `:158`, `:319`.
- **Fakten v1:** Docker Compose mit Caddy (HTTPS, Sicherheits-Header, gekürzte IPs, 14 Tage Logs), manuelle rsync-Skripte, Keys nur auf dem Entwicklungsrechner.
- **Empfehlung:** Den Ablauf übernehmen, Image nur mit App-Abhängigkeiten. Keys: Congress.gov und OpenFIGI nur, falls genutzt; Kursquelle; Kontakt-User-Agent für die SEC.

---

## H. Recht in der Umsetzung

### F53 Impressum, Datenschutz, Information für Politiker
- **Herkunft:** `v1:deploy/legal/impressum.html:18-50` (4 Abschnitte), `v1:deploy/legal/datenschutz.html:21-132` (9 Abschnitte); `v1:organisation/DEPLOYMENT.md:333`.
- **Befund:**
  - § 18 Abs. 1 MStV verlangt Name und Anschrift für jedes Telemedium, das nicht ausschließlich persönlichen Zwecken dient ([MStV § 18](https://www.gesetze-bayern.de/Content/Document/MStV-18)). § 5 DDG gilt für „geschäftsmäßige, in der Regel gegen Entgelt angebotene“ Dienste ([DDG § 5](https://www.gesetze-im-internet.de/ddg/__5.html)); die IHK legt das weit aus ([IHK Karlsruhe](https://www.ihk.de/karlsruhe/fachthemen/recht/internetrecht/impressumspflichten-6266634)).
  - DSGVO Art. 13 für Besucher, Art. 14 Abs. 5 lit. b für die Politiker: öffentliche Information, wenn eine Einzelbenachrichtigung unverhältnismäßig ist ([DSGVO](https://eur-lex.europa.eu/legal-content/DE/TXT/HTML/?uri=CELEX:32016R0679)).
  - § 25 TDDDG: Speichern im Endgerät nur mit Einwilligung oder wenn unbedingt erforderlich ([TDDDG](https://www.gesetze-im-internet.de/ttdsg/__25.html)). Streamlit sendet ohne `gatherUsageStats = false` Seiten-URL, Referrer und User-Agent an einen Fivetran-Webhook und setzt eine 1-Jahres-ID ([config.toml](https://docs.streamlit.io/develop/api-reference/configuration/config.toml), [MetricsManager.ts](https://github.com/streamlit/streamlit/blob/develop/frontend/app/src/MetricsManager.ts)). v1 hat die Option bereits aus (`v1:.streamlit/config.toml:9`).
- **Empfehlung:** v1-Texte als Vorlage, an Quellen und Stack von v2 anpassen. Name, Anschrift und E-Mail ins Impressum. Art.-14-Information und Methodik ergänzen. Vor dem Livegang Cookies und Drittanfragen im Browser prüfen. Nutzungshinweis nach § 13107 übernehmen.

### F54 Umgang mit Auskunfts- und Widerspruchsanfragen
- **Herkunft:** Neubau-Bedarf; DSGVO Art. 15, 17, 21.
- **Empfehlung:** Kontaktweg in der Datenschutzerklärung, Antwortvorlage, Sperrvermerk je Person oder Trade im Datenmodell (F45). Ob ein Widerspruch greift, klärt der Anwalt (F05).

---

## I. Qualität und Arbeitsweise

### F55 Qualitätsvertrag (README #7, E5, O16)
- **Herkunft:** `README:35`, `:37`; `v1:docs/sanierung/audit.md:256-263`, `:445`, `:459`, `:480`; `v1:CONSTRAINTS.md:6-55`; `GB:455-495`.
- **Bausteine aus v1:** Grundregeln (keine neuen Unterdrückungen, keine übersprungenen Tests, keine Secrets), Zeilenbudget als Ratchet, Architekturgrenzen (App nur über die Lese-Schnittstelle, Netz nur in Adaptern, Signale unabhängig), Testlaufzeit, Ausnahmen mit Ablaufdatum, Doku nur bei Schema-, CLI- oder Architekturänderung.
- **Empfehlung:** Grundregeln und Architekturgrenzen blockierend ab dem ersten Commit. Zeilenbudget mit Zielwert aus der Planung, nicht aus v1.

### F56 Testkonzept mit aufgezeichneten Fixtures
- **Herkunft:** `v1:docs/sanierung/audit.md:416`, `:426-432`; `v1:tests/fixtures/openfigi/mapping_responses.json`; `v1:tests/test_network_canary.py:1-5` (v1: nur monkeypatch).
- **Optionen:** (1) Gekürzte, aufgezeichnete Antworten je Quelle plus manuell gestartete Live-Tests. (2) Nur synthetische Daten. (3) Test-Doubles wie in v1.
- **Empfehlung:** 1. Lizenzierte Kursdaten nicht ins Repo, wenn es öffentlich ist; dort nur synthetische Kurse. Ob das Repo öffentlich ist, entscheidet F59.

### F57 Wissensinventur der v1-Sonderfälle und Defekt-Fixtures
- **Herkunft:** `GB:445`, `:491-493`; `v1:docs/sanierung/audit.md:427-432`; `submapper.md:54`.
- **Fälle:** FB-Trade 2015, Option, Open-End-Fonds, Muni AONC und Gegenprobe GCBC, KLAC-Splice, Ticker-Recycling, doppelte Lots, versetzte H2-Texte bei House Appropriations, Datums-Fallback.
- **Empfehlung:** Vor dem Bau eine Tabelle „Sonderfall, Fundstelle in v1, übernehmen ja/nein, Testfall“. Die Sollwerte rechnet ein Mensch einmal von Hand.

### F58 Abnahmekriterien, Datengates und erster Release
- **Herkunft:** `v1:docs/sanierung/audit.md:353-383` (Messplan), `:477` (O13), `:490` (11.3); `GB:426-431`.
- **Gates:** Frische der Quelle, eindeutige Schlüssel, Anteil `unresolved`, Kursabdeckung je Jahr, Anteil NULL-Renditen, Niveausprünge in Kursen, Abdeckung von Ausschüssen und Votes, Treffer je Signal und Jahr.
- **Optionen:** (1) Kursabdeckung relativ zur erreichbaren Obergrenze je Jahr. (2) Feste 80 % je Jahr. In v1 für 2013–2019 nicht erreichbar.
- **Empfehlung:** 1. Erster Release: Trades mit Mitglied, Wertpapier, Rendite, AR und Ausschussbezug; Rechtstexte live; Abgleich einer Stichprobe mit v1 und den PTRs. Erwartete Abweichungen zu v1 vorher schriftlich festhalten.

### F59 Repo-, Branch- und Review-Konventionen
- **Herkunft:** `AGENTS.md:5` („Konventionen entstehen in der Planung“); globale Regeln zu Branch und Review-Anker.
- **Zu entscheiden:** Repo öffentlich oder privat, Tickets als GitHub Issues oder lokal, Sprache von Code und Commits, Ort für ADRs und Glossar, CI oder nur lokal.
- **Empfehlung:** Privates Repo bis zur Klärung von F05 und F10. Branch je Feature, Review vor Merge. Code und Identifier Englisch, Doku Deutsch. Review-Anker ist der aktuelle Stand von `main`.

---

## Grenzen dieser Recherche

- Die Trade-Quelle wurde bewusst nicht recherchiert.
- Nicht geprüft wurden: Inhalt des Tiingo Security Masters, Sharadar ACTIONS mit Bezahlschlüssel, Massive mit Schlüssel, Senate-eFD-Asset-Typen, Lizenz der Voteview-Daten, Zugriff auf senate.gov vom VPS, Persönlichkeits- und Äußerungsrecht.
- Kein Konto wurde angelegt. Getestet wurde nur mit öffentlichen Test-Schlüsseln (Congress.gov `DEMO_KEY`, Sharadar Test-Key).
