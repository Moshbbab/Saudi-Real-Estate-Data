# Real Estate Data — Analysis Ideas & Use Cases

<p align="center">
  <a href="https://rega.gov.sa"><img src="" height="50" alt="REGA - Real Estate General Authority (الهيئة العامة للعقار)"></a>
  &nbsp;&nbsp;&nbsp;&nbsp;
  <a href="https://moj.gov.sa"><img src="" height="50" alt="MOJ - Ministry of Justice (وزارة العدل)"></a>
</p>

**Created:** 2026-03-12
**Status:** Living document — brainstorming phase
**Data sources:** MOJ transactions (5M rows), REGA indicators, Ejar rentals (104K), regulatory events

---

## Data Capability Summary (from audits)

### What we CAN do
- Track sale prices, volumes, and area by region/city/district quarterly (2020–2025)
- Distinguish residential/commercial/agricultural/industrial (use classification)
- Distinguish land vs built property — **only for 2023 Q1–Q3** (نوع العقار) and REGA aggregates
- Track seizure and release volumes by area (Riyadh only in 2025 data)
- Track mortgage issuance and release volumes
- Track enforcement (court-ordered) sales
- Track property division, merging, deed updates
- Track rental indicators by region (REGA) + actual Ejar contracts
- Overlay regulatory events (White Land Tax phases, vacant property fines) with known dates and districts

### What we CANNOT do (yet)
- Link individual assets across transaction categories (no shared property ID in open data)
- Distinguish land vs built for 2020–2022 and 2024+ (must infer from price/area patterns)
- Track individual asset lifecycles (seizure → release → sale)
- Identify specific properties subject to White Land Tax

### Workarounds to explore
- **Price/area inference:** Establish price-per-m² benchmarks for land vs built in each district using 2023 Q1–Q3 labeled data, then apply those ranges to classify unlabeled periods
- **Probabilistic matching:** Composite key matching (region + city + date proximity + area) for sales data where both price and area exist
- **REGA aggregate cross-check:** Use REGA's property-type breakdowns to validate/calibrate our inferences

---

## Analysis Ideas — Market Dynamics

### 1. Price per m² trend by district (2020→2025)
- **Data needed:** MOJ sales (1.4M rows)
- **Challenge:** Can't distinguish land vs built except 2023 Q1–Q3. Mixed asset types inflate noise.
- **Workaround:** Use 2023 labeled data to establish land vs built price bands per district, then segment other years probabilistically. Also use REGA aggregates (which have type breakdowns) as calibration.
- **Feasibility:** Medium — viable with inference layer
- **Uniqueness:** High — no one publishes district-level trends publicly
- **Commercial potential:** High — developers, investors, banks

### 2. Transaction volume trend by city
- **Data needed:** MOJ sales
- **Challenge:** Minimal — straightforward count + group by
- **Feasibility:** High
- **Uniqueness:** Medium — REGA publishes some aggregate indicators
- **Commercial potential:** Medium

### 3. Residential vs commercial vs agricultural price divergence
- **Data needed:** MOJ sales (تصنيف العقار field)
- **Challenge:** Only 4 categories. Within "residential," land and villas behave very differently.
- **Enhancement:** Layer in نوع العقار from 2023 files and REGA type breakdowns for deeper segmentation
- **Feasibility:** High for broad categories, medium for subtypes
- **Uniqueness:** High — cross-classification divergence analysis not published
- **Commercial potential:** High

### 4. Seasonal patterns — which quarters consistently outperform?
- **Data needed:** MOJ sales, 24 quarters of data
- **Challenge:** Need to separate seasonality from trend. Also Ramadan/Hajj timing shifts each year.
- **Feasibility:** High
- **Uniqueness:** Medium
- **Commercial potential:** Medium — timing guidance for investors

### 5. Emerging cities — low base, high growth
- **Data needed:** MOJ sales across all 175 cities
- **Challenge:** Small city data may be noisy (few transactions per quarter)
- **Feasibility:** High
- **Uniqueness:** High — no one is ranking emerging cities by growth rate
- **Commercial potential:** High — early-mover advantage for investors/developers

### 6. Average deal size + lot/unit size trends
- **Data needed:** MOJ sales (price + area fields)
- **Challenge:** More insightful if segmented by asset type. Median better than mean for skewed data.
- **Enhancement:** Track median lot size for land deals, median unit size for apartments (where identifiable). Are developers building smaller? Are lots being subdivided?
- **Feasibility:** High
- **Uniqueness:** High
- **Commercial potential:** Medium — market structure insight

---

## Analysis Ideas — Distress & Opportunity

### 7. Seizure-to-release ratio by district
- **Data needed:** MOJ seizure (737K) + release (506K)
- **Challenge:** Both limited to Riyadh in 2025 data. No asset-level linking — aggregate ratios only.
- **Feasibility:** Medium (Riyadh only, aggregate)
- **Uniqueness:** High — not published anywhere
- **Commercial potential:** High — distress signal for opportunity hunters

### 8. Seizure volume trend as financial stress indicator
- **Data needed:** MOJ seizure, quarterly
- **Challenge:** Only 3 quarters of data (2025 Q1–Q3). Need more history for trend.
- **Feasibility:** Low now, improves with future data collection
- **Uniqueness:** High
- **Commercial potential:** High

