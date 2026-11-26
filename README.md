# Congresstracker v2

Neubau des Congress Trade Trackers. Die Architektur und die Konventionen entstehen in der Planung und gelten als einziger Maßstab.

**Stand:** Planung, noch kein Code.

**Entschieden (2026-11-27):** Das Dashboard ist öffentlich und hat keinen kommerziellen Zweck. Bei der Trade-Quelle bleibt Quiver möglich, andere Anbieter sind ebenfalls denkbar (`docs/recherche/trade-datenquellen.md`).

## Altbestand (v1)

Repo `Bene77-w/congress-trade-tracker`, lokal unter `/home/bene/Nextcloud/Projekte/bmb_trdprg/congress_tracker`. Seit 2026-11-25 eingefroren. Er dient nur als Nachschlagewerk für gelöste Probleme. Verweise in diesem Repo zeigen auf den Checkout von v1-`main`.

| Quelle in v1 | Nutzen für v2 |
|---|---|
| `docs/sanierung/audit.md` | Maßgeblicher Befund vom 2026-11-20: Ist-Architektur, Defekte in den Zahlen (Abschn. 4), Skizze der Modulgrenzen (Abschn. 6), Entscheidungen E1–E5 und O1–O19 (Abschn. 11). Die Entscheidungen galten der Reparatur von v1. Für v2 gelten sie erst, wenn sie unten bestätigt sind. Alle Laufzahlen stammen aus Code vor Stufe 1. |
| `data/reference/` | Mitglieder, Ausschüsse, Mitgliedschaften und das freigegebene Ausschuss→Industry-Mapping `map-fullrun-20261016` (225 Units, 522 Zuordnungen). Begründungen in `docs/reviews/t3-1b43496c/entscheidungen.md`. |
| `organisation/DATA_STRUCTURE.md`, `organisation/tool_specific_md/` | Quellfelder, Ticker-Auflösung, PTR-Scraper. Nur zum Nachschlagen, das Design ist laut Audit teilweise fehlerhaft. |

Nicht als Wahrheit verwenden: `docs/sanierung/plan-stufe2-verworfen.md` (verworfener Plan), die Zahlen und Fristen in `CONSTRAINTS.md` (beziehen sich auf v1) sowie Statusangaben in `organisation/` und `CHANGELOG.md`. Das alte Rebuild-Audit vom 2026-10-17 ist abgelöst und nur noch in der Git-Historie (`git show 4f2dfa9^:organisation/rebuild_audit/00_GESAMTBERICHT.md`).

Analysen für die Übernahme stehen unter `docs/uebernahme/`.

## Offene Entscheidungen

In dieser Reihenfolge, weil die späteren von den früheren abhängen:

| # | Frage | Stand |
|---|---|---|
| 1 | **Trade-Quelle** | Der Quiver-Export liefert seit 2026-08-03 keine Daten. Besteht das Abo noch? Sonst eigene House/Senate-PTR-Scraper oder nur historische Analyse. Blockiert alles Weitere. |
| 2 | **Kursquelle** | yfinance (kostenlos, Lücken und Survivorship) oder eine kostenpflichtige Quelle mit Delistings und Symbolhistorie. Nie entschieden. |
| 3 | **Kongressabdeckung** | Nur ab dem 119. Kongress oder historische Ausschuss-Mitgliedschaften. In v1 war das eine Notlösung (E3). |
| 4 | **Zweck des Scores** | Auffälligkeit erklärbar markieren oder Rendite vorhersagen. Braucht v2 einen Score oder nur Flags? Nie entschieden. |
| 5 | **Ausschuss→Industry-Mapping** | Bestehendes Mapping übernehmen und von Hand pflegen (Audit E1) oder den Submapper kompakt neu bauen (`docs/uebernahme/submapper.md`). Dazu: Ist die Abhängigkeit von den Claude-Code-/Codex-CLIs akzeptabel? |
| 6 | **Signale und Vote-Timing** | Welche Signale v2 baut (O6), ob Vote-Timing neu entsteht oder entfällt (O8). Belastbar erst nach einem Lauf auf sauberen Daten. |
| 7 | **Qualitätsvertrag** | Grundregeln, Architekturgrenzen und Zeilenbudget für v2. |

Fachregeln aus dem Audit, die voraussichtlich übernommen werden und noch bestätigt werden müssen: ein Committee-Signal ohne Halbtreffer (E2), Vererbung von Elternausschüssen nur an Chair und Ranking Member (E4), Lots statt Duplikate (O3), Optionen und Closed-End-Fonds ausschließen und Ticker zum Handelsdatum auflösen (O9–O12), ein Schreibweg mit Datenvertrag (O14), knappe Doku-Regel (O16).
