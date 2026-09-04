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

### Source files and how they map to the dashboard
The monthly Tableau/platform exports land in `~/Downloads` as three CSVs:

| File | Drives |
|---|---|
| `Pyx_Aetna_Medicare_Weekly_Activity_Report_<date>.csv` | `membersEnrolled` (distinct `UserId`), `mapData` (member `Zip` → state), screening counts (`ActivityCategory = BH Screening` rows by `ActivityName`), `careBarrier*`, `resourceReferral*`, enrollment cohorts (`FirstEncounter`) |
| `Pyx_Aetna_Medicare_Monthly_Screening_Report_<date>.csv` | `phq4Avg`, `ucla3Avg`, `medicareWellBeingAvg`, insight-card score distributions (one `Total_Score` per distinct `ScreeningId`), PRAPARE answer detail |
| `Pyx_Aetna_Medicare_Appointment_Report_<date>.csv` | Milestone boxes 7/8/9 and `awvAttestations`. `AppointmentReason` is **semicolon-delimited multi-select** — split it before counting |

Parse these with PowerShell `Import-Csv` (handles the quoted commas in `ScreeningQuestion`).

**Milestone box mapping** — count *distinct members*, attended + scheduled:
- Box 7 (GSD) ← `Diabetes Maintenance (A1c)`
- Box 8 (PDC-Statin) ← `Mail Order Pharmacy Enrollment` or `Statin Therapy Review`
- Box 9 (CBP) ← `Blood pressure check - Provider Visit`
- AWV ← `Annual Physical / Wellness Exam`

Attended and scheduled counts **overlap** (a member can have both) — never present them as addends.

**Not in these three files** (request separately): outreach volume / conversion rate / app registration, food box shipment counts, the SDoH domain rollup (Income / Food / Healthy Days / …), and billing actuals. Fields sourced elsewhere are marked `// STALE` in `D.metrics`.

### ⚠ Encoding
`index.html` is **UTF-8 without BOM** and contains emoji and typographic characters (— · ≥ −). Do **not** round-trip it through PowerShell `Get-Content`/`Set-Content` — PS 5.1 reads it as ANSI and writes UTF-8, which mangles every special character and adds a BOM. Use the Edit tool, or explicit `[System.IO.File]::ReadAllText($f, (New-Object System.Text.UTF8Encoding($false)))`.

### Monthly update checklist
All data lives in the `const D = { ... }` object near the bottom of `index.html`.

Also remember: `renderInsights()` holds the four screening insight cards (PRAPARE / PHQ-4 / UCLA-3 / Medicare Well-Being) **hardcoded outside `D`** — score averages and rubric percentages must be edited there. The SDOH need-rate and avg-needs KPI tiles above the screening grid are likewise inline in the `screeningsHTML` template.

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
