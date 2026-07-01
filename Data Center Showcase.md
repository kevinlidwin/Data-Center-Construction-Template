# Data Center Template — Detailed Project Overview

*An owner-side capital-program cost and investment model for a hyperscale data-center campus, built as a self-directed portfolio project.*

---

## Summary

Project Data Center Template is a two-part deliverable that models the full owner-side capital program for a representative **800,000 SF, 90 MW Tier III hyperscale data-center campus** in Northern Virginia:

1. **A 39-sheet Excel cost workbook** — a discipline-level construction estimate, S-curve draw schedule, earned-value tracker, development pro forma, and quantitative risk register, totaling **9,585 formulas** across **3,435 cross-sheet references**.
2. **A self-contained interactive HTML dashboard** — a zero-dependency, single-file web application (~340 KB, no frameworks, no build step) that replicates the workbook across **17 linked, editable views**, with every figure tying out live to the underlying model.

The project exists to demonstrate a specific intersection: **construction cost estimating discipline + capital-program finance + data-center domain knowledge** — the combination that owner-side cost engineering and project-controls roles in hyperscale and mission-critical construction actually require.

---

## Why this project

Most cost-estimating portfolios stop at the estimate. Most financial models stop at the pro forma. Owners need both, linked: when a cost assumption moves, the question that matters is *what happens to the return*. Project Data Center Template was built to prove that link end-to-end — from a CSI MasterFormat division-level estimate, through an S-curve draw schedule and earned-value system, into interest-during-construction, total development cost, and a full levered/unlevered returns model — with every number reconciling back to source.

---

## What it demonstrates

**Construction cost estimating**
- CSI MasterFormat division-level basis of estimate (Divisions 01–33) with documented inclusions, exclusions, and assumptions
- Parametric $/MW and $/SF benchmarking against 10 comparable hyperscale/edge/colocation projects
- Bid leveling and weighted multi-criteria evaluation across 4 GC/CMAR proposals
- Value-engineering log with accept/reject tiers, savings, and resiliency-risk flagging
- Location-factor analysis across 49 North American and international markets

**Capital-program finance**
- Development pro forma producing yield-on-cost, levered and unlevered IRR, DSCR, equity multiple, and development margin
- Capital stack (senior debt / sponsor equity) with sources-and-uses reconciliation
- Interest-during-construction calculated from loan-to-cost, rate, average-draw factor, and **construction duration explicitly reconciled to the CPM schedule** (a real inconsistency — 24-month financing assumption vs. a 30-month build — found and corrected during development; see *Methodology rigor* below)
- Variance-to-return analysis: a live cost-to-NPV/IRR bridge showing how a capital-cost change flows through to investment outcome

**Risk quantification**
- 14-line risk register using PERT three-point estimates (min/likely/max × probability)
- Probability-weighted EMV with σ derived analytically from compound Bernoulli-triangular variance
- P50/P80/P90/P95 contingency percentiles (normal approximation), reproducing a Monte Carlo–equivalent result without requiring a simulation engine
- Contingency adequacy check: carried reserve vs. P80 risk-based requirement, with the two largest exposures auto-surfaced

**Project controls**
- Earned-value management (SPI, CPI, EAC, VAC, TCPI) computed live from a planned-value S-curve
- Change-order log with live contingency drawdown and running balance
- 24→30-month draw schedule spread across 24 CSI divisions via a position-aware cubic smoothstep (with bespoke flat and declining-ramp profiles for General Conditions and Soft Costs)
- 15-gate milestone tracker from site selection through go-live, with critical-path flagging
- Schedule-acceleration trade-off log (cost-per-day-recovered across 8 independent levers)

**Decision support**
- One-page investment-committee summary with automatic ACCEPT / CONDITIONAL / REVIEW recommendation against 5 underwriting gates
- Side-by-side scenario comparison (save and compare up to 6 configurations)
- ESG/carbon view: embodied + operational carbon with a lever-based reduction model

---

## Engineering approach

**The workbook** uses defined names for the firm letterhead, data validation on 18 sheets, conditional formatting on 14 sheets, and a hidden chart-data helper sheet — the structure of a workbook built to be handed to someone else, not just to compute an answer. Every dollar figure traces through an explicit formula chain rather than a hardcoded value; the only "errors" Excel reports are 121 intentional `NA()` sentinels that stop the earned-value chart from plotting actuals beyond the data date.

