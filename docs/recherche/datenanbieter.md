# Datenanbieter für Trades, Kurse und Industries

Ticket #2. Alle Abrufe am **2026-11-28**, wenn nicht anders angegeben. Zitate stehen wörtlich auf Englisch. *unbelegt* bedeutet, dass keine Primärquelle gefunden oder abrufbar war. Das ist eine Lesart der Texte und keine Rechtsberatung.

Vorgaben: öffentlich, nicht kommerziell, höchstens 250 € im Jahr, keine Handarbeit im Normalbetrieb, House und Senate ab Januar 2025.

## Vergleich Trade-Anbieter

| Anbieter | Preis/Jahr | Lizenz für öffentliche Anzeige | House/Senate | Historie ab 2025 | Verzug | Felder | Zugriff | Kurse | Industry |
|---|---|---|---|---|---|---|---|---|---|
| **Disclosed Capitol** | Core 72 $, Pro 180 $ (Monatspreis ×12; jährlich bis 25 % günstiger) | **Wahrscheinlich ja**: lizenziert für „News and media use … other publication to the general public“. Attribution nicht Pflicht. Bulk-Weitergabe verboten | beide | *unbelegt* (Endpunkt liefert „full disclosed stock-trade history“, Startjahr nicht genannt) | „within minutes“ nach Verarbeitung der Meldung | Ticker, asset_type, amount_range, transaction_date, disclosure_date, owner, chamber, politician_id (eigene ID) | REST-API, Webhooks ab Pro | `price_on_trade_date` und Performance-Felder | Sektor-Filter erwähnt, Feld *unbelegt* |
| **FMP** (Financial Modeling Prep) | Starter 228 $ (19 $/Mo jährlich) | **Nein**: nur persönlich. Anzeige braucht „Data Display and Licensing Agreement“ (Enterprise, Preis *unbelegt*) | beide (ab Starter) | ja (Starter: 5 Jahre) | „updates … as new trades or filings are released“, Takt *unbelegt* | symbol, senateID (BioGuide-Format), disclosureDate, transactionDate, owner, assetDescription, assetType, type, amount, link | REST-API | EOD ab Basic | `sector`, `industry` im Profil |
| **Quiver** API | Hobbyist 300 $, Startup 1.250 $ (1. Jahr mit Rabatt, danach 2.500 $) | **Nein** bis Trader. Startup/Enterprise „Commercial Use Rights“; Weitergabe nur mit Vertrag oder E-Mail-Erlaubnis | beide | ja (ab 2014) | „Every business day“ | *unbelegt* (Vorarbeit vom 2026-11-27 nennt BioGuideID, Range, ReportDate, TransactionDate, TickerType) | REST-API | Datensatz „Daily Equity Prices“ (Lizenz wie oben) | *unbelegt* |
| **Quiver** Export (Web) | *unbelegt* (Login nötig) | **Nein**: ToS gelten für alle „Quiver Data“ der Website | beide | ja | wie API | wie Web-Tabelle | Download nach Login, manuell | – | – |
| **EODHD** | 999,90 € (nur All-in-One) | **Nein** für Non-Professional | beide | ja (ab 2012, lückenlos ab 2014) | viermal je Werktag | member/asset/transaction/source, owner, asset_type, bioguide | REST-API | ja | Fundamentals im Paket |
| **Unusual Whales** | 765 $ (Starter, Aktionspreis) | **Nein**: „strictly for personal use“ | *unbelegt* | *unbelegt* | *unbelegt* | *unbelegt* | REST, MCP | ja | *unbelegt* |
| **Bargo** Free API | 0 | Anzeige **ja**, mit Attribution-Pflicht. Speichern und Weitergeben der Rohdaten verboten | beide | **nein**: nur letzte 3 Monate | *unbelegt* | member, chamber, state, ticker, asset, type, amount_low/high/range, transaction_date, disclosure_date | REST, MCP | est_price, recent_price | – |
| **Finnhub** | 0 (Personal) oder 3.500 $/Mo | **Nein** im Free-Plan („Personal Use“) | *unbelegt* | *unbelegt* | *unbelegt* | *unbelegt* | REST | ja | Company Profile |
| **Benzinga**, **Capitol Trades**, **Kapitol.ai**, Apify-Scraper | *unbelegt* | *unbelegt* | – | – | – | – | – | – | – |
| **House Clerk / Senate eFD** (amtlich) | 0 | Nur § 13107 (siehe unten), eigene Nutzungsbedingungen *unbelegt* | je Kammer getrennt | ja | Meldung ≤ 45 Tage nach Trade | PDF bzw. HTML, Felder selbst parsen | House: ZIP-Index + PDF; Senate: HTTP 403 | – | – |

