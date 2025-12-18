# Portfolio Risk Report (Python) — Reproducerbar risk- & dataanalys

**Kort:** En koddriven analys-pipeline som tar transaktionsliknande data och bygger en daglig portföljpanel (pris/position/exponering) + en bankig riskrapport (HTML) med VaR, volatilitet, drawdown, exponeringar och segmentanalyser.

> **Rekryterar-fokus:** visar att jag kan gå från rådata → kvalitetssäkring → analys → tydlig rapport.

## Varför projektet finns (business value)
Målet är att skapa ett robust beslutsunderlag för risk- och portföljuppföljning:
- Snabb bild av risknivå (VaR/vol/drawdown)
- Transparens i exponering (sektor, risk_rating m.m.)
- Tydlig rapport som går att dela internt (HTML + figurer + CSV-tabeller)

## Output (öppna detta först)
- **HTML-rapport:** `report/portfolio_risk_report.html`
- **Figurer:** `report/figures/`
- **Tabeller:** `report/*.csv`
- **Notebook (full pipeline):** `Financial Analysis.ipynb`

## Projektstruktur
```text
.
├─ Financial Analysis.ipynb
├─ report/
│  ├─ portfolio_risk_report.html
│  ├─ figures/
│  └─ *.csv

## Screenshots
![Report](assets/report_1.png)