### 9. Enforcement sale prices vs market prices
- **Data needed:** MOJ enforcement sales (8K rows) + MOJ sales for same districts
- **Challenge:** Enforcement sales have NO price or area field — only reference number, date, city, and document type. Cannot compute discount.
- **Feasibility:** Low — missing price data in enforcement
- **Uniqueness:** Would be extremely high if feasible
- **Commercial potential:** Very high

### 10. Seizure spike → price decline delay
- **Data needed:** Seizure volumes + sales prices by district over time
- **Challenge:** Seizure data limited to Riyadh 2025. Need multi-year series to establish lag patterns.
- **Feasibility:** Low now
- **Uniqueness:** Very high
- **Commercial potential:** Very high

### 11. High seizure + high new mortgage districts = overleveraged areas
- **Data needed:** Seizure + mortgage volumes by district
- **Challenge:** Seizure is Riyadh only. Mortgage data covers all regions but only 3 quarters.
- **Feasibility:** Medium (Riyadh only)
- **Uniqueness:** Very high
- **Commercial potential:** High — banking/risk assessment

---

## Analysis Ideas — Mortgage & Lending

### 12. Mortgage volume vs sale volume — financing penetration rate
- **Data needed:** MOJ mortgage (36K) + MOJ sales
- **Challenge:** Different time coverage. Mortgage data is 2025 only, sales go back to 2020.
- **Feasibility:** Medium (limited to 2025 comparison)
- **Uniqueness:** High
- **Commercial potential:** High — banking sector interest

### 13. Mortgage release trend — repayment velocity
- **Data needed:** MOJ mortgage release (43K)
- **Challenge:** Only 2025 Q1–Q3. Trend needs more periods.
- **Feasibility:** Low now, improves over time
- **Uniqueness:** High
- **Commercial potential:** Medium

### 14. Net mortgage position by district
- **Data needed:** Mortgage (new) minus mortgage release by area
- **Challenge:** Same time limitation. Aggregate only (no property linking).
- **Feasibility:** Medium (snapshot, not trend)
- **Uniqueness:** High
- **Commercial potential:** High — leverage hotspot identification

### 15. RE Development Fund POA concentration
- **Data needed:** MOJ POA RE Fund (7K rows)
- **Challenge:** Small dataset. Shows where government-backed lending is concentrated.
- **Feasibility:** High
- **Uniqueness:** Medium
- **Commercial potential:** Medium — policy/development correlation

---

## Analysis Ideas — Ownership & Development Signals

### 16. Property division (فرز) hotspots
- **Data needed:** MOJ division (90K rows)
- **Challenge:** High volume, indicates active subdivision. But is it development or liquidation?
- **Cross-reference:** Layer with White Land Tax zone data — division in taxed zones likely = liquidation. Division in untaxed growth areas likely = development.
- **Feasibility:** High
- **Uniqueness:** Very high
- **Commercial potential:** High — supply pipeline indicator

### 17. Property merge hotspots — consolidation signal
- **Data needed:** MOJ merge RE (10K rows)
- **Challenge:** Small volume. Could indicate developer land assembly or administrative cleanup.
- **Feasibility:** High
- **Uniqueness:** High
- **Commercial potential:** Medium

### 18. Old deed registration by area — formalization map
- **Data needed:** MOJ register old deed (143K rows)
- **Challenge:** High volume. Shows where legacy ownership is being formalized — precursor to development or sale.
- **Feasibility:** High
- **Uniqueness:** High
- **Commercial potential:** Medium — development readiness indicator

### 19. Deed update activity — title cleanup map
- **Data needed:** MOJ deed updates (28K)
- **Feasibility:** High
- **Uniqueness:** Medium
- **Commercial potential:** Low–Medium

### 20. Physical registration (عيني) adoption rate
- **Data needed:** MOJ physical registration (501K — large dataset)
- **Challenge:** Shows rollout of the new property identity system. Geographic adoption patterns.
- **Feasibility:** High
- **Uniqueness:** Medium
- **Commercial potential:** Low — mostly governance interest

---

## Analysis Ideas — Rental & Yield

### 21. Gross rental yield by neighborhood
- **Data needed:** REGA rental indicators + MOJ sales prices
- **Challenge:** Different granularity (REGA is aggregate, MOJ is transactional). Need to aggregate MOJ to match.
- **Feasibility:** Medium
- **Uniqueness:** High — nobody publishes computed yields
- **Commercial potential:** Very high — direct investment decision input

### 22. Ejar actuals vs REGA indicators — accuracy check
- **Data needed:** Ejar collector (104K) + REGA rental indicators
- **Challenge:** Matching geography/time periods between the two sources.
- **Feasibility:** Medium
- **Uniqueness:** High — tests whether official stats reflect reality
- **Commercial potential:** Medium — data quality insight

### 23. Rental yield trend — compression analysis
- **Data needed:** Time series of both rental and sale data
- **Challenge:** Rental data (REGA) limited to 2019–2024. Need overlapping periods.
- **Feasibility:** Medium
- **Uniqueness:** High
- **Commercial potential:** High — bubble/value signal

