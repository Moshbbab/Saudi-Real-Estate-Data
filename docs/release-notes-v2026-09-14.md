# Release Notes — v2026-09-14

**Type:** Data refresh + two new source collections
**Adds:** 75 MOJ files (Jan–Jul 2026), 16 REGA quarterlies (Q1 2026 rental), `kapsarc/ods/` (11 datasets), `cma/` (9 collections)
**Files added:** 236 · **modified:** 14 · **removed:** 1
**Rows added:** ~3.0 million (MOJ 2,984,030 · REGA 20,257 · KAPSARC 31,303 · CMA ~4,600 data rows)

## Summary

The transaction side moves forward two quarters: MOJ real-estate
operations now run through **Q2 2026** (2.9 M new operation records
across the 36-type taxonomy), MOJ sales through **Q1 2026**, and the
monthly power-of-attorney aggregates through **July 2026**. REGA's
rental indicators gain the complete **Q1 2026** set for all 13 regions.

Two sources join the release for the first time as collections:

- **KAPSARC Open Data Portal (`kapsarc/ods/`)** — the 11 datasets that
  underlie the existing `kapsarc/` index files, plus household and
  construction-cost series that were not published here before. All are
  Public Domain per the portal's metadata. Snapshot date: 2026-09-14.
- **CMA statistical bulletins (`cma/`)** — the Capital Market Authority's
  seven statistical bulletins, the 2024 statistical appendix and the
  register of supervised institutions. Relevant to real estate through
  the mutual-funds bulletin (REIT tier), the sukuk/bond series and the
  list of licensed real-estate fund managers.

## What's new

| Directory | Files | Rows | Period | Notes |
|---|---:|---:|---|---|
| `moj/real-estate/` | 64 | 2,907,145 | 2026 Q1–Q2 | large files gzip-compressed |
| `moj/monthly/` | 10 | 44,298 | 2026-03 … 2026-07 | POA issued / annulled |
| `moj/sales/` | 1 | 32,587 | 2026 Q1 | individual sale records |
| `rega/quarterlies/rental/` | 13 | 20,146 | 2026 Q1 | all 13 regions |
| `rega/quarterlies/sales/` | 3 | 111 | 2025 | EP Q4, Jazan Q1–Q2 |
| `kapsarc/ods/` | 11 (+README) | 31,303 | 1987–2026 | Public Domain |
| `cma/` | 131 (+README) | ~4,600 data rows | 2007–2026 | 9 collections |

### KAPSARC ODS datasets

| dataset_id | rows |
|---|---:|
| building-permits-issued-by-municipalities-by-regions-and-type-of-permit-1987-201… | 14,289 |
| household-environment-statistics | 8,861 |
| household-income-and-consumption-expenditure-survey | 1,592 |
| construction-cost-indices-by-sector-and-section | 1,472 |
| construction-cost-index-series-by-sections-and-groups-at-national-level | 1,391 |
| real-estate-indices-by-regions-2023-100 | 938 |
| real-estate-indices | 830 |
| real-estate-price-index-by-sector-2023-100 | 680 |
| construction-cost-indices-by-sector | 621 |
| real-estate-indices-by-regions | 499 |
| housing-units-electrical-energy-consumption-by-season-and-region | 130 |

The building-permits series duplicates the KAPSARC half of
`data/permits/csv/permits_historical.csv.gz` (May 2026 release); it is
kept here in its portal-native shape for reproducibility.

### CMA collections

| Collection | CSV sheets | Lines (incl. bilingual headers) |
|---|---:|---:|
| bulletin-1-securities-offerings | 11 | 664 |
| bulletin-2-equities | 20 | 2,603 |
| bulletin-3-sukuk-bonds | 6 | 295 |
| bulletin-4-mutual-funds | 14 | 1,112 |
| bulletin-5-cmis | 14 | 1,127 |
| bulletin-6-corporate-governance | 4 | 124 |
| bulletin-7-fintech | 6 | 197 |
| appendix-2024 | 39 | 1,201 |
| institutions-under-supervision | 17 | 1,947 |

Sheets keep CMA's bilingual (Arabic/English) multi-row headers as
published; treat the first two rows as header when loading.

## Corrections

- `gastat/REPI-2023-Q4.csv` removed — mislabeled file (SWCC water series,
  not the real-estate price index).

## How to fetch

```bash
git clone https://github.com/civillizard/Saudi-Real-Estate-Data.git
# or a single file, e.g.
curl -O https://raw.githubusercontent.com/civillizard/Saudi-Real-Estate-Data/main/kapsarc/ods/real-estate-indices-by-regions.csv.gz
```

## Validation

`scripts/validate_release.py` — 0 errors; registry artifacts match a
fresh rebuild. Every file in this release passed the migration leak-vet
(the same pattern catalog as the repository's leak-guard workflow).
