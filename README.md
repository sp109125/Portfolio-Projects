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
| [Cyclistic — Power BI build](#cyclistic-bike-share--power-bi-build) | Same question, end-to-end in Power BI from raw multi-schema files | Power BI · Power Query/M · DAX |

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

## Cyclistic Bike-Share — Power BI build

**Question:** Same business question — how do members and casual riders use the bikes differently — built entirely in Power BI to demonstrate the Power Query → DAX workflow end to end.

**Finding:** Members are commuters (12.9 min avg, peak midweek); casuals are leisure users (~3× longer rides, peak weekends, surging in summer from lakefront/tourist stations).

**Recommendation:** A weekend-framed membership offer launched in spring, targeted at lakefront/tourist stations, selling the long-ride economics casual riders already show.

**How it was built:** A full year of public Divvy data — 3.87M rides across four quarterly files in three different schemas. The core prep task was conforming all three (mapping `usertype` → `member_casual`, aligning columns, recalculating ride length from timestamps where the duration field was missing), all in Power Query/M, then DAX measures and Power BI visuals.

*The two Cyclistic projects are deliberate companions: the same business question solved on different data with different toolchains — SQL/BigQuery in one, Power BI's M-and-DAX pipeline in the other.*

