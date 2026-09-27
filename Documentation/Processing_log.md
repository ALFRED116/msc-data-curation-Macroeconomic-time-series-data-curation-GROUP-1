# Processing Log

**Dataset:** Macroeconomic Indicators for Sub-Saharan Africa, 2006–2025 (WDI Extract)
**Group:** Group 1 — Macroeconomic time-series data (SE/DMD/25/0001 | SE/DMD/25/0002 | SE/DMD/25/0003 |SE/DMD/25/0004)
**Version:** 1.0
**Date:** 26 September 2026

---

## 1. Data Provider and Source

| Item | Detail |
|------|--------|
| **Data provider** | World Bank |
| **Source dataset title** | World Development Indicators (WDI) |
| **Source landing page** | https://databank.worldbank.org/source/world-development-indicators |
| **API (optional)** | https://api.worldbank.org/v2/indicator |
| **Licence (source)** | CC BY-4.0 — https://datacatalog.worldbank.org/int/public-licenses#cc-by |

> The World Bank is the original producer and owner of the WDI data.
> This repository does **not** claim ownership of the source data.

---

## 2. Retrieval

| Item | Detail |
|------|--------|
| **Retrieva date** | 15 SEPTEMBER 2026 |
| **Download format** | Microsoft Excel (.xlsx) |
| **Original filename** | `P_Data_Extract_From_World_Development_Indicators.xlsx` |
| **Raw file location** | `data/raw/P_Data_Extract_From_World_Development_Indicators.xlsx` (unmodified) |
| **Download method** | Manual extract via the WDI DataBank web portal |

---

## 3. Portal Filters and Scope

| Filter | Value |
|--------|-------|
| **Region** | Sub-Saharan Africa (World Bank classification) |
| **Countries** | 48 SSA countries (list in README.md) |
| **Years** | 2006–2025 (20 years) |
| **Indicators** | 8 macroeconomic indicators (see codebook.csv) |
| **Disaggregations** | None (national-level only; no sex or age breakdown) |
| **Frequency** | Annual |
| **Aggregates** | Excluded — regional aggregates not treated as countries |

---

## 4. Software and Package Versions

| Tool | Version |
|------|---------|
| Python | 2.2.3 |
| pandas | 2.2.3 |
| openpyxl | 2.1.2 |
| Jupyter Notebook | 7.3.2 |

---

## 5. Processing Steps

1. Loaded the raw WDI Excel extract (sheet `Data`), skipping footer rows.
2. Renamed columns to machine-readable names: `country_name`, `country_code`, `year`, `indicator_code`.
3. Extracted WDI indicator codes from bracketed column headers.
4. Replaced the WDI missing marker `..` with `NA`.
5. Reshaped wide → long (country–year–indicator).
6. Attached indicator metadata: `indicator_name`, `unit`, `price_basis`, `observation_status`.
7. Distinguished missing from zero via `value_status` (`observed`, `zero`, `missing`).
8. Added constant fields: `periodicity`, `source_dataset`, `retrieval_date`.
9. Ran quality checks (duplicate keys, impossible values, coverage gaps).
10. Exported the curated dataset to `data/processed/curated_dataset.csv` (UTF-8, CSV).

Full code: `code/data_preparation.ipynb`

---

## 6. Rows Removed and Reasons

| Action | Count | Reason |
|--------|-------|--------|
| Footer rows removed | 5 | WDI footer lines ("Data from database…", "Last Updated…") |
| Blank rows removed | 3 | Trailing empty rows in the Excel sheet |
| Country rows dropped | 0 | No countries were dropped |
| Duplicate rows dropped | 0 | No duplicate keys found |
| **Rows retained** | **≈ 8,544** | Country × year × indicator |

No valid data rows were removed.

---

## 7. Variables Renamed, Recoded, or Derived

| Original (WDI) | Curated Name | Action |
|----------------|--------------|--------|
| Country Name | `country_name` | Renamed |
| Country Code | `country_code` | Renamed |
| Time | `year` | Renamed + coerced to integer |
| Time Code | — | Dropped (redundant) |
| `GDP growth (annual %) [NY.GDP.MKTP.KD.ZG]` | `NY.GDP.MKTP.KD.ZG` | Code extracted |
| (all other indicator columns) | (WDI codes) | Code extracted |
| — | `indicator_name` | Derived from WDI metadata |
| — | `unit` | Derived from WDI metadata |
| — | `price_basis` | Derived from WDI metadata |
| — | `value_status` | Derived (observed / zero / missing) |
| — | `observation_status` | Derived (reported / modelled) |
| — | `periodicity` | Constant: Annual |
| — | `source_dataset` | Constant: World Development Indicators |
| — | `retrieval_date` | Constant: 2026-09-15 |

---

## 8. Unit Conversions and Rounding

| Decision | Detail |
|----------|--------|
| **Unit conversions** | None. Values retained in the provider's original units. |
| **Rounding** | None. Values retain full provider precision. |
| **Monetary variables** | Documented with `price_basis` (current price, constant price, modelled). |

---

## 9. Missing Values, Suppression Flags, and Uncertainty

| Aspect | Treatment |
|--------|-----------|
| **Provider missing marker** | `..` replaced with `NA` |
| **True zeros** | Retained as `0` |
| **Distinction** | Encoded in `value_status` (`observed` / `zero` / `missing`) |
| **Suppression flags** | None present in the WDI extract |
| **Uncertainty bounds** | Not supplied by WDI for these indicators; not imputed |
| **Imputation** | None performed |

---

## 10. Licensing — Source vs. Curated (Separate)

| Item | Licence | Notes |
|------|---------|-------|
| **Source data (World Bank WDI)** | CC BY-4.0 | Owned by the World Bank. |
| **Curated dataset** | CC BY-4.0 | Derived from WDI; attribution required. |
| **Scripts and documentation** | CC BY-4.0 | Original work by Group 1. |

> The repository licence does **not** replace the World Bank's terms of use.
> Users must comply with **both**.

---

## 11. Reproduction Instructions

1. Download the WDI extract from the World Bank DataBank using the filters above.
2. Save it to `data/raw/P_Data_Extract_From_World_Development_Indicators.xlsx`.
3. Run `code/data_preparation.ipynb` from top to bottom.
4. The script produces `data/processed/curated_dataset.csv`.
5. Validate against `documentation/codebook.csv`.

---

**End of processing log.**