**The dashboard** is hand-built: vanilla JavaScript, no React or charting library, with SVG bar/line/donut/needle/histogram charts generated by ~150 lines of custom rendering code. State persists to the browser via `localStorage` — named configurations, comparison snapshots, and an editable Basis of Estimate all survive a reload. Board-ready print/PDF packs are generated client-side. The interface is responsive across phone, tablet, and desktop breakpoints, with a dedicated present/print mode.

---

## Methodology rigor — a worked example

During development, a date-consistency audit surfaced a real discrepancy: the **interest-during-construction calculation and draw schedule assumed a 24-month build**, while the detailed CPM construction schedule (NTP → power-on → commissioning) ran **~30 months**. Reconciling it meant:

- Re-timing all 24 CSI division draw curves to a 30-month window, including two divisions with bespoke (non-smoothstep) spread logic, while preserving exact 100% allocation of the $1.088B construction budget
- Extending the earned-value table from 24 to 30 monthly periods so cumulative planned value reaches Budget at Completion exactly at month 30
- Re-deriving total development cost, yield-on-cost, IRR, DSCR, and development margin from the corrected financing cost
- Updating every built-in QC tie-check, chart range, and cross-document reference (workbook, dashboard, README) so all three artifacts agree

The result was a **~$17M increase in carried financing cost** and a **12-basis-point reduction in stabilized yield-on-cost** — a small, defensible, and fully traceable change. This is the kind of reconciliation a cost manager is actually paid to catch.

---

## Quality assurance

The deliverable was audited, not just built:

- **Formula integrity** — 9,585 formulas scanned for broken references: zero found. 3,435 cross-sheet links verified live across 36 distinct sheets.
- **Reconciliation** — draw schedule allocates exactly 100.00% of construction cost; earned-value cumulative planned value lands exactly on Budget at Completion; all 7 built-in dashboard QC tie-checks pass.
- **Interactive regression testing** — every one of the 17 dashboard views was programmatically loaded and exercised for runtime errors.
- **Edge-case hardening** — boundary inputs (0% exit cap rate, negative and >100% loan-to-cost) were deliberately tested; a division-by-zero defect this surfaced (which produced `Infinity`/`NaN` in the returns display) was traced to its source and fixed with input floors in the core valuation function, then re-verified clean against the same test matrix.
- **Cross-document consistency** — naming, headline metrics, and internal storage/export keys were swept for stale references after every model change.

---

## Headline model outputs — base case

| Metric | Value |
|---|---|
| Construction cost | $1,088.3M |
| Total development cost | $1,512.9M |
| All-in cost intensity | ~$16.8M / MW |
| Stabilized NOI | $165M |
| Yield-on-cost | 10.90% |
| Levered equity IRR | 26.7% |
| Unlevered IRR | 17.44% |
| Stabilized DSCR | 2.37× |
| Equity multiple (8-yr) | 5.20× |
| Development margin | 67.7% |
| P80 risk-based contingency | $120.8M (ΣEMV $93.8M) |

*All figures are outputs of an editable, illustrative model — not actuals, and not tied to any real named project.*

---

## The 17 dashboard modules

Home index · Executive overview · Cost analysis · Basis of estimate · Location factors · Benchmarks · Owner returns · IC summary · Compare scenarios · Delivery & controls · Power & space · Value engineering · Bids & alternates · Schedule · Milestones · Risk & contingency · ESG / carbon

---

## Where this fits

This project sits at the intersection I'm building a career toward: **owner-side cost engineering for hyperscale and mission-critical capital programs** — combining a construction-estimating background, an MBA in finance, and direct exposure to the financial mechanics (yield-on-cost, capital stack, DSCR) that owners and lenders actually underwrite against. It's also a working demonstration of the project-controls toolkit — EVM, change-order management, risk-adjusted contingency — built for portfolio-level capital program oversight.

---

## Access

- **Live dashboard:** open `Data Center Template.html` in any modern browser — no install required
- **Source workbook:** `Data_Center_Template.xlsx`
- **Repository:** see `README.md` for setup and hosting instructions

---

## Using this document

This write-up is intended as source material for three audiences:

- **LinkedIn Projects entry / post** — use the *Summary*, *Why this project*, and *Headline model outputs* sections, or the shorter pre-written versions in `Project_Cardinal_LinkedIn_Copy.md`
- **GitHub** — pair with `README.md` (technical setup) and consider adding this file as `CASE_STUDY.md` or linking it from the repo's About section
- **Interview / skills conversation** — the *Methodology rigor* and *Quality assurance* sections are written to answer "tell me about a time you caught and fixed an error" and "how do you ensure a model is reliable" directly, with specifics instead of generalities
