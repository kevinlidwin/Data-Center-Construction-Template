# Data Center Template — Hyperscale Capital-Program Dashboard

> An independent, interactive **owner's cost-and-investment model** for a representative **90 MW / 800,000 SF** hyperscale data-center campus in Northern Virginia — built as a single, self-contained HTML file with **zero external dependencies**.

**▶ Live dashboard: https://kevinlidwin.github.io/Data-Center-Construction-Template/**

---

## Overview

Data Center Template models the full owner-side capital program for a representative hyperscale data-center campus, replicating a 39-sheet cost workbook across **17 linked, interactive views**. It connects the two things owners actually underwrite — the **construction estimate** and the **investment decision** — in one place: change a cost assumption and watch total development cost, $/MW, yield-on-cost, IRR, DSCR, and development margin recompute live, tying out exactly to the underlying model at every scenario.

It was built as a self-directed portfolio project to demonstrate owner-side cost engineering for hyperscale and mission-critical construction.

## What it demonstrates

- **Construction cost estimating** — discipline-level CSA/MEP buildup, parametric $/kW and $/MW benchmarking, basis of estimate, allowances, alternates, and value engineering.
- **Investment underwriting** — a live development pro forma producing yield-on-cost, levered/unlevered IRR, DSCR, equity multiple, development margin, and exit valuation from editable owner assumptions (exit cap, NOI, leverage, escalation).
- **Risk quantification** — an editable risk register using PERT three-point estimates with probability-weighted EMV, plus σ and P50/P80/P90/P95 contingency percentiles derived live (triangular + normal approximation, reproducing a Monte Carlo result).
- **Project controls** — earned-value (SPI/CPI), a change-order log with live contingency drawdown, draw schedule, milestones, and schedule-acceleration trade-offs.
- **Decision support** — an investment-committee recommendation, scenario comparison, location-factor analysis, and an ESG / embodied-carbon view.

## Headline model outputs — base case

| Metric | Value |
|---|---|
| Total development cost | **$1.51B** |
| All-in cost intensity | **~$16.8M / MW** |
| Stabilized NOI | **$165M** |
| Yield-on-cost | **10.90%** |
| Stabilized DSCR | **2.37×** |
| Development margin | **68%** |
| P80 risk-based contingency | **$120.8M** (ΣEMV $93.8M) |

*All figures are model outputs driven by editable assumptions, not actuals.*

## The 17 modules

Home index · Executive overview · Cost analysis · Basis of estimate · Location factors · Benchmarks · Owner returns · IC summary · Compare scenarios · Delivery & controls · Power & space · Value engineering · Bids & alternates · Schedule · Milestones · Risk & contingency · ESG / carbon

## Built with

- A single self-contained **`index.html`** — **no frameworks, no build step, no external libraries, no network calls.** Everything (data model, ~2,900 lines of logic, hand-rolled SVG charts, styling) lives in one file that runs by double-clicking.
- Vanilla JavaScript, custom SVG charting, CSS.
- Browser `localStorage` for auto-save, plus JSON export/import and named-configuration management for portability.

## Companion workbook

The repo also includes **`Data_Center_Template.xlsx`** — the 39-sheet source cost model the dashboard is built from: full discipline-level construction estimate, S-curve draw schedule, earned-value tracking, development pro forma, capital stack, and a quantitative risk register. Every figure in the dashboard ties out to this workbook.

## Run it

Open `index.html` in any modern browser. No installation, no server, no internet connection required. Your edits and saved configurations persist locally in that browser.

## Note on scope

This is an **independent, illustrative model** of a *representative* hyperscale campus, built to demonstrate cost-engineering and capital-program methodology. It is **not affiliated with any actual named project**, and all figures are model outputs from editable assumptions.

## About

Built by **Kevin Lidwin**, a cost manager focused on owner-side data-center and mission-critical capital programs — bridging construction cost control and capital-program finance.
https://www.linkedin.com/kevinlidwin/ kevin.lidwin@outlook.com