## Vergleich Kurse und Industry

| Quelle | Preis/Jahr | Lizenz für öffentliche Anzeige | Kurse | Sektor/Industry |
|---|---|---|---|---|
| **SEC EDGAR** (`data.sec.gov`) | 0 | **Ja**: „may be copied or further distributed … without the SEC’s permission“ | – | SIC-Code und `sicDescription` je Emittent |
| **FMP** | ab 228 $ | Nein (s. o.) | EOD | `sector`, `industry` |
| **Tiingo** | 0 / 300 $ | Nein: „Internal Use Only“. Display-Lizenz 250 $/Mo (Start-ups) | EOD, 30+ Jahre | – |
| **Massive** (ehem. Polygon) | ab 29 $/Mo | Nein: „Individual use only“ | ja | – |
| **Yahoo Finance** (yfinance) | 0 | Nein: Abruf per Skript ohne Erlaubnis verboten | ja | ja |
| **Alpha Vantage** | 0 (25 Abrufe/Tag) bzw. ab 49,99 $/Mo | *unbelegt* (Terms-Seite ohne lesbaren Text) | ja | *unbelegt* |
| **Disclosed Capitol** | s. o. | wie Trades | Kurs am Handelstag, Performance | *unbelegt* |

---

## Belege

### 5 U.S.C. § 13107 (Rechtsrahmen)

Quelle: https://www.law.cornell.edu/uscode/text/5/13107 und https://www.law.cornell.edu/uscode/text/5/13105 (die amtliche Fassung auf uscode.house.gov lieferte HTTP 404).

- § 13105(l): PTRs sind fällig „Not later than 30 days after receiving notification of any transaction … but in no case later than 45 days after such transaction“. PTRs sind damit Berichte nach diesem Subchapter, und § 13107 gilt für sie.
- § 13107(c)(1): „It shall be unlawful for any person to obtain or use a report— (A) for any unlawful purpose; (B) for any commercial purpose, other than by news and communications media for dissemination to the general public; (C) for determining or establishing the credit rating of any individual; or (D) for use, directly or indirectly, in the solicitation of money for any political, charitable, or other purpose.“
- § 13107(c)(2): Zivilklage durch den Attorney General, Strafe „not to exceed $10,000“.
- § 13107(b)(2): Einsicht nur auf schriftlichen Antrag mit der Angabe, dass man „aware of the prohibitions on the obtaining or use of the report“ ist.

**Einordnung:**
- Das Verbot knüpft an die Nutzung des *Berichts* an, nicht an die Quelle. Es gilt also auch für Daten, die ein Anbieter aus den Berichten abgeleitet hat. Disclosed Capitol zitiert die Norm deshalb selbst in seinen Terms.
- Ein öffentliches Dashboard ohne kommerziellen Zweck fällt nach dem Wortlaut nicht unter (B). Werbung, Bezahlfunktionen und Spendenaufrufe auf derselben Seite würden das ändern, (D) erfasst Spendenaufrufe ausdrücklich.
- Das Gesetz gibt keine Nutzungsrechte an der Aufbereitung eines Anbieters. Dessen Lizenz gilt zusätzlich. Die Ausnahme für Medien in (B) erklärt, warum mehrere Anbieter (Disclosed Capitol) die Nutzung durch „news and media“ ausdrücklich erlauben.

### Disclosed Capitol

