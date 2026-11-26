# Trade-Datenquellen für Kongress-Wertpapiergeschäfte (Ersatz für Quiver-Export)

**Stand der Recherche:** 2026-11-27 (alle Abrufe an diesem Datum, sofern nicht anders angegeben)
**Frage:** Welche Quelle liefert die PTRs (STOCK Act, Periodic Transaction Reports) von US-Kongressmitgliedern als Grundlage für die Entscheidung „Trade-Quelle" (README, Offene Entscheidung 1)?

**Legende:** *unbelegt* = nicht an einer Primärquelle verifiziert (Grund steht daneben). Preise, die nicht auf einer abgerufenen Seite standen, sind nicht angegeben.

## Vergleich

| Quelle | Kosten | Historie ab | Mitglieds-ID | Aktualität | Lizenz für öffentliche Anzeige | Aufwand |
|---|---|---|---|---|---|---|
| **House Clerk** (Index-ZIP + PTR-PDF) | Kostenlos laut Clerk-Angebot, Nutzungsbedingungen unbelegt | Index-ZIPs 2012, 2014, 2025, 2026 per HTTP 200 belegt; Inhalt älterer Jahre nicht geprüft | Nein im Index (nur Name, Wahlkreis, DocID). Zuordnung zu BioGuideID nötig | Index-Datei 2026 mit Zeitstempel 2026-11-25; 483 PTR-Einträge im Jahr 2026 | *unbelegt* (keine Nutzungsbedingungen im Abruf gefunden) | Mittel bis hoch: PDF-Parsing, Namensmapping, OCR für Papierformulare |
| **Senate eFD** | Kostenlos | *unbelegt* (Abruf blockiert) | Nein (nur Name). Zuordnung nötig | *unbelegt* | *unbelegt*; Zweckbindung laut Seite: 5 U.S.C. app. § 105(c) (Zitat aus Drittquelle) | Hoch: Zugang für unsere Abrufe gesperrt (HTTP 403) |
| **Quiver Quantitative API** | Hobbyist 30 $/Mo (25 $/Mo jährlich), Trader 75 $/Mo, Startup 250 $/Mo, Enterprise auf Anfrage | „ab 2014" (Quiver-Dokumentation) | **Ja**: `BioGuideID` | „jeden Werktag" | **Nein** bei Hobbyist und Trader (nur nicht kommerziell); Startup (Umsatz unter 100.000 $) und Enterprise mit kommerziellen Rechten, Weitergabe nur mit Vertrag | Niedrig (API-Client); Lizenz ist die eigentliche Hürde |
| **Disclosed Capitol API** | Core 6 $/Mo, Pro 15 $/Mo, Max 30 $/Mo (Credits-Modell) | *unbelegt* | Ja: `politician_id` (Format nicht geprüft) | *unbelegt* | Nur persönlich und Nachrichten/Medien; andere Nutzung nur mit schriftlicher Genehmigung; Bulk-Weitergabe verboten | Niedrig |
| **EODHD Congressional Trades** | Nur im Paket „All-in-One": 99,99 €/Mo bzw. 999,90 €/Jahr. Ohne Paket HTTP 403 | Ab 14.06.2012, lückenlos ab 2014 | Ja: `member.bioguide_id` (bei ca. 1/4 leer) | Abruf viermal werktags | **Nein**: Anzeige und Weitergabe im Standardvertrag ausgeschlossen | Niedrig |
| **Unusual Whales API** | Congress in allen API-Tarifen: Starter 99 $/Mo, Basic 150 $/Mo, Advanced 375 $/Mo (Aktionspreise auf Seite, Listenpreise nicht eindeutig) | Starter 1 Jahr, Basic und Advanced 2 Jahre (Lookback) | *unbelegt* (Felder nicht abgerufen) | „Echtzeit" laut FAQ | **Nein**: nur persönliche Nutzung, Weitergabe verboten; Enterprise mit Weitergabe auf Antrag | Niedrig |
| **Benzinga Government Trades** | *unbelegt* (Preisseite HTTP 403) | *unbelegt* | Ja: `filer_info.member_id` (Beispiel „B001325") | `report_date` vorhanden, Frequenz *unbelegt* | *unbelegt* | Niedrig, falls Lizenz passt |
| **Finnhub Congressional Trading** | *unbelegt* | *unbelegt* | *unbelegt* (Schema mit `amountFrom`, `transactionDate`, `filingDate` gesehen) | *unbelegt* | *unbelegt* | *unbelegt* |
| **Financial Modeling Prep** (`senate-trades`, `house-trades`) | *unbelegt* (Seiten HTTP 403) | *unbelegt* | *unbelegt* | *unbelegt* | *unbelegt* | *unbelegt* |
| **Capitol Trades** | *unbelegt* (HTTP 429) | *unbelegt* | *unbelegt* | *unbelegt* | *unbelegt*; kein offizielles API gefunden | *unbelegt* |
| **Polygon / Massive** | Kein Kongress-Endpunkt gefunden (Suche) | – | – | – | – | – |
| **House/Senate Stock Watcher** (Community) | kostenlos | – | – | **Tot** laut Drittquellen (siehe unten) | – | – |
| **Eigene Scraper** (House-Index + PDFs; Senate-eFD) | Kostenlos, Eigenaufwand | Wie Quelle | Mapping über `unitedstates/congress-legislators` (CC0) | Abhängig von Quelle | Abhängig von Quelle (Clerk-Terms unbelegt) | Siehe Abschnitt 4 |

---

## 1. Offizielle Quellen

### 1.1 House Clerk (disclosures-clerk.house.gov)

- **Index-ZIP ist maschinenlesbar und erreichbar.** `https://disclosures-clerk.house.gov/public_disc/financial-pdfs/2026FD.ZIP` liefert HTTP 200 (66.777 Bytes, Abruf 2026-11-27). Das ZIP enthält `2026FD.xml` (506 KB) und `2026FD.txt` (Tab-getrennt), Zeitstempel 2026-11-25 09:00. Quelle: eigener Download und Inspektion, nicht veröffentlicht.
- **Struktur der XML:** Je `<Member>` die Felder `Prefix`, `Last`, `First`, `Suffix`, `FilingType`, `StateDst`, `Year`, `FilingDate`, `DocID`. **Keine BioGuideID.** 1.879 Einträge im Jahr 2026.
- **FilingType:** `P` = PTR (483 Einträge 2026), `C`, `X`, `W`, `A`, `D`, `H`, `T`. Die PTRs sind über `FilingType = P` eindeutig filterbar. Ein Eintrag ist nicht gleich ein Trade.
- **PTR-PDF-URL belegt:** `https://disclosures-clerk.house.gov/public_disc/ptr-pdfs/2026/{DocID}.pdf` liefert HTTP 200, `application/pdf` (zwei Stichproben, DocIDs 20034201 und 20033751). Das Muster `financial-pdfs/{Jahr}/{DocID}.pdf` gilt für PTRs **nicht** (404), es gilt nur für andere Formulare.
- **Historie:** `2012FD.ZIP`, `2014FD.ZIP`, `2025FD.ZIP`, `2026FD.ZIP` liefern HTTP 200 (`2012FD.ZIP` mit 36 KB). Den Inhalt älterer Jahre habe ich nicht geprüft.
- **Zugriff:** Plain-Requests mit generischem User-Agent kommen ohne Captcha durch. Ob es Rate-Limits gibt: *unbelegt*.
- **Nutzungsbedingungen:** Die Seite `https://disclosures-clerk.house.gov/FinancialDisclosure` (HTTP 200) enthielt im Abruf keinen Nutzungstext. Ein Verweis auf „Terms of Service" betrifft den Member-Information-Bereich (`https://clerk.house.gov/member_info/Terms_of_Service.pdf`), nicht geprüft. Lizenz für öffentliche Anzeige: *unbelegt*.
- **Suchmaske:** `ViewMemberSearchResult` liefert HTTP 405 bei einfachem Abruf. Für die Auswertung nicht nötig, weil der Index-ZIP reicht.
- **Papier-PTRs:** Laut v1-Doku (`Trade_scraper_status.md`, Abschn. 1) sind 51 % der House-Fälle Papierformulare, deren PDFs keinen Textlayer haben. Für diese ist OCR nötig. Heute nicht neu gemessen.

### 1.2 Senate eFD (efdsearch.senate.gov)

- **Zugriff blockiert:** `https://efdsearch.senate.gov/search/home/` und `/search/` liefern HTTP 403, sowohl bei einfachem Abruf (Fetch-Tool) als auch per curl. Ursache ist nicht geklärt (Bot-Schutz oder Sperre). Ich habe keine Umgehung versucht.
- **Nutzungsbedingungen:** *unbelegt*. Die Seite verlangt laut Suchergebnis vor der Suche eine Zustimmung (Click-through, „acknowledge use prohibitions"). Den Wortlaut habe ich nicht gelesen. Die einzige belegte Aussage stammt aus einer Drittquelle (Disclosed Capitol): 5 U.S.C. app. § 105(c) macht die Nutzung „for any unlawful purpose" strafbar.
- **Format:** Laut v1-Doku (`Trade_scraper_status.md`, Abschn. 2 und 4) liefern elektronische PTRs HTML, Papier-PTRs sind GIF-Bilder bzw. PDF. Die v1-Doku nennt den Endpunkt `POST /search/report/data/` mit `length=-1`. **Heute nicht gegen die Seite geprüft**, weil der Zugriff gesperrt ist.
- **Mitglieds-ID:** Nicht geprüft. Zuordnung über Name nötig.

### 1.3 Rechtsrahmen für beide Kammern

Quelle: 5 U.S.C. § 13107 (früher Ethics in Government Act § 105), https://www.law.cornell.edu/uscode/text/5/13107, Abruf 2026-11-27. Die amtliche Fassung auf uscode.house.gov lieferte HTTP 404.

- **Geltung:** Abs. (a) nennt den Clerk of the House und den Secretary of the Senate ausdrücklich. Abs. (c) gilt für jeden „report“ ohne Einschränkung auf bestimmte Melder. Damit gilt er für die Meldungen beider Kammern. Ob PTRs unter diesen Abschnitt fallen, wurde nicht an § 13101 geprüft. Es ist aber naheliegend, weil der Clerk sie als Financial Disclosure veröffentlicht.
- **Verbotene Nutzung (Abs. (c)(1)):** Unzulässig ist es, einen Bericht zu beziehen oder zu nutzen
  - „for any unlawful purpose“,
  - „for any commercial purpose, other than by news and communications media for dissemination to the general public“,
  - zur Bonitätsprüfung von Personen,
  - für Spendenwerbung.
- **Sanktion (Abs. (c)(2)):** Zivilklage durch den Attorney General, Strafe bis 10.000 $. Eine Strafvorschrift enthält der Abschnitt nicht.
- **Aufbewahrung (Abs. (d)):** Die Berichte eines Mitglieds sind bis sechs Jahre nach seinem Ausscheiden öffentlich zugänglich. Wie weit die offizielle Historie zurückreicht, hängt deshalb vom Mitglied ab. Ob der Clerk ältere PDFs tatsächlich entfernt, ist *unbelegt*.

**Folge:** Ein öffentliches Dashboard ohne kommerziellen Zweck (keine Werbung, kein Bezahlangebot) fällt nach dem Wortlaut nicht unter das Verbot. Jede kommerzielle Nutzung wäre unzulässig, außer als Medienangebot. Das gilt unabhängig davon, ob die Daten vom Clerk, vom Senat oder von einem Anbieter kommen. Das ist eine Lesart des Wortlauts und keine Rechtsberatung.

### 1.4 Einordnung

Die House-Seite ist für einen eigenen Scraper heute belastbar. Die Senate-Seite ist für unsere Abrufe gesperrt. Ohne Klärung der Senate-Zugriffsregeln ist die Senate-Abdeckung offen.

---

## 2. Kommerzielle und API-Anbieter

### 2.1 Quiver Quantitative

- **Preise (https://api.quiverquant.com/pricing/, HTTP 200, Abruf 2026-11-27):** Hobbyist 30 $/Mo bzw. 25 $/Mo jährlich, enthält „Congress Trading". Trader 75 $/Mo bzw. 62,50 $/Mo jährlich. Startup 250 $/Mo bzw. 208,33 $/Mo jährlich, für Unternehmen unter 100.000 $ Umsatz. Enterprise „Contact for Pricing". Außerdem Black-Friday-Aktion (Hobbyist 12 $/Mo mit Code), nicht dauerhaft.
- **Kein Free-Tier** für die Quiver-API gefunden.
- **Historie:** „Trades from 2014 onward" laut https://api.quiverquant.com/datasets/congress-trades. Das widerspricht dem v1-Export (ab 2012). Herkunft der 2012-Daten bei Quiver ist *unbelegt*.
- **Felder (OpenAPI-Schema, Live- und Historical-Endpunkt):** `Representative`, `BioGuideID`, `ReportDate`, `TransactionDate`, `Ticker`, `Transaction` (Purchase/Sale), `Range` (Betragsspanne als String), `Amount` (Untergrenze), `Party`, `Description`, `TickerType`, `District`, `House`, `ExcessReturn`, `PriceChange`, `SPYChange`. Ein Feld „Asset-Name" gibt es nicht. `Description` ist der nächste Kandidat (nicht im Detail geprüft).
- **Endpunkt:** `/beta/historical/congresstrading/{ticker}` (Pfad-Parameter Ticker, Quelle: https://quiver-quantitative-f9529011.mintlify.dev/docs/api-reference/congress/historical-congress-trading.md). Der in v1 genannte Pfad `api.quiverquant.com/docs/.../historical-congress-trading-by-ticker` liefert 404. Rate-Limits: Doku verweist auf `/docs/rate-limits` (nicht geprüft).
- **Update:** „Every business day, as new STOCK Act filings are published" (Dataset-Seite).
- **Lizenz (https://www.quiverquant.com/termsofservice/, „Last Modified: June 25, 2026"):**
  - Abschn. 6: „Quiver Data is licensed for your personal, non-commercial use only."
  - Abschn. 5: Verbot, Daten „publicly display, publicly perform, republish" zu dürfen.
  - Abschn. 6: Weitergabe nur über einen „executed enterprise service agreement" oder schriftliche Erlaubnis.
  - Preisseite: Hobbyist und Trader „No Commercial Use Rights"; Startup und Enterprise mit „Commercial Use Rights".
  - Abschn. 24 verweist auf eine separate „API License Agreement" (**nicht gelesen**). Sie könnte abweichende Regeln enthalten.
- **Konsequenz:** Ein öffentliches Dashboard braucht mindestens Startup (sofern Umsatzgrenze passt) oder Enterprise. Das ist aus den Terms abgeleitet, nicht aus der API-License-Vereinbarung.
- **Abo-Status:** Ob das bestehende Quiver-Abo (Web-Export) auch den API-Zugang umfasst, ist *unbelegt*. Das kann nur der Nutzer im Konto prüfen.

### 2.2 Disclosed Capitol

- **Preise (https://www.disclosedcapitol.com/plans, HTTP 200):** Core 6 $/Mo (7.500 Credits, 120 Req/min, keine Webhooks). Pro 15 $/Mo (30.000 Credits, 240 Req/min). Max 30 $/Mo (125.000 Credits, 600 Req/min). Credits ab 10 $ ohne Abo. Jahrespreise „save up to 25 %".
- **Historische Tiefe:** *unbelegt* (weder Plan- noch Entwicklerseite nennen sie).
- **Felder (https://www.disclosedcapitol.com/developers):** `politician_id`, `politician_name`, `party`, `state`, `chamber`, `ticker`, `trade_type`, `asset_type`, `amount_range`, `transaction_date`, `disclosure_date`, `days_to_disclose`, `price_on_trade_date`, `owner`. Endpunkte u. a. `/politicians/{id}/trades`, `/tickers/{symbol}/trades`, `/trades/recent`.
- **Lizenz (https://www.disclosedcapitol.com/terms, zuletzt 10.10.2026):** Abschn. 9.1: API-Daten lizenziert für „Personal use" und „News and media use"; andere Nutzung nur mit vorheriger schriftlicher Erlaubnis. Ausgeschlossen: Weitervertrieb als Feed/API/Datenbank, Scraping. Die Auswertungen sind laut Abschn. 9 „proprietary", die Filings selbst öffentlich.
- **Konsequenz:** Öffentliche Anzeige ist nur mit schriftlicher Genehmigung erlaubt.

### 2.3 EODHD (Congressional Trades)

- **Preise (https://eodhd.com/pricing, Abruf 2026-11-27):** Nur im Paket „All-in-One" enthalten: 99,99 €/Mo oder 999,90 €/Jahr. In anderen Paketen „Not included". Ohne Paket liefert die API HTTP 403.
- **Historie:** Ab 14.06.2012, lückenlos ab 2014. Stand August 2026 laut Anbieter 45.561 Datensätze.
- **Felder (https://eodhd.com/financial-apis/congressional-trades-api):** `member.bioguide_id` (bei ca. 1/4 leer), `asset.symbol` (bei ca. 1/4 leer), `transaction.amount_range`, `amount_low`, `amount_high`, `transaction_date`, `disclosure_date`, `days_to_disclose`, `is_late`, `source.filing_url`.
- **Update:** Abruf viermal täglich an Werktagen (00, 06, 12, 19 UTC), Abgleich um 03:00 UTC.
- **Lizenz (https://eodhd.com/financial-apis/terms-conditions):** Non-Professional-Nutzer dürfen die Daten nicht „Selling, reselling, retransmitting, redistributing, displaying, or granting access to" weitergeben oder anzeigen. Kommerzielle Nutzung nur nach gesonderter Lizenzierung (https://eodhd.com/financial-apis/commercial-vs-personal-license-use).
- **Konsequenz:** Für öffentliche Anzeige ist ein gesonderter Vertrag nötig. Preis dafür: *unbelegt*.

### 2.4 Unusual Whales

- **Preise (https://unusualwhales.com/pricing?product=api, Black-Friday-Aktion):** Options Starter 99 $/Mo (765 $/Jahr), Basic 150 $/Mo (1.125 $/Jahr), Advanced 375 $/Mo (2.835 $/Jahr). Alle drei nennen „Congressional and Insider Trades". Aktionspreise minus 25 % für 3 Monate. Listenpreise sind auf der Seite nicht eindeutig trennbar.
- **Historie:** Starter 1 Jahr Lookback, Basic und Advanced 2 Jahre.
- **Felder und Update für Congress:** *unbelegt*. Die Endpunkt-Doku (api.unusualwhales.com/docs) habe ich nicht abgerufen. Laut Seite „All API plans include real-time data".
- **Lizenz (https://unusualwhales.com/public-api):** „The Unusual Whales API is strictly for personal use. Redistribution is not allowed." Enterprise (ab 625 $/Mo, jährlich) mit Weitergabe auf Antrag.
- **Konsequenz:** Für öffentliche Anzeige nicht geeignet, außer Enterprise.

### 2.5 Benzinga

- **Docs (https://docs.benzinga.com/api-reference/calendar-api/government-trades/overview.md, und `.../get-government-trades.md`), abgerufen:** Filter `date_from`/`date_to`, `pagesize` max. 1.000, `page` 0–100.000. Felder: `filer_info.member_id` (Beispiel „B001325"), `security.ticker` (im Beispiel leer), `amount` als Bandtext („$1,001 - $15,000"), `transaction_date`, `report_date`, `notification_date`.
- **Preise, Historie, Update, Lizenz:** *unbelegt*. Die Seite https://www.benzinga.com/government-trades lieferte HTTP 403.

### 2.6 Finnhub

- **Docs-Seite (https://finnhub.io/docs/api/congressional-trading) liefert HTTP 200.** Im eingebetteten Schema ist eine Kongress-Trading-Definition mit `amountFrom`, `transactionDate` und `filingDate` enthalten.
- **Preise, Plan-Zugang (Free vs. Premium), Mitglieds-ID, Historie, Lizenz:** *unbelegt*. Die Preisseite lieferte keine Plandaten.

### 2.7 Financial Modeling Prep (FMP)

- **Endpunkte laut Suchergebnis (nicht selbst abgerufen):** `stable/senate-trades`, `stable/house-trades` (Filter `symbol`), `senate-trades-by-id`, `house-trades-by-name`. Dokumentationsseiten (`site.financialmodelingprep.com/developer/docs/stable/senate-trading`) und Preisseite lieferten HTTP 403 bei Fetch und curl.
- **Free-Tier:** *unbelegt*. Eine Drittquelle nennt 250 Calls/Tag allgemein; ob Kongressendpunkte darin enthalten sind, ist nicht belegt.
- **Mitglieds-ID, Felder, Historie, Lizenz:** *unbelegt*.

### 2.8 Capitol Trades

- **capitoltrades.com liefert HTTP 429** (Rate-Limit) bei Fetch und Terms-Seite. Ein offizielles API- oder Export-Angebot ist *unbelegt*. Die Suche fand nur Drittanbieter-Scraper.
- Wegen Terms-Unbekanntheit nicht als Quelle nutzbar.

### 2.9 Polygon / Massive

- Suche nach einem Kongress-Endpunkt ergab nichts. Polygon wird nur als Kursdatenquelle erwähnt. Dokumentation nicht direkt geprüft (*unbelegt*, bitte bei Bedarf gegenprüfen).

---

## 3. Kostenlose und Community-Datensätze

| Datensatz | Status | Beleg |
|---|---|---|
| **House Stock Watcher** (housestockwatcher.com, S3-JSON) | **Tot.** Domain: DNS-Fehler (`ENOTFOUND`). S3-Datei `house-stock-watcher-data.s3-us-west-2.amazonaws.com/data/all_transactions.json`: HTTP 403 | Abruf 2026-11-27 durch Fetch-Tool. Drittquelle: https://orthogonal.info/housestockwatcher-is-dead-heres-how-to-pull-the-latest-house-trades-yourself/ (veröffentlicht 22.06.2026, aktualisiert 02.09.2026) |
| **Senate Stock Watcher** (senatestockwatcher.com) | **Tot.** Domain: DNS-Fehler | Abruf 2026-11-27 durch Fetch-Tool |
| **timothycarambat/senate-stock-watcher-data** (GitHub) | Repo erreichbar (HTTP 200), 12 Commits, keine Releases. Letztes Push-Datum auf der Seite nicht sichtbar. Drittquelle (Spiegel) nennt letzten Push 2021-03-16 | https://github.com/timothycarambat/senate-stock-watcher-data (Abruf 2026-11-27); Datum *unbelegt* an GitHub direkt |
| **unitedstates/congress-legislators** (Mitglieder-Mapping, nicht Trades) | Repo erreichbar, Lizenz CC0-1.0. Letztes Commit-Datum *unbelegt* | https://github.com/unitedstates/congress-legislators (Abruf 2026-11-27) |

**Fazit:** Die kostenlosen Trade-Datensätze sind nicht mehr nutzbar. Das Mapping über `congress-legislators` ist eine belegte, CC0-lizenzierte Basis für die BioGuideID.

---

## 4. Eigene Scraper: Aufwand und Fallstricke

Quelle für die Fallstricke: v1-Doku `organisation/tool_specific_md/Trade_scraper_status.md` (Stand 2026-03-21, nicht neu gemessen). Heute gegen die Seiten geprüft ist nur der House-Teil.

**House (heute gegen Primärquelle geprüft):**
- Index-ZIP plus PTR-PDFs erreichbar (Abschn. 1.1). Die Index-XML hat keine BioGuideID, Mapping nötig (Name, Wahlkreis-Kürzel `StateDst`, Abgleich mit `congress-legislators`).
- v1-Fallstricke, die bleiben: Textlayer fehlt bei Papierformularen (laut v1 etwa 51 % der House-Fälle), Feld-Extraktion braucht Regex-Logik, Amounts bei Formulartyp D sind v1 zufolge fehlerhaft (v1: ca. 2.500 Trades). Vision-API-Halluzinationen bei OCR (v1: 50–100 Trades). Bond-Fälligkeit als Trade-Datum (v1: ca. 100). Fehlende Ticker (v1: 49 % insgesamt).
- v1-Architektur (`scrapers/house_scraper.py`, pdfplumber, Dedup, Delta-Modus) ist im Altbestand vorhanden und reusable als Vorlage, dort aber nur lesend übernehmbar (Repo-Regel).
- Groben Aufwand: nicht geschätzt. Abhängig von OCR-Anteil und Mapping.

**Senate (heute nicht prüfbar):**
- Zugriff liefert HTTP 403. v1 nutzte `POST /search/report/data/` (DataTables-API, `length=-1`), ob das ohne Browser-Session funktioniert, ist *unbelegt*.
- v1-Fallstricke: Papier-PTRs als GIF (OCR nötig; v1: nur ein Senator betroffen und nicht produktiv genutzt), Race-Conditions bei DOM-Pagination (v1: ~16 % Varianz, gelöst über API-Aufruf).
- Ob eine automatisierte Abfrage nach den Nutzungsbedingungen zulässig ist, ist *unbelegt*. Das muss vor einem Scraper geklärt werden.

---

## 5. Empfehlung

1. **House: eigener Scraper auf Basis des offiziellen Index-ZIP und der PTR-PDFs.** Belegt maschinenlesbar, kostenlos, PTRs per `FilingType = P` filterbar. Die Lizenzlage des Clerk ist ungeklärt; sie vor einer öffentlichen Anzeige prüfen (Clerk-Terms bzw. Rückfrage).
2. **Senate: noch keine Entscheidung möglich.** Der Zugriff ist für unsere Abrufe gesperrt, und die Nutzungsbedingungen sind unbelegt. Zuerst die Bedingungen lesen (im Browser) und ggf. den Clerk-/Senate-Ansprechpartner fragen. Ein Eigenbau darf erst danach gebaut werden.
3. **Kommerzielle API nur, wenn öffentliche Anzeige Pflicht ist und Lizenz passt.** Quiver hat als einzige verifizierte Quelle eine `BioGuideID` und einen kommerziellen Tarif (Startup 250 $/Mo, sofern Umsatzgrenze passt; sonst Enterprise). Disclosed Capitol bietet günstige Pläne, verlangt aber für öffentliche Anzeige eine schriftliche Genehmigung. EODHD, Unusual Whales und die anderen Terms verbieten Anzeige oder Weitergabe im Standard.
4. **Vor der Entscheidung zu klären:** (a) Soll das Dashboard öffentlich sein, und bleibt es ohne kommerziellen Zweck? Das entscheidet über die Lizenz der Anbieter und über 5 U.S.C. § 13107(c) (Abschn. 1.3). (b) Besteht der Quiver-API-Zugang noch? (c) Umsatzgrenze für Quiver Startup.

**Begründung:** Der House-Weg ist der einzige, der heute belegt funktioniert, kostenlos ist und keine Lizenz-Hürde für eine nicht kommerzielle Anzeige hat (Abschn. 1.3), solange der Clerk nichts Gegenteiliges sagt. Die Senate-Frage bleibt offen, und eine kommerzielle API ist nur bei klarer Lizenz sinnvoll.

---

## Methodik und Grenzen

- Primärquellen per Fetch-Tool und curl mit generischem User-Agent abgerufen. Keine Konten angelegt, keine Zugangsdaten verwendet, keine .env-Dateien geöffnet, keine personenbezogenen Daten übermittelt.
- Heruntergeladen und geprüft: `2026FD.ZIP` (Inhalt inspiziert, temporäre Dateien gelöscht).
- Gesperrt bzw. nicht abrufbar: efdsearch.senate.gov (403), capitoltrades.com (429), FMP-Docs und Preisseite (403), benzinga.com/government-trades (403), Finnhub-Preisseite (nur Titel). Umgehungen wurden nicht versucht.
- Drittquellen (Suchergebnisse, Vergleichsseiten) sind als solche markiert. Preise der Black-Friday-Aktionen sind kurzfristig und nicht die Dauerpreise.
- Quiver-API-Lizenz-Anhang und Clerk-Nutzungsbedingungen: nicht gelesen.
