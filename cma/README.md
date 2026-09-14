# CMA Open Data

Source: [cma.org.sa](https://cma.org.sa) — Capital Market Authority (Saudi Arabia)
open-data statistical bulletins. Built 2026-06-18 (per source zip timestamps).

Each CSV was extracted from the CMA's official CSV-format zip bundle for that
collection and individually gzip-compressed. Filenames (Arabic) are the
original per-table sheet names from the source bundle.

| Collection | Member CSVs | Total rows |
|---|---:|---:|
| bulletin-1-securities-offerings | 11 | 303 |
| bulletin-2-equities | 20 | 997 |
| bulletin-3-sukuk-bonds | 6 | 125 |
| bulletin-4-mutual-funds | 14 | 538 |
| bulletin-5-cmis | 14 | 502 |
| bulletin-6-corporate-governance | 4 | 59 |
| bulletin-7-fintech | 6 | 95 |
| appendix-2024 | 39 | 734 |
| institutions-under-supervision | 17 | 1226 |

The two pre-existing `cma/portal/*.csv` files are unchanged in this release.
