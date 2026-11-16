# Agents for Analysts: course pack

KAPSARC, Riyadh, 17 November 2026 · Aleš Maršál

**The question.** Why do OPEC, the IEA and the EIA disagree about world oil demand in 2026? In their September 2026 editions, 2026 demand is OPEC 105.8 mb/d, EIA 102.6 and IEA 102.4 (IEF comparison, 14 September 2026, p. 3).

## Start here

- **Prompt cards:** [agent_cards.md](agent_cards.md). Open it on a second laptop and copy each card; GitHub puts a copy button on every prompt. Card numbers match the activities on the slides.
- **Data:** green **Code** button → **Download ZIP**. Do not unzip it yourself: card 6a asks Claude Code to unpack it into `data/raw`.

## Two files you download yourself

The IEF does not allow reposting its comparisons, so they are not in this pack. Card 6a downloads them. If that is blocked, open the links and save each file in `data/raw` under the name shown:

- `2026-09_IEF_comparison.pdf`: https://www.ief.org/_resources/files/news/comparative-analysis-of-monthly-reports-on-the-oil-market/september-2026/ief-comparative-analysis-09-2026.pdf
- `2026-02_IEF_comparison.pdf`: https://www.ief.org/_resources/files/news/comparative-analysis-of-monthly-reports-on-the-oil-market/february-2026/ief-comparative-analysis-02-2026.pdf

## What is in the pack

| File | What it is | Used in |
|---|---|---|
| `agent_cards.md` | Every prompt for the practical | all activities |
| `reports/2026-09_EIA_STEO.pdf` | EIA, *Short-Term Energy Outlook*, September 2026 (Table 3a, PDF p. 33) | card 7 |
| `reports/2026-09_EIA_STEO_data.xlsx` | The data file of the same edition | optional |
| `excerpts_OPEC_IEA.md` | Exact numbers and sentences from OPEC (September 2026) and the IEA (17 June 2026), with table and PDF page | cards 8 and 9 |
| `gdp_note.md` | What each agency assumes for world GDP growth in 2026, with pages | card 8 |
| `manifest.csv` | Every file: agency, edition, publication date, source | card 6a |

## Editions

All numbers are frozen at the **September 2026** editions (IEF comparison of 14 September 2026), plus the IEF comparison of the **February 2026** editions. Exception: the IEA numbers come from its report of 17 June 2026. Newer editions are deliberately not used. Some traps are left in the data on purpose.

## Sources and reuse

- **EIA**, *Short-Term Energy Outlook*, September 2026: U.S. government work, included in full. https://www.eia.gov/outlooks/steo/
- **OPEC**, *Monthly Oil Market Report*, 10 September 2026: short excerpts for educational, non-commercial use, © OPEC Secretariat. Full report: https://www.opec.org/monthly-oil-market-report.html
- **IEA**, *Oil Market Report*, 17 June 2026: short excerpts for teaching, © IEA. Full report (subscription): https://www.iea.org/reports/oil-market-report-june-2026
- **IEF**, *Comparative Analysis of Monthly Reports on the Oil Market*, February and September 2026: links only, © IEF.

Page numbers are PDF pages. Data pack prepared by Aleš Maršál and Emre Hatipoglu (KAPSARC).
