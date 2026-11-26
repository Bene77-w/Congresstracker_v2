# Planung Congresstracker v2

Stand 2026-11-27. Einziges Planungsdokument: Entscheidungen, offene Fragen, Befunde, Quellen. Details stehen in den verlinkten Dateien.

## Entschieden

| Datum | Entscheidung | Folge |
|---|---|---|
| 2026-11-25 | Neubau statt Sanierung. v1 ist eingefroren. | v1 dient nur als Nachschlagewerk. Seine Entscheidungen gelten erst, wenn sie hier bestätigt sind. |
| 2026-11-27 | Das Dashboard ist öffentlich und hat keinen kommerziellen Zweck. | Die Datenquellen müssen eine öffentliche Anzeige erlauben. Die Meldungen von House und Senat dürfen nicht kommerziell genutzt werden. Ein nicht kommerzielles Dashboard ist nach dem Wortlaut zulässig (5 U.S.C. § 13107(c)). |
| 2026-11-27 | Bei der Trade-Quelle bleibt Quiver möglich. Andere Anbieter sind ebenfalls denkbar. | Siehe offene Frage 1. |

## Offene Entscheidungen

In dieser Reihenfolge, weil die späteren von den früheren abhängen.

| # | Frage | Stand |
|---|---|---|
| 1 | **Trade-Quelle** | Drei Wege. (a) Eigene Abrufe beim House Clerk: kostenlos, heute erreichbar, ohne BioGuideID, rund die Hälfte Papierformulare mit Texterkennung. (b) Quiver-API: liefert die BioGuideID, die öffentliche Anzeige braucht aber den Tarif Startup für 250 $ im Monat oder eine schriftliche Erlaubnis. Hobbyist und Trader erlauben nur private Nutzung. (c) Disclosed Capitol: günstig, öffentliche Anzeige nur mit schriftlicher Genehmigung. Der Senat ist offen, weil eFD automatische Abrufe sperrt (HTTP 403) und die Nutzungsbedingungen ungelesen sind. Blockiert alles Weitere. |
| 2 | **Kursquelle** | yfinance (kostenlos, Lücken, Survivorship) oder eine kostenpflichtige Quelle mit Delistings und Symbolhistorie. Die Lizenz muss die öffentliche Anzeige erlauben. Nie entschieden. |
| 3 | **Kongressabdeckung** | Nur ab dem 119. Kongress oder auch historische Ausschuss-Mitgliedschaften. In v1 war das eine Notlösung (E3). Die offiziellen Meldungen bleiben nur bis sechs Jahre nach dem Ausscheiden eines Mitglieds öffentlich. |
| 4 | **Zweck des Scores** | Auffälligkeit erklärbar markieren oder Rendite vorhersagen. Braucht v2 einen Score oder reichen Flags? Nie entschieden. |
| 5 | **Ausschuss→Industry-Mapping** | Das bestehende Mapping übernehmen und von Hand pflegen (Audit E1) oder den Submapper kompakt neu bauen ([submapper.md](uebernahme/submapper.md)). Dazu: Ist die Abhängigkeit von den CLIs von Claude Code und Codex akzeptabel? |
| 6 | **Signale und Vote-Timing** | Welche Signale v2 baut (O6) und ob Vote-Timing neu entsteht oder entfällt (O8). Belastbar erst nach einem Lauf auf sauberen Daten. |
| 7 | **Qualitätsvertrag** | Grundregeln, Architekturgrenzen und Zeilenbudget für v2. |

Folgende Fachregeln aus dem Audit werden voraussichtlich übernommen, sind aber noch zu bestätigen:
- ein Committee-Signal ohne Halbtreffer (E2)
- Vererbung von Elternausschüssen nur an Chair und Ranking Member (E4)
- Lots statt Duplikate (O3)
- Optionen und Closed-End-Fonds ausschließen, Ticker zum Handelsdatum auflösen (O9–O12)
- ein Schreibweg mit Datenvertrag (O14)
- eine knappe Doku-Regel (O16)

## Befunde

| Thema | Kern | Datei |
|---|---|---|
| Trade-Quellen | Siehe Frage 1. House Stock Watcher und Senate Stock Watcher sind eingestellt. EODHD und Unusual Whales verbieten die Anzeige ohne Sondervertrag. FMP, Finnhub, Benzinga und Capitol Trades sind unbelegt, weil ihre Seiten die Abrufe blockiert haben. | [trade-datenquellen.md](recherche/trade-datenquellen.md) |
| Submapper | Empfehlung: kompakter Neubau mit integriertem Probelauf, 970–1.450 Produktions- und 310–500 Testzeilen. Produktiv lief Codex `gpt-6.1-sol/high` mit Prompt v3 (225 Units, 522 Paare). Dass das Modell oder die Begründungen besser waren als die Alternativen, ist nicht belegt. | [submapper.md](uebernahme/submapper.md) |
| Datenherkunft | *Recherche läuft* | `uebernahme/datenherkunft.md` |
| Alle offenen Fragen | *Recherche läuft*. Sammelt auch Fragen, die oben noch fehlen, z. B. Stack, Speicherformat, Betrieb und Abnahmekriterien. | `recherche/offene-fragen.md` |

## Quellen im Altbestand (v1)

v1 ist das Repo `Bene77-w/congress-trade-tracker`, lokal unter `/home/bene/Nextcloud/Projekte/bmb_trdprg/congress_tracker`. Die Verweise zeigen auf den Checkout von v1-`main`.

| Datei | Nutzen |
|---|---|
| `docs/sanierung/audit.md` | Maßgeblicher Befund vom 2026-11-20: <br>• Ist-Architektur <br>• Defekte in den Zahlen (Abschn. 4) <br>• Skizze der Modulgrenzen (Abschn. 6) <br>• Entscheidungen E1–E5 und O1–O19 (Abschn. 11) <br>Alle Laufzahlen stammen aus Code vor Stufe 1. |
| `data/reference/` | Mitglieder, Ausschüsse, Mitgliedschaften und das freigegebene Mapping `map-fullrun-20261016`. Die Begründungen stehen in `docs/reviews/t3-1b43496c/entscheidungen.md`. |
| `organisation/DATA_STRUCTURE.md`, `organisation/tool_specific_md/` | Quellfelder, Ticker-Auflösung und PTR-Scraper. Nur zum Nachschlagen, das Design ist laut Audit teilweise fehlerhaft. |

Nicht als Wahrheit verwenden:
- `docs/sanierung/plan-stufe2-verworfen.md`
- die Zahlen und Fristen in `CONSTRAINTS.md`
- die Statusangaben in `organisation/` und `CHANGELOG.md`
- das alte Rebuild-Audit vom 2026-10-17. Es ist nur noch in der Git-Historie: `git show 4f2dfa9^:organisation/rebuild_audit/00_GESAMTBERICHT.md`.