- Terms, https://www.disclosedcapitol.com/terms („Last updated: October 10, 2026“), Abschn. 9.1: „data you retrieve through the Disclosed Capitol API using an active API key, whether on a free or paid plan, is licensed to you for: Personal use … News and media use — reporting, newsletters, commentary, and other publication to the general public. Any other use requires our prior written permission.“
- Ebd., ausgeschlossen: „Reselling or redistributing the dataset in bulk as a standalone data feed, API, or database product substantially similar to the Service“.
- Ebd., Abschn. 9: „The underlying government filings are public records, but our aggregation, analysis, enrichment, presentation, and derived datasets are proprietary.“
- Ebd., Abschn. 9.2: „Attribution is appreciated but not required for the uses permitted under Section 9.1.“
- Doku, https://www.disclosedcapitol.com/developers: Core „$6/month“, Pro „$15/month“, Max „$30/month“, „Annual billing saves up to 25%“. Kostenloses Konto mit 750 Credits. „Every endpoint includes U.S. Senate and U.S. House STOCK Act disclosures“. „Once a filing is parsed and verified, it's available through the API within minutes.“ Beispielfelder siehe Tabelle, `owner` „is Self, SP, JT or DC“. `GET /politicians/{id}/trades` „returns that politician's full disclosed stock-trade history“.
- Historie ab welchem Jahr, Format von `politician_id` und Abbildung auf BioGuideID: *unbelegt*.

### Financial Modeling Prep

