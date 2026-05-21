# Aetna Medicare National Partnership Dashboard

## What this is
A single-page HTML dashboard for the Pyx Health account team managing the Aetna Medicare National Partnership. Deployed via GitHub Pages at **millskaylanpyx.github.io/aetna-medicare**.

Everything is one file: `index.html` — HTML + CSS + JS, all inline. No build step, no backend.

---

## File structure
```
index.html    — the entire dashboard (HTML + CSS + JS inline)
CLAUDE.md     — this file
```

---

## Program Context
- **Program Name:** Aetna Medicare National Partnership
- **Program Type:** TBD — pending SOW review
- **Line of Business:** Medicare
- **Scope:** National — multiple states under one contract
- **Markets:** TBD — to be populated from SOW
- **Program Start:** TBD
- **Program End:** TBD
- **NOT TO EXCEED:** TBD

---

## How to update the dashboard

### Monthly update checklist
All data lives in the `const D = { ... }` object near the bottom of `index.html`.

Core fields to update each month:
- `D.program.reportMonth` — e.g. "June 2026"
- `D.program.dataAsOf` — exact date of Tableau pull
- `D.program.programMonth` — e.g. "2 of 12"
- `D.metrics.*` — all metric fields from Tableau
- `D.milestones[*].actual` and `.status`
- `D.screenings[*].actual`
- `D.revenue.revenueToDate`
- `D.flags[]` — account health narrative
- `D.journey[*]` — update answers as phases progress
- `D.updates[]` — net new changes since last report

### Milestone / SLA status values
- `"pending"` — not yet reached
- `"active"` — in progress / currently trackable
- `"done"` — completed
- `"exceed"` — at or above target
- `"behind"` — below target
- `"ramping"` — accumulating, on track

---

## Deploying changes
Push to `main` — GitHub Pages auto-deploys in ~60 seconds.

```bash
git add index.html
git commit -m "Update [Month] metrics"
git push
```

---

## Brand
Pyx Health brand:
- Green: `#49a601` | Slate: `#2e4456` | Teal: `#29a4a2`
- Headlines: Roboto Slab | Body: Montserrat
- Tone: action-oriented, data-driven, warm

---

## Related projects
- Wellcare Indiana: `millskaylanpyx/wellcare-indiana` → millskaylanpyx.github.io/wellcare-indiana
- Molina DSNP Stars: `rswan-code/molina-stars-partnership` → rswan-code.github.io/molina-stars-partnership

---

## Owner
Kaylan Mills — kaylan.mills@pyxhealth.com
