# msc-data-curation-Macroeconomic-time-series-data-GROUP-1
A curated longitudinal dataset of eight macroeconomic indicators for 48 World Bank-classified sub-Saharan African countries over 20 years (2006 - 2025), sourced from the World Bank's World Development Indicators (WDI). The dataset supports cross-country and time-series analysis of growth, inflation, employment, trade, investment, and fiscal policy.

## Group Members
- NII OKOE LUKE SOWAH (SE/DMD/25/0001) - Data retrieval, processing script
- ALFRED ASUMAH TETTEH (SE/DMD/25/0002) - Data curation, metadata, codebook
- DANIEL ANNAN (SE/DMD/25/0003) - Quality checks, documentation
- TAHIDU HUDU (SE/DMD/25/0004) - Dublin Core and DDI metadata

## Research/Reuse Purpose
This dataset supports comparative macroeconomic analysis of sub-Saharan African 
economies, including growth, inflation, unemployment, and investment dynamics.
It is suitable for panel data analysis, cross-country comparisons, and 
development policy research.

## Original Data Provider
World Bank — World Development Indicators (WDI)
- Source dataset: World Development Indicators
- Direct source: https://databank.worldbank.org/source/world-development-indicators
- API documentation: https://datahelpdesk.worldbank.org/knowledgebase/articles/889392

## Retrieval Date and Query
- Date retrieved: 15 September 2026
- Original filename: `P_Data_Extract_From_World_Development_Indicators.xlsx`
- Query: World Bank DataBank query for all SSF countries, indicators 
  NY.GDP.MKTP.KD.ZG, NY.GDP.PCAP.KD, FP.CPI.TOTL.ZG, SL.UEM.TOTL.ZS, 
  NE.CON.GOVT.ZS, NE.TRD.GNFS.ZS, BX.KLT.DINV.WD.GD.ZS, NE.GDI.TOTL.ZS, 
  years, 2006–2024.

  ## Geographic Scope
Region: Sub-Saharan Africa (World Bank SSF classification)
Countries included: 48 
Country-selection rule: All countries with World Bank region code SSF; 
  regional aggregates excluded.
### Countries included (48):
  Angola, Benin, Botswana, Burkina Faso, Burundi, Cabo Verde, Cameroon,
  Central African Republic, Chad, Comoros, Congo Dem. Rep., Congo Rep.,
  Cote d'Ivoire, Equatorial Guinea, Eritrea, Eswatini, Ethiopia, Gabon,
  Gambia, Ghana, Guinea, Guinea-Bissau, Kenya, Lesotho, Liberia,
  Madagascar, Malawi, Mali, Mauritania, Mauritius, Mozambique, Namibia,
  Niger, Nigeria, Rwanda, Sao Tome and Principe, Senegal, Seychelles,
  Sierra Leone, Somalia Fed. Rep., South Africa, South Sudan, Sudan,
  Tanzania, Togo, Uganda, Zambia, Zimbabwe

## Temporal Scope
- Years: 2006 - 2024 (20 years)
- Unit of observation: Country-year
- Frequency: Annual
- Indicators: 8 macroeconomic indicators (see codebook)

# Indicators Included
| Indicator Code  | Indicator Name | Unit |
|-----------------|----------------|------|
| NY.GDP.MKTP.KD.ZG | GDP growth (annual %) | % |
| NY.GDP.PCAP.KD | GDP per capita (constant 2015 US$) | constant 2015 US$ |
| FP.CPI.TOTL.ZG | Inflation, consumer prices (annual %) | % |
| SL.UEM.TOTL.ZS | Unemployment, total (% of labour force, modelled ILO) | % |
| NE.CON.GOVT.ZS | General government final consumption expenditure (% of GDP) | % |
| NE.TRD.GNFS.ZS | Trade (% of GDP) | % |
| BX.KLT.DINV.WD.GD.ZS | Foreign direct investment, net inflows (% of GDP) | % |
| NE.GDI.TOTL.ZS | Gross capital formation (% of GDP) | % |

## Repository Structure
- `data/raw/` - Original, unmodified WDI download
- `data/processed/` - Cleaned, reshaped curated dataset (CSV)
- `code/` - Python script for data preparation
- `documentation/` - Codebook, data quality notes, processing log
- `metadata/` - Dublin Core (JSON-LD) and DDI-Codebook (XML) metadata

## Data Retrieval and Processing
1. Downloaded WDI bulk .xlsx from World Bank DataBank
2. Filtered to SSF countries and selected indicators
3. Reshaped from wide to long format (country-year-indicator-value)
4. Distinguished missing values (blank/NA) from zero values
5. Retained original indicator codes, country codes, years, values, units
6. Documented all cleaning decisions in `documentation/processing_log.md`

## How to Reproduce
1. Download the WDI extract from the World Bank DataBank.
2. Place the file in `data/raw/` without modification.
3. Run `python code/data_preparation.py`.
4. The script produces `data/processed/curated_dataset.csv`.
5. Validate outputs against `documentation/codebook.csv`.

## Cleaning, Reshaping, Recoding Decisions
Renamed columns to machine-readable names.
Reshaped wide → long (country–year–indicator).
Distinguished missing (`..`) from zero (0).
Retained original indicator codes.
Documented monetary variables as constant-price or current-price.

## Missing-Data Conventions
- Missing values are represented as empty cells in the CSV and as `NA` in code.
- Missing ≠ zero. Zero values are retained where reported.
- Countries with no data for a given indicator-year are documented, not imputed.

## Known Limitations
- WDI data are compiled from national sources; comparability across countries 
  may be affected by differences in definitions and reporting practices
- Some indicators have gaps for conflict-affected countries.
- Unemployment is modeled (ILO estimate), not observed.
- 2025 values may be provisional.

## Licensing
- Source data: World Bank WDI is licensed under CC-BY 4.0 [citation:8]
- Curated dataset: This curated version is released under CC-BY 4.0.
- Code: MIT License
- Note: The World Bank's CC-BY 4.0 license applies to the source data. 
  Our repository license applies to our original documentation and code only.

## Suggested Citation
Tetteh, A.A., et al. (2026). Curated Dataset: Macroeconomic Indicators for Sub-Saharan
Africa, 2006–2025 (WDI Extract)* (Version 1.0) [curated_dataset]. 
https://github.com/ALFRED116/msc-data-curation-Macroeconomic-time-series-data-GROUP-1

## Software Versions
- Python 2.2.3
- pandas 2.2.3
- numpy 2.1.3

## Metadata Standards : 
### Version Declaration
Dublin Core: DCMI Metadata Terms (JSON-LD) - `metadata/dublin-core.jsonld`
DDI-Codebook version: 2.5 - `metadata/ddi-codebook.xml`
DDI-Codebook version used: 2.5
Namespace: ddi:codebook:2_5
Schema location: https://ddialliance.org/Specification/DDI-Codebook/2.5/XMLSchema/codebook.xsd

