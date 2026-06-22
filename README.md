# Data Analytics & BI Portfolio — Prashanth Kathiresan

Analytics and BI work spanning public-dataset analysis and live manufacturing-ERP engineering. Each project starts from a business question, shows the method, and ends with a recommendation a decision-maker can act on.

**Core stack:** Power BI (Power Query / M, DAX, semantic modeling) · BigQuery SQL · Epicor ERP (BAQ) · Python (matplotlib) · dashboard design & stakeholder analysis

[LinkedIn](https://www.linkedin.com/in/prashanth-kathiresan/)

---

## Projects

| Project | What it answers | Stack |
|---|---|---|
| [Warehouse Slotting Efficiency](#warehouse-slotting-efficiency-analysis) | Are fast-moving parts slotted close to the shipping dock? (No — and here's the $22K/yr fix) | Epicor BAQ · Power Query/M · DAX · Python |
| [Cyclistic — BigQuery / SQL build](#cyclistic-bike-share--bigquery--sql-build) | How do members vs. casual riders use the bikes, and where should Cyclistic add stations? | BigQuery SQL · interactive dashboard |
| [Google Fiber Repeat-Caller Analysis](#google-fiber--repeat-caller-analysis) | How often do customers call back after a first inquiry, and where does first-contact resolution fail? | BigQuery SQL · interactive dashboard |

---

## Warehouse Slotting Efficiency Analysis

**Question:** Are the warehouse's fast-moving (Smooth-demand) parts stored close to the shipping dock, or slotted in ways that make pickers walk farther than they should?

**Finding:** No. The densest concentration of fast-moving parts sits *farthest* from shipping, while bins beside the dock sit empty — so the most-picked bins are the longest walk away.

**Recommendation:** Re-slot the hottest far bins into the open near-dock bins, highest-leverage first. Relocating ~100 parts is estimated to save ~$22K/year and free ~1,095 labor hours (about half an FTE), modeled with a transparent sensitivity range.

**How it was built:** Epicor BAQ → Power Query/M (bin normalization) → two-table star schema → DAX `DISTINCTCOUNT` → custom Python (matplotlib) floor-plan heatmap inside Power BI. The heatmap places each bin at its true physical location, which native Power BI visuals can't reproduce.

*Data note: figures use a randomized representative sample that preserves the real distribution's shape and totals without exposing any proprietary part, customer, or volume data. The methodology is real; the numbers are a sanitized stand-in.*

---

## Cyclistic Bike-Share — BigQuery / SQL build

**Question:** How do annual members differ from casual customers, and what drives demand across season, weather, and location — before Cyclistic funds new stations?

**Finding:** Members ride short commute trips; casuals ride longer and wider, peaking on weekends and in summer. Weather is the top demand driver (daily trips correlate +0.66 with temperature; rain cuts demand ~20%), and demand concentrates in a handful of Manhattan ZIP codes.

**Recommendation:** Convert casuals with a weekend/summer-framed offer, forecast and rebalance the fleet on daily weather rather than the calendar, and add capacity in the high-demand Manhattan core first.

**How it was built:** 663K trips queried and cleaned in BigQuery (joining NYC Citi Bike, NOAA GSOD weather, and US Census boundaries), with weighted aggregation and data-integrity checks (sentinel detection, outlier handling), then a wireframed three-tab interactive dashboard.


---

## Google Fiber — Repeat Caller Analysis

**Question:** How often do customers call back after a first inquiry — and where is first-contact resolution failing, by market and issue type?

**Finding:** The overall repeat-call rate is 31.2% and holds steady week to week, but it's badly uneven underneath. Market 3 calls back 44.7% of the time (vs. 17.9% in Market 2), and issue Types 1 and 3 drive two-thirds of repeats. The single worst hotspot is Market 3 × Type 1 at 197% — nearly two callbacks for every first call.

**Recommendation:** Audit Market 3's first-contact handling first, rebuild the Type 1 / Type 3 resolution playbooks, target the Market 3 × Type 1 hotspot directly, and adopt the 31% repeat rate as a weekly-tracked first-contact-resolution KPI.

**How it was built:** Three market contact tables unioned in BigQuery into a single 1,350-row reporting table (64,939 first contacts, Q1 2022), with a defined repeat-rate metric (repeat contacts ÷ first contacts), null-handling (blank cells confirmed as true zeros via the funnel pattern), and a wireframed interactive dashboard with week/month/quarter/year granularity, trend, ranked bars, a repeat funnel, and a market × type heatmap.

