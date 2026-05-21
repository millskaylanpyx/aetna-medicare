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
- **Program Name:** Aetna Medicare Chronic Condition Care Gap Closure Program (2026)
- **Program Type:** HEDIS Pilot — GSD (A1c) + CBP (Blood Pressure) + PDC-Statin (Pharmacy)
- **SOW:** SOW #4 · Work Order 1 · Contract Ref: CNRCT-26018
- **Line of Business:** Medicare Advantage
- **Scope:** National — All 50 States (per Work Order 1)
- **Eligible Members:** 5,255
- **Activation Target:** 1,051 (20% of eligible)
- **Program Go-Live:** May 4, 2026
- **Program Deliveries End:** December 31, 2026
- **Work Order Ultimate End Date:** May 3, 2027
- **Master SOW Term:** March 31, 2026 – March 31, 2028 (auto-renews annually)
- **NOT TO EXCEED:** $800,337 (Work Order 1)
- **Milestone Boxes:** Box 7 = A1c attestation · Box 8 = Statin adherence + mail-order pharmacy · Box 9 = BP outpatient reading (CBP)
- **Required ROI:** 1.2:1 minimum · Projected: 1.36:1 ($1,086,734 CMS reimbursement at 20% engagement)
- **CVS Signed By:** Anthony Marini, AVP Enterprise Procurement (April 10, 2026)
- **Pyx Signed By:** Cindy Jordan, CEO (April 10, 2026)
- **Key Contact (CVS):** Melissa Arthur, PMP · melissa.piechowiak@cvshealth.com
- **Key Contacts (Pyx):** Christina Rice (COO) · Kaylan Mills (Account Lead) · Stephanie Mount (Sales)

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