### 24. High yield + low appreciation = cash flow plays
- **Data needed:** Combined yield + price trend analysis
- **Feasibility:** Medium (depends on #21 and #1 working)
- **Uniqueness:** Very high
- **Commercial potential:** Very high — direct investment strategy

### 25. Low yield + high appreciation = speculative markets
- **Data needed:** Same as #24
- **Feasibility:** Medium
- **Uniqueness:** Very high
- **Commercial potential:** Very high — risk identification

---

## Analysis Ideas — Cross-Source Signals

### 26. Seizure → enforcement → price impact chain
- **Data needed:** Seizure + enforcement + sales
- **Challenge:** No asset-level linking. Enforcement has no price. Aggregate correlation only.
- **Feasibility:** Low
- **Uniqueness:** Extremely high if feasible
- **Commercial potential:** Very high

### 27. Mortgage release surge + rising sales = refinancing into upgrades?
- **Data needed:** Mortgage release + sales by area/time
- **Challenge:** Limited overlap periods. Aggregate correlation.
- **Feasibility:** Medium
- **Uniqueness:** High
- **Commercial potential:** Medium

### 28. POA volume as leading indicator for transactions
- **Data needed:** POA (758K — large) + sales
- **Challenge:** POA is 2025 only. Need more history to establish lead-lag.
- **Feasibility:** Low now
- **Uniqueness:** High
- **Commercial potential:** High if confirmed

### 29. Division (فرز) volume → subsequent sale volume — supply pipeline
- **Data needed:** Division + sales by area/quarter
- **Challenge:** Division is 2025 only. Sales go back to 2020. Limited overlap.
- **Enhancement:** As we collect more quarters, this becomes testable.
- **Feasibility:** Low now, medium over time
- **Uniqueness:** Very high
- **Commercial potential:** High — supply forecasting

### 30. Register-without-deed clusters — informal ownership map
- **Data needed:** MOJ register-no-deed (21K rows)
- **Challenge:** Small volume. But concentrated areas may indicate informal/unregistered ownership hotspots — potential development friction or opportunity.
- **Feasibility:** High
- **Uniqueness:** Very high
- **Commercial potential:** Medium — due diligence tool

---

## Analysis Ideas — Regulatory Impact

### 31. White Land Tax impact — before/after by district
- **Data needed:** Sales + regulatory event timeline
- **Approach:** Compare transaction volume and prices in Tier 1 districts (10% fee) vs untaxed control districts in same city, 3 months before vs after enforcement dates.
- **Key dates:** Jan 2026 (first 60K Riyadh invoices), Phase 1 cities from 2017
- **Feasibility:** High for Riyadh (known zone maps), medium for other cities
- **Uniqueness:** Extremely high
- **Commercial potential:** Very high — policy impact quantification

### 32. Vacant property fine — rental market impact
- **Data needed:** Ejar contracts + regulatory timeline
- **Approach:** Monitor Ejar contract volume and rental rates in affected districts after fine announcements. Expect supply increase and price softening.
- **Key dates:** Regulations expected May 2026
- **Feasibility:** Medium (regulations not yet issued)
- **Uniqueness:** Very high
- **Commercial potential:** Very high

### 33. White Land Tax → division (فرز) correlation
- **Data needed:** Division volumes in taxed vs untaxed zones
- **Approach:** Do taxed zones show higher subdivision rates? This indicates owners breaking up land to sell parcels rather than pay the annual fee.
- **Feasibility:** High
- **Uniqueness:** Very high
- **Commercial potential:** High

### 34. Forced rental market entry — rental price elasticity
- **Data needed:** Ejar data + vacancy proxies + regulatory timeline
- **Approach:** As vacant fines push idle properties into rental market, measure the rental rate response in each district. Districts with already-high supply will see sharper drops.
- **Feasibility:** Medium (needs vacancy proxy, regulations pending)
- **Uniqueness:** Very high
- **Commercial potential:** Very high

### 45. Systematic regulatory text ingestion → data-strategy guidance loop
- **Data needed:** Saudi gov laws, regulations, procedures, announcements (REGA bulletins, ZATCA RETT amendments, NHC announcements, Foreign Ownership Law executive bylaws, ministry circulars, royal decrees, municipal directives)
- **Approach:** Beyond curating a regulatory timeline (#43), systematically ingest the FULL TEXT of regulatory artifacts, extract the structured elements (effective dates, scope geographies, scope asset-types, exemption rules, compliance thresholds, reporting requirements), and use those elements as direct inputs to: (a) discovery scanner seed priorities — when a new asset-type is named in a regulation, surface it as a gap; (b) entity-model evolution — new actor types or transaction types named in regulations may justify new entities or fields; (c) corroboration authority weights — regulatory definitions of "valid" data sources inform v2 source-priority calibration.
- **Mechanism:** The regulatory text feed becomes a continuous-improvement loop, not a static timeline. policy_event entities carry the parsed structured elements as columns; an "open questions" / "open relationships" tracker derived from regulatory language drives future data-asset planning.
- **Feasibility:** Medium — text ingestion + structured extraction is v3+ work (after canonical layer + identity + corroboration foundations). Manual triage of new regulations is feasible day-one.
- **Uniqueness:** Extremely high — no public RE dataset treats regulations as a continuous strategy input.
- **Commercial potential:** Very high — directly compounds Tawafuq compliance value AND positions the data asset as policy-aware (banks, REITs, investors all need this).
- **Captured from:** Apple Notes "REGA/Talgeeh:" item 1, 2026-05-26.

---

## Analysis Ideas — Macro & Structural

### 35. E-service adoption rate by category
- **Data needed:** نوع الخدمة field across all operation files
- **Challenge:** Straightforward. Shows digitization progress.
- **Feasibility:** High
- **Uniqueness:** Low — MOJ publishes this
- **Commercial potential:** Low

### 36. Public vs private sector transaction split
- **Data needed:** نوع القطاع field
- **Feasibility:** High
- **Uniqueness:** Low
- **Commercial potential:** Low

### 37. Total market size — SAR transacted per quarter
- **Data needed:** MOJ sales (price column)
- **Feasibility:** High
- **Uniqueness:** Medium — REGA publishes some aggregates
- **Commercial potential:** Medium

### 38. Concentration risk — top 5 cities' share of total value
- **Data needed:** MOJ sales
- **Feasibility:** High
- **Uniqueness:** Medium
- **Commercial potential:** Medium — portfolio diversification input

### 39. The 2023 dip — uniform or localized?
- **Data needed:** MOJ sales by city/quarter
- **Approach:** Was the 47% volume drop (281K → 140K) uniform across regions, or concentrated? Did prices also drop, or just volume? Schema changed in 2023 — was it a data issue?
- **Feasibility:** High
- **Uniqueness:** High — nobody has explained this publicly
- **Commercial potential:** Medium — market understanding

---

## Analysis Ideas — Asset Type Inference (Workaround)

### 40. Build land/built classifier from 2023 labeled data
- **Data needed:** 2023 Q1–Q3 sales with نوع العقار
- **Approach:** Use 131K labeled transactions to establish price-per-m² distributions for land vs villa vs apartment in each district. Then apply those ranges to classify 2020–2022 and 2024+ unlabeled data probabilistically.
- **Feasibility:** Medium — accuracy depends on how distinct the distributions are
- **Uniqueness:** Novel methodology
- **Commercial potential:** Foundational — enables many other analyses

### 41. REGA aggregate calibration for asset type inference
- **Data needed:** REGA sales indicators (have type breakdowns) + MOJ sales
- **Approach:** REGA tells us "in District X, 60% of transactions were land, 30% villas, 10% apartments." Use this distribution to validate our price-based classifier from #40.
- **Feasibility:** Medium
- **Uniqueness:** High
- **Commercial potential:** Foundational

---

## Monitoring & Data Collection Ideas

### 42. Data source monitoring cron
- Monitor Saudi Open Data portal APIs for new MOJ/REGA quarterly releases
- Monitor idlelands.momah.gov.sa for new zone/phase announcements
- Monitor Ejar collector for schema changes
- Alert on new files or format changes

### 43. Regulatory event timeline database
- Curate White Land Tax phase dates, cities, districts, fee rates
- Vacant property fine announcements and effective dates
- Any new real estate regulatory changes
- Small DB (dozens of rows) but high interpretive value

### 44. Historical REGA/MOJ data gap-filling
- MOJ operations data only covers 2024–2025. Sales covers 2020+.
- Future portal checks may reveal older operation datasets being published retroactively.
- The monitoring cron should also watch for new datasets, not just new files in existing datasets.

---

## Priority Framework

### Scoring dimensions
- **Feasibility:** Can the current data answer this? (High/Medium/Low)
- **Uniqueness:** Is anyone else answering this publicly? (High = nobody, Low = already published)
- **Commercial potential:** Would someone pay for this insight? (High = investors/banks, Medium = government/researchers, Low = academic)

### Quick wins (High feasibility + High uniqueness)
- #2 Transaction volume trends
- #4 Seasonal patterns
- #5 Emerging cities
- #6 Deal size trends
- #16 Division hotspots
- #18 Old deed registration map
- #30 Informal ownership clusters
- #37 Total market size
- #38 Concentration risk
- #39 The 2023 dip investigation

### High-value targets (Medium feasibility, very high potential)
- #1 Price per m² by district (needs asset type inference)
- #21 Gross rental yield by neighborhood
- #24/#25 Cash flow vs speculative market identification
- #31 White Land Tax impact analysis
- #33 Tax → division correlation
- #40 Land/built classifier from 2023 data (foundational)

### Future potential (Low feasibility now, very high value)
- #9 Enforcement sale discounts (needs price data in enforcement)
- #10 Seizure → price decline lag
- #26 Full distress chain tracking
- #28 POA as leading indicator
- #29 Division → sale supply pipeline

---

## Open Questions

1. Can we access MOJ or REGA authenticated APIs for richer property-level data?
2. Will MOJ bring back the نوع العقار column in future quarterly releases?
3. What additional external data sources could enrich the analysis? (municipality permits, building completion data, population registry)
4. Are there commercial real estate data providers in Saudi we should benchmark against?

---

**Next steps:**
1. Build the monitoring cron
2. Ingest raw data into 3-DB architecture
3. Start with quick wins to validate the pipeline
4. Build the land/built classifier (#40) as foundation for deeper analysis

---

# Appendix B — 2026-05-26 Research Sweep (Streams A–D)

**Context:** Post-v0 (Phases 1–5 shipped 2026-05-25/26), the canonical layer is populated but `analysis/notebooks/` is essentially empty. Operator (Mr Ed) requested a sweep across four research streams: (A) execute-ready analyses given current data, (B) cross-source joins, (C) new Saudi RE source discovery, (D) productization angles for public release + commercial product. This appendix is the sweep output; one or more streams will get a deep-dive follow-up.

**Consumers in scope per scoping qanda:** (a) `Saudi-Real-Estate-Data` public releases, (b) future commercial product. NOT scoped: Tawafuq, Mr Ed personal analysis.

---

## A. Execute-Ready Analysis Inventory

### Reality check from canonical-layer probe (2026-05-26)

Canonical entity row counts and key population rates:

| Entity | Rows | Notes |
|---|---|---|
| `deed` | 7,664,011 | **Only `deed_type` populated** — price/date/parcel/parties all NULL. Source: MOJ (100%). |
| `valuation_event` | 7,821,894 | MOJ 7.66M + REGA 151K + GASTAT 6.8K + Riyad REIT 50 + Al Rajhi REIT 1. |
| `parcel` | 15,167 | **Permits only.** MOJ does NOT contribute parcels in v0 (consistent with DEC-020). |
| `building` | 15,167 | Permits only. |
| `permit` | 16,093 | Permits only. |
| `neighborhood` | 17,201 | GASTAT 11.8K + Sakani 5.3K. |
| `lease` | 28,788 | **Sakani only.** REGA Ejar 104K contracts NOT yet in canonical. |
| `policy_event` | 1,281 | Discovery 1,167 (OSINT seeds, unverified) + REGA 113 + RCRC 1. |
| `reit_fund` | 90 | Riyad 50 + CMA 37 + AlRajhi 3. |
| `actor` | 37 | **CMA only.** MOJ deed parties NOT yet extracted. |

**Macro measures** (`re_measures.db`): REGA 151K rows / 151 metrics, DataSaudi 88K / 97 metrics (back to 1969!), SAMA 28.8K / 111 metrics, GASTAT 258 / 7 metrics. Note: SAMA + GASTAT + some REGA have `_unparsed_*` period strings — period parsing fix needed before time-series analysis.

**Implication:** v0 is a no-loss preservation foundation, not a query-ready layer. Source-native data lives in (a) `feeders/*.db` source-native tables, and (b) `*_source_record.raw_json` blobs. Analyses today route through one of:

- **Path 1 — Direct feeder query.** Fastest; requires UNION across ~200 MOJ tables per analysis.
- **Path 2 — JSON extract from `*_source_record.raw_json`.** Uniform interface, but JSON extraction per row is slow at 7.6M rows.
- **Path 3 — v0.1 "promotion" pass.** A one-time job to ETL canonical columns (deed.price, deed.deed_date, deed.region_code, etc.) from source_record. ~1-day effort, unblocks every analysis below.

**Recommendation:** Land a v0.1 promotion pass for the workhorse columns (`deed.price`, `deed.deed_date`, `deed.region`, `deed.city`, `deed.district`, `deed.classification_ar`, `deed.area_sqm`) BEFORE writing analysis notebooks. Otherwise every analysis re-implements the same SQL UNION + JSON-extract scaffolding.

### Ready-to-ship analyses (ranked by data sufficiency × commercial/public value × effort)

Maps to existing ANALYSIS_IDEAS.md numbers. "Path" column refers to the three routes above; "v0.1" means it works trivially once the promotion pass lands.

| Rank | Maps to | Title | Path | Effort | Commercial | Public-release fit |
|---|---|---|---|---|---|---|
| A1 | #2 + #5 | National transaction volume + emerging cities (2020-2025 by city × quarter) | v0.1 (or P1) | 1 day | Medium | **HIGH** — flagship public artifact |
| A2 | #37 + #38 | Total market size + top-5 concentration | v0.1 | 0.5 day | Medium | HIGH |
| A3 | #6 | Median deal-size + lot-size trend (by region × quarter) | v0.1 | 1 day | Medium | HIGH |
| A4 | #39 | The 2023 dip — uniform or localized? | v0.1 | 1 day | Medium | **VERY HIGH** (no one has explained this publicly) |
| A5 | #4 | Seasonal patterns (Ramadan / Hajj timing adjustment) | v0.1 | 1.5 days | Medium | HIGH |
| A6 | #16 + #18 | Division (فرز) + old-deed-registration hotspots — supply pipeline + formalization map | P1 + v0.1 | 2 days | High | HIGH |
| A7 | #17 + #30 | Merge hotspots + register-without-deed clusters | P1 + v0.1 | 1.5 days | High | Medium |
| A8 | #20 | Physical-registration (عيني) adoption rate by region | P1 | 1 day | Low | Medium |
| A9 | #15 | RE Development Fund POA concentration | P1 | 0.5 day | Low | Low |
| A10 | #43 | Regulatory event timeline DB (White Land Tax + Vacant Property Fine + Foreign Ownership) | net-new | 2 days | High | **VERY HIGH** — high interpretive value |

**High-value but data-limited (deferred):**

- **#1 Price/m² by district** + **#40 Land/built classifier from 2023 labeled data** — foundational, unblocks 8+ downstream analyses. Effort: 1 week. Strongly recommend tackling A11 = #40 next, gated on v0.1 promotion.
- **#21 Gross rental yield by neighborhood** — needs lease canonical populated from REGA Ejar 104K (currently Sakani 28K only). Effort: 0.5 day to ingest REGA Ejar, then 2 days for the analysis.
- **#31 White Land Tax impact** — has its own research doc (`docs/WHITE_LAND_TAX_RESEARCH.md`). Combine with A10 timeline. Effort: 3 days.

**Future-data-gated (no analysis until N+ quarters):**

- #8, #10, #11, #13, #14, #28, #29 — all need ≥4 more quarters of MOJ operations data (2025-Q4 onward will close most). Time-gated, not effort-gated.

---

## B. Cross-Source Join Opportunities

Joins that work at district/time aggregate level — NO v1 identity required (the only ones executable in v0).

### B1. Builder/developer health composite

- **Sources joined:** MOJ division `فرز` (90K rows) × KAPSARC building permits × Sakani ROSHN unit completions × REGA REPI quarterly
- **Join key:** `(region_ar, year, quarter)`
- **Output:** "supply-pipeline health index" per region × quarter
- **Why unique:** Each source on its own gives a partial picture (deeds/permits/completions/price). Combining yields a leading indicator nobody publishes.
- **Effort:** 3 days (post-v0.1)

### B2. Mortgage stress index

- **Sources joined:** SAMA mortgage credit aggregates × MOJ seizure × MOJ mortgage release × MOJ enforcement-sale count
- **Join key:** `(region, quarter)` — Riyadh-only for MOJ seizure, national for SAMA
- **Output:** composite stress score per region per quarter
- **Why unique:** Maps directly to ANALYSIS_IDEAS #11 (overleveraged areas) using the canonical layer
- **Effort:** 2 days

### B3. White Land Tax × division correlation

- **Sources joined:** MOJ division (`فرز`) × policy_event (WLT phase rollouts) × REGA REPI
- **Join key:** `(district_code, quarter)`, dummy for `wlt_phase_active`
- **Output:** division-rate elasticity to WLT exposure (ANALYSIS_IDEAS #33)
- **Why unique:** Quantifies the regulation's behavioral impact
- **Effort:** 3 days (gated on A10 timeline)

### B4. Rental-vs-sales pulse divergence

- **Sources joined:** REGA Ejar contracts × MOJ sales × REGA REPI rental + sales indices
- **Join key:** `(district, month/quarter)`
- **Output:** for each district, is the rental market diverging from the sales market? (e.g., sales freezing while rents climbing → undersupply; opposite → buyer's market)
- **Why unique:** Standard yield analysis (ANALYSIS_IDEAS #21) framed as a divergence signal
- **Effort:** 3 days (gated on lease canonical from REGA Ejar)

### B5. REIT NAV-vs-market gap

- **Sources joined:** Riyad/Al Rajhi REIT NAVs × CMA REIT registry × MOJ deed prices in the REITs' geographic portfolios
- **Join key:** REIT factsheet asset list → city/district aggregate from MOJ
- **Output:** is the public REIT trading above/below implied market valuation?
- **Why unique:** Public REIT analysts can't easily get to MOJ aggregate prices for the relevant districts; we can
- **Effort:** 4 days (manual factsheet → asset-geography mapping in v0; automatable later)

### B6. Macro-deed-price correlation pack (already exists)

- Existing `monitor/datasaudi_repi_saibor_correlation.py` proves the pattern. Extend to:
  - REPI × oil price × SAR liquidity (Riyadh / national)
  - GASTAT inflation × MOJ avg deed price
  - SAMA credit aggregates × MOJ transaction velocity
- **Effort:** 1 day each, mostly scaffolding follows the existing script

### Joins gated on v1 identity (deferred)

- **B7. Property lifecycle (deed → mortgage → seizure → enforcement)** — proven impossible from MOJ public data per DEC-020. **Wathq /api/13 deeds API** (in discovery seeds) MAY provide parcel-level deed records — verify in deep-dive.
- **B8. Buyer/seller actor network** — needs MOJ deed parties extracted to `actor` (currently 0 from MOJ).

---

## C. New Saudi RE Source Sweep

Cross-referenced against `discovery/seeds.yaml` (32 sources currently seeded, 22 of which are Tier A).

### C.1 — Seeded but not yet promoted to a collector (HIGH-VALUE BACKLOG)

These are already on the discovery scanner's radar but no feeder exists yet:

| Domain | Source | Why valuable for Asl | Priority |
|---|---|---|---|
| `developer.wathq.sa` | Wathq Unified-Access API — `/api/13` is the RE deeds API | **Highest** — could provide parcel-level deeds (the v1 identity unblocker) | **P0** |
| `developers.najiz.sa` | Najiz (MOJ developer portal) | RE deeds + judicial actions, API-tier vs CSV-tier | **P0** |
| `zatca.gov.sa` | ZATCA — host of RETT (RE Transaction Tax) | Transaction tax filings are independent corroborator for MOJ sale prices | **P0** (also Tawafuq anchor) |
| `balady.gov.sa` | Bena building-permits platform (national) | Complements the 14-amana CSVs with a unified national feed; supply pipeline | **P1** |
| `api.address.gov.sa` | National Address API | Geocoding (address → coordinates → parcel) — enrichment for canonical | **P1** |
| `geosa.gov.sa` | GEOSA — parcel boundaries + GIS | Spatial layer; parcel polygons | **P1** |
| `pif.gov.sa` | PIF (Public Investment Fund) | Giga-project supply pipeline (NEOM, Red Sea, AlUla, Diriyah, Qiddiya); WebKit stealth required | **P2** |
| `mof.gov.sa` | Ministry of Finance open data | Housing-program budget allocations, NHC subsidies | **P2** |
| `misa.gov.sa` | Ministry of Investment | Foreign-investor licenses (intersects Foreign Ownership Law) | **P2** |
| `se.com.sa` | Saudi Electricity Company | Connection requests as housing-readiness proxy | **P3** (proxy signal) |
| `nwc.com.sa` | National Water Company | Same | **P3** |
| `monshaat.gov.sa` | SME General Authority | Commercial-RE demand proxy (SME formation → office demand) | **P3** |

### C.2 — Not yet in seeds.yaml (NEW CANDIDATES TO ADD)

| Domain | Source | Why valuable | Difficulty | Priority |
|---|---|---|---|---|
| `taqeem.gov.sa` | TAQEEM — Saudi Authority for Accredited Valuers | Independent valuation authority; ground truth for #40 land/built classifier | Medium (auth-gated likely) | **P1** |
| `srco.sa` | Saudi Real Estate Refinance Company | Mortgage refinancing volumes — leading indicator for housing demand | Medium | **P1** |
| `momrah.gov.sa` | Ministry of Municipal & Rural Affairs & Housing | Municipal master plans, land-use, white-land registry (the WLT primary source) | Medium | **P1** (anchors A10) |
| `aqar.fm` / `bayut.sa` / `propertyfinder.sa` / `wasalt.com` | Listing platforms | Real-time asking prices + supply; rental yield denominator | High (anti-bot, ToS, possibly stealth) | **P2** — high signal, high friction |
| `tadawul.com.sa` | Saudi Stock Exchange | REIT + listed RE-co quarterly filings; CMA already provides registry | Medium | **P2** |
| Listed RE companies (~10 cos) | Dar Al Arkan, Jabal Omar, Knowledge Economic City, Emaar Economic City, Makkah Construction, Taiba Holding, etc | Quarterly project-by-project disclosures (units delivered, presales) | Medium | **P2** — high signal per filing, low frequency |
| `neom.com`, `theredsea.sa`, `diriyah.sa`, `experiencealula.com`, `qiddiya.com` | Giga-project portals | Construction pipeline, employment, residential offerings | Medium | **P3** — narrative-rich, data-thin |
| `idlelands.momah.gov.sa` | Idle Lands (وزارة بلدية — WLT zones) | Authoritative WLT zone map | Medium (already in monitor probes per ANALYSIS_IDEAS #42) | **P0** for A10 timeline |
| `foreign-ownership-portal.gov.sa` (TBD) | Foreign Ownership of RE | Net foreign RE capital inflows | Unknown | **P2** |
| `eya.gov.sa` or Premium Residency | Premium Residency Center | Foreign-investor RE qualifications | High (auth) | **P3** |
| Real estate broker registries (REGA-licensed brokers) | Broker activity as channel signal | Medium | **P2** |

### C.3 — Not new sources but worth pursuing as analytical benchmarks

These are commercial competitors / quality references rather than ingestion targets:

- **JLL Saudi Arabia quarterly reports** (free PDF) — benchmark for whose office/retail rents we should publish
- **CBRE Middle East market reports** — same
- **Knight Frank KSA Wealth Report + RE notes** — same
- **Colliers KSA market intelligence** — same
- **Al Rajhi Capital / SNB Capital / Riyad Capital research desks** — quarterly RE notes referenced by industry
- **Argaam (already seeded)** — commercial RE news; useful for policy_event corroboration

---

## D. Productization Angles

### D.1 — Public release (`Saudi-Real-Estate-Data` repo)

**Goal:** stake a credible position as the highest-quality public Saudi RE data + analysis. Drives credibility for the future commercial product.

**Most compelling first artifacts (rank order):**

1. **A4 — "The 2023 Dip" investigation** (single notebook + writeup). The 47% volume drop from 281K→140K transactions in 2023 has no public explanation. We have the data to explain it. High narrative draw → likely picks up press / Argaam coverage.
2. **A1 — National transaction volume + emerging cities** dashboard (interactive HTML, AR+EN). Recurring quarterly artifact; sets a publication cadence.
3. **A4 + A10 + B3 — White Land Tax impact study** (long-form analysis). Defines the methodology for measuring policy impact; positions Asl as the policy-analytics layer.
4. **B1 — Builder/developer health composite** (per-region scorecard, refreshed quarterly). The "vendor diligence" use case for buyers commissioning new builds.

**Publishing cadence target:** quarterly major artifacts + monthly transaction-volume update. Stop short of daily — keeps news cycle predictable.

### D.2 — Commercial product (future)

**Buyer personas + price benchmarks (rough, from competitive scan):**

| Buyer | Annual budget range | What they need | Closest comp |
|---|---|---|---|
| Individual investors | 200-2,000 SAR/yr | Yield + appreciation maps | None public; consumer apps don't analyze |
| Institutional investors / family offices | 60K-500K SAR/yr | Custom market intel | JLL/CBRE retainer |
| Developers (medium) | 50K-300K SAR/yr | Supply pipeline + demand | Colliers / JLL |
| Banks / mortgage providers | 300K-3M SAR/yr | Risk + credit + zonal exposure | Internal teams + consultants |
| REIT managers | 100K-1M SAR/yr | Comparable valuations + macro | Al Rajhi Capital / SNB Capital research |
| Consultancies (downstream resale) | 20K-200K SAR/yr | Wholesale data | None public |

**Gap:** nobody publishes **district-level cross-source RE analytics in AR+EN with refresh-on-source-change**. JLL/CBRE/Knight Frank publish quarterly aggregate reports as PDF. Argaam publishes news. Bayut/Aqar publish listings. **Asl could be the analyst layer above the public data sources** — the missing tier.

**Delivery shape options (pick or combine):**

1. **Public reports (free)** — drives credibility; recurring artifacts (D.1 above).
2. **API subscription** — district-level series, freshness-tracked, AR+EN labels. Power-user pricing 500-5,000 SAR/mo.
3. **Dashboard subscription** — operator-facing, no-SQL UI. Mid-market pricing 200-1,000 SAR/mo.
4. **Custom reports** — bespoke pulls for institutions. 20K-100K SAR per engagement.
5. **Embedded data layer in Tawafuq** — out of scope per qanda but worth flagging: if Tawafuq is the compliance UI for licensed RE pros, surfacing market data alongside compliance status is a natural cross-sell.

**Recommended D direction:** D.1 public reports + D.2 API subscription, in that order. Public reports prove the analyst muscle and seed inbound demand; API monetizes power users without requiring sales motion.

---

## Highest-Leverage Finding (Stream X candidate)

The single biggest unlock surfaced in this sweep:

**Wathq `/api/13` (real-estate deeds API) — if it serves parcel-level deeds, it dissolves the DEC-020 lock.**

DEC-020 stated that within-MOJ cross-category identity resolution is impossible from current open data. That blocks A11 (#40 land/built classifier), B7 (property lifecycle), and ~6 ANALYSIS_IDEAS entries marked "future potential." If Wathq /api/13 is a structured API returning deeds with stable parcel identifiers, those analyses move from "blocked, wait for years of more data" to "1-2 weeks of work."

**Worth verifying in deep-dive:**
- What `/api/13` actually returns (sample response shape)
- Auth model (free / paid / OAuth)
- Rate limits + ToS
- Coverage (national? Riyadh-only?)
- Whether parcel IDs cross to MOJ public CSVs (probably no — but maybe to REGA / Sakani parcel IDs?)

**Alternative deep-dive candidates if Wathq turns out to be unusable:**

- **TAQEEM data unlock** — independent valuation as the ground truth for #40 classifier
- **REGA Ejar canonical population** — 104K contracts ready to ingest, immediately unblocks #21 yield + B4 rental-divergence
- **v0.1 promotion pass** — the cross-cutting unblock for A1-A10

---

*Sweep completed 2026-05-26 by Mr Ed + Claude. Next: pick a deep-dive subject (Wathq /api/13 most-likely candidate) and validate before scoping a phase.*


---

## Report-differentiation ideas vs REGA bulletin (filed 2026-07-11 from tasks.md To-Promote; harvest 2026-04-16)

Reports we can publish that REGA does NOT cover (we have district-level microdata; REGA = national-only, means-only, retrospective). VERIFY-FIRST — some may already be built.
- **Geographic depth:** Median/P10/P90 distribution per city (means hide skew); intra-city transaction-share migration YoY.
- **Leading indicators:** Sakani allocations × MOJ sales (program vs open-market flow); Ejar new/ending contracts → vacancy-trend proxy per city.
- **Cross-dataset joins:** Real (CPI-adjusted) vs nominal price trend (deflate by GASTAT CPI housing); mortgage affordability index (SAMA rates + MOJ price + GASTAT income, DSR-style).
- **Time/behavioral:** Hijri effects (Ramadan/Hajj dips, Hijri date per MOJ txn); day-of-week/month-end clustering; multi-parcel bundle deals `عدد العقارات>1` (institutional vs retail); 6-year trend lines 2020-Q1→ (vs REGA's 3 points).
- **Risk/anomaly:** Top-N outlier transactions/month (>100M SR) + geographic clustering.
- **Enabler (LOW):** OCR ingestion for rasterized REGA PDFs (Indicators Report v2) — gate: only if rasterized 3+ consecutive months AND adds signal beyond our joins.
Origin: tasks.md To-Promote (Apr-16 harvest); triggered by REGA March-2026 bulletin review.