- Preise, https://site.financialmodelingprep.com/pricing-plans: Basic 0 $, Starter „$19.00/month … Billed yearly“ (monatlich 29 $), Premium 49 $, Ultimate 99 $. Matrix: „U.S. House Trades (Basic): Not included.“, „U.S. House Trades (Starter): Full Access.“, „Senate Trading Activity (Starter): Full Access.“, „Historical Data Range (Starter): 5 years.“
- Ebd.: „Displaying or redistributing data sourced from FMP requires a specific Data Display and Licensing Agreement with FMP.“ Der Tarif „Commercial Use“ (https://site.financialmodelingprep.com/pricing-plans?planType=commercial) führt nur „Enterprise … Display and Redistribution“ mit Kontaktformular, Preis *unbelegt*.
- Terms, https://site.financialmodelingprep.com/terms-of-service („Effective Date: November 17, 2026“): Lizenz „solely for your own personal, non-business and non-commercial purposes“. Acceptable Data Use Policy, Abschn. 2: Als „Commercial Use“ gilt auch „(c) incorporating FMP Data into … any product, service, application, website … that is made available to … any other person … whether or not for a fee“ und „(e) … any analysis, signals … or other information derived from or based on FMP Data“. Abschn. 3: kein „publish, post, display“ an Dritte. Auch abgeleitete Daten sind damit erfasst.
- Doku, https://site.financialmodelingprep.com/developer/docs/stable/house-trading: `stable/house-trades?symbol=…` („symbol*“ Pflicht), Beispielantwort mit den Feldern aus der Tabelle. Alle Meldungen ohne Ticker liefert `stable/house-latest?page=0&limit=100` („Maximum 250 records per request | Page maxed at 100“, https://site.financialmodelingprep.com/developer/docs/stable/house-latest). Senate analog `stable/senate-trades`.
- Profil, https://site.financialmodelingprep.com/developer/docs/stable/profile-symbol: Beispiel `"sector": "Technology"`, `"industry": "Consumer Electronics"`.

### Quiver Quantitative

- Preise, https://api.quiverquant.com/pricing/: Hobbyist „$25.00/month billed annually … Your full annual price is $300“, enthält „Congress Trading“, „* No Commercial Use Rights“. Trader 750 $/Jahr, ebenso ohne Rechte. Startup „With discount applied, your full annual price is $1,250 a year against $1,500 with monthly payments“, „Commercial Use Rights“, „only offered to companies with under $100k in annual revenue“. Enterprise „Contact for Pricing“.
- Dataset, https://api.quiverquant.com/datasets/congress-trades: „Trades from 2014 onward“, „Every business day, as new STOCK Act filings are published“.
- Terms, https://www.quiverquant.com/termsofservice/ („Last Modified: June 25, 2026“): „Quiver Data is licensed for your personal, non-commercial use only.“ „Quiver Data“ umfasst alle Daten von „Website, Mobile App, or API“. „you may not redistribute, republish, resell, sublicense, broadcast, or otherwise make Quiver Data available to any third party, whether for commercial purposes or otherwise.“ Erlaubt nur mit „An executed enterprise service agreement … or A written permission granted by Quiver Quantitative's team via email“. Eine separate „API License Agreement“ wird erwähnt, ist aber nicht öffentlich verlinkt (*unbelegt*).
- Export: https://www.quiverquant.com/congresstrading/ verlinkt „Export Data … Download our data to use for your own analysis“. https://www.quiverquant.com/export/ zeigt nur eine Anmeldemaske. Ob der Export kostenlos ist: *unbelegt*. Die Lizenz ist dieselbe wie oben. Laut README liefert der Export seit 2026-08-03 keine Daten.

### EODHD

- Preise, https://eodhd.com/pricing: Zeile „Congressional trades“ nur im Paket All-in-One „Included“, Paketpreis „€999.90/year“.
- Terms, https://eodhd.com/financial-apis/terms-conditions: Non-Professional Users sind „prohibited from: Selling, reselling, retransmitting, redistributing, displaying, or granting access to the Information“.
- Doku, https://eodhd.com/financial-apis/congressional-trades-api: „Both chambers appear from 2012 onwards“, „Filings are collected four times on each weekday“.

### Unusual Whales

- https://unusualwhales.com/public-api: „The Unusual Whales API is strictly for personal use. Redistribution is not allowed.“ API Options Starter „Personal use“, „Billed $765 a year“ (Aktionspreis, regulär 99 $/Mo).

### Bargo

- Terms, https://www.bargo.ai/free-apis/terms: Abschn. 2 „Any page … that displays Data from the API must include a clear attribution to Bargo as a clickable link“, sichtbar „Above the fold“. Abschn. 5: „Showing live results to your own end users … with attribution, is permitted … Storing the raw Data and providing it to other parties … is redistribution and is not allowed.“ Abschn. 4: Abgeleitete Werke sind erlaubt, wenn sie keine „reconstruction of the underlying raw records“ zulassen.
- Doku, https://www.bargo.ai/free-apis/congress: „this page provides the free rolling three-month API distribution“.

### Finnhub, Benzinga, Capitol Trades, weitere

- Finnhub, https://finnhub.io/pricing: Free „$0/month“ und All-In-One „$3500/month“, jeweils „License Personal Use“. Ob Kongress-Trades im Free-Plan enthalten sind: *unbelegt*.
- Benzinga: https://www.benzinga.com/apis/licensing/ HTTP 403. Preise und Lizenz *unbelegt*.
- Capitol Trades: https://www.capitoltrades.com/ HTTP 429. *unbelegt*.
- Kapitol.ai (https://kapitol.ai, „7 days for $1“) und Apify-Scraper (Suche): nicht geprüft, *unbelegt*.

### Amtliche Quellen

- House: Index `https://disclosures-clerk.house.gov/public_disc/financial-pdfs/{Jahr}FD.ZIP` und PDFs laut Vorarbeit (2026-11-27). Die Seite https://disclosures-clerk.house.gov/FinancialDisclosure enthält keinen eigenen Nutzungstext. Ein Scraper ist Eigenbau mit OCR-Anteil und widerspricht der Vorgabe ohne Handarbeit nicht, kostet aber Wartung.
- Senate: https://efdsearch.senate.gov/search/home/ liefert HTTP 403 („Access Denied“), auch im Browser. Nutzungsbedingungen *unbelegt*.

### SEC EDGAR, Tiingo, Massive, Yahoo, Alpha Vantage

- SEC API, https://www.sec.gov/search-filings/edgar-application-programming-interfaces: „These APIs do not require any authentication or API keys“. `https://data.sec.gov/submissions/CIK0000320193.json` liefert `"sic":"3571","sicDescription":"Electronic Computers"`, `"tickers":["AAPL"]`.
- Fair Access, https://www.sec.gov/about/developer-resources: „no more than 10 requests per second“. „The SEC does not allow "unclassified" bots“. Der Abruf braucht einen deklarierten User-Agent.
- Weiterverbreitung, https://www.sec.gov/about/privacy-information: „Information presented on sec.gov is considered public information and may be copied or further distributed by users of the web site without the SEC’s permission. Please consider appropriate citation to the SEC as the source.“
- Einschränkungen: SIC ist grob, gilt je Emittent und fehlt für ETFs und Fonds. Die Zuordnung Ticker→CIK über `company_tickers.json` ist *unbelegt* (nicht abgerufen).
- Tiingo, https://www.tiingo.com/about/pricing und https://www.tiingo.com/products/end-of-day-stock-price-data: „$30/month (or $300/year) for individuals“, „License Internal Use Only“. „BASE EQUITIES REDISTRIBUTION … Business Display Redistribution … $250/Month for Start-ups“.
- Massive, https://massive.com/pricing: alle angezeigten Pläne „Individual use only“. Business-Preise nicht geprüft.
- Yahoo, https://legal.yahoo.com/us/en/yahoo/terms/otos/index.html: Verboten ist „access or collect data … from our Services using any automated means … without our express, prior permission“. Damit scheidet yfinance für den Normalbetrieb aus.
- Alpha Vantage, https://www.alphavantage.co/premium/: „25 API requests per day“ frei, Premium ab „$49.99/month“. Lizenz *unbelegt*.

---

## Empfehlung

1. **Trades: Disclosed Capitol (Core oder Pro, ca. 70–180 $ im Jahr).** Disclosed Capitol ist der einzige geprüfte Anbieter, der im Budget liegt, beide Kammern abdeckt, eine API ohne Handarbeit bietet und die Veröffentlichung „to the general public“ in der Standardlizenz erlaubt. Die Lizenz ist an § 13107(c)(1)(B) ausgerichtet.
2. **Industry: SEC EDGAR (SIC), kostenlos und frei weiterverbreitbar.** Für ETFs und Fonds ohne SIC braucht es eine eigene Regel. Die Taxonomie gehört zu Release 2.
3. **Kurse: Für Release 1 die Kursfelder von Disclosed Capitol nutzen (Kurs am Handelstag, Performance).** Keine geprüfte Kursquelle im Budget erlaubt eine öffentliche Anzeige. FMP und Tiingo schließen auch abgeleitete Kennzahlen aus oder verlangen eine Display-Lizenz ab 250 $/Mo.
4. **Nicht geeignet:** Quiver (Hobbyist ohne Anzeigerecht, Startup über Budget), FMP (Anzeige nur mit Enterprise-Vertrag), EODHD, Unusual Whales und Finnhub (Lizenz und/oder Preis). Bargo nicht, weil es nur 3 Monate liefert und Speichern verbietet.
5. **Rückfallebene:** eigener House-Scraper auf dem amtlichen Index. Die Senate-Seite bleibt gesperrt.

**Offene Punkte (vom Nutzer zu klären):**
- Per E-Mail an Disclosed Capitol (admin@disclosedcapitol.com) schriftlich bestätigen lassen, dass ein öffentliches, nicht kommerzielles Dashboard unter „other publication to the general public“ fällt. Das Speichern der Trades in eigener Datenbank und die Anzeige der Kursfelder in die Anfrage aufnehmen.
- Mit den 750 Gratis-Credits prüfen: Reicht die Historie bis Januar 2025? Wie viele Credits kostet der Backfill? Lässt sich `politician_id` auf die BioGuideID abbilden?
- Optional Quiver per E-Mail um Erlaubnis zur Veröffentlichung fragen. Die Terms sehen das vor, der Ausgang ist offen.
- Ist eine Kurshistorie über Release 1 hinaus nötig? Falls ja, gibt es im Budget keine lizenzierte Quelle. Dann bleiben nur eine Anfrage bei FMP zum Display-Preis oder ein Verzicht.
- Dashboard ohne Werbung, Bezahlfunktion und Spendenaufruf betreiben (§ 13107(c)(1)(B) und (D)).
