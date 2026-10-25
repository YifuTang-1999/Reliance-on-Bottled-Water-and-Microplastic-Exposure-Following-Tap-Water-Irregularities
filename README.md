# Reliance-on-Bottled-Water-and-Microplastic-Exposure-Following-Tap-Water-Irregularities# Drinking-Water Violations, Bottled-Water Reliance, and Microplastic Exposure

This repository contains the code for a research project on how households respond to drinking-water violations, how long those responses last, and what they imply for microplastic exposure and the burden of defensive spending.

> **Status:** work in progress. Results are preliminary and should not be cited.

## Overview

When a public water system issues a health-based violation notice, households buy more bottled water. This is well documented (Graff Zivin, Neidell & Schlenker 2011; Allaire et al. 2019). Bottled water, however, contains several times more microplastic particles than tap water (Singh et al. 2025). This project asks:

1. **Persistence.** After a violation is resolved, does bottled-water purchasing return to baseline, or does it stay elevated?
2. **Substitution.** Which households switch to bottled water (higher exposure) and which switch to filters (lower exposure)? Does this differ by income and race/ethnicity?
3. **Notice severity.** Do Tier 1 notices (issued within 24 hours) produce different responses than Tier 2/3 notices?
4. **Exposure and incidence.** What are the implied increases in microplastic exposure, and how regressive is the defensive spending?

## Empirical strategy

- **Design:** staggered event study around the public-notice date of health-based violations (MCL and treatment-technique violations), with a window of 12 months before to 24 months after. A second event at the return-to-compliance date measures post-resolution decay.
- **Specification:** household and year-month fixed effects; Callaway–Sant'Anna or Sun–Abraham estimators; standard errors clustered by water system.
- **Heterogeneity:** interactions with income group, race/ethnicity, and renter status; separate estimates for filters and replacement cartridges.
- **Placebos:** monitoring and reporting violations; soft drinks and juice.
- **Exposure:** purchase response × (bottled − tap concentration), using size-harmonized Global North parameters from Singh et al. (2025), with Monte Carlo intervals. The project reports exposure only and does not estimate health effects.

## Repository structure

```
.
├── code/
│   ├── 01_violations/       # download and clean SDWA violation data
│   ├── 02_geography/        # service-area boundaries → ZIP crosswalk
│   ├── 03_panel/            # build household × month panel (runs in licensed environment)
│   ├── 04_analysis/         # event studies, heterogeneity, placebos
│   └── 05_exposure/         # concentration parameters, Monte Carlo, incidence
├── data/
│   ├── raw/                 # NOT tracked; see Data section
│   ├── intermediate/        # NOT tracked
│   └── public/              # small public inputs that can be shared
├── output/
│   ├── figures/
│   └── tables/
├── docs/                    # proposal and notes
└── README.md
```

## Data

| Dataset | Use | Source | In repo? |
| --- | --- | --- | --- |
| NielsenIQ Consumer Panel | Household bottled-water, filter, and beverage purchases; demographics; ZIP | Kilts Center, University of Chicago Booth | **No** (licensed) |
| NielsenIQ Retail Scanner (optional) | Store-level robustness checks | Kilts Center | **No** (licensed) |
| SDWA violations | Violation type, contaminant, dates, notice tier | [EPA ECHO data downloads](https://echo.epa.gov/tools/data-downloads) | No (download script provided) |
| Water-system service-area boundaries, v3 (Mar 2026) | Link water systems to ZIP codes and census tracts | [EPA](https://www.epa.gov/ground-water-and-drinking-water/community-water-system-service-area-boundaries) | No (download script provided) |
| American Community Survey | Neighborhood income, race/ethnicity, housing | Census API | No |
| Area Deprivation Index | Neighborhood disadvantage | [Neighborhood Atlas](https://www.neighborhoodatlas.medicine.wisc.edu/); [NaNDA standardized ADI](https://www.openicpsr.org/openicpsr/project/210581/version/V1/view) | No |
| Microplastic concentrations | Exposure parameters | [SamikshaSingh2506/BottledWaterMP](https://github.com/SamikshaSingh2506/BottledWaterMP) | No (cite and download) |
| Residential water rates (optional) | Control variable | Duke water-affordability dashboard; UNC EFC state dashboards | Partial |

### NielsenIQ data use

NielsenIQ data are proprietary and are used under the Kilts Center license. **No NielsenIQ microdata, household-level extracts, or intermediate files derived from them are stored in this repository.** Scripts in `code/03_panel/` and later must be run inside the licensed computing environment. Only aggregated results permitted under the license are exported.

Any output based on these data must include the acknowledgment and disclaimer language required by the Kilts Center. Use the exact wording from the current Kilts terms of use.

## Replication

1. Clone the repository.
2. Download the public data with the scripts in `code/01_violations/` and `code/02_geography/`.
3. Inside the licensed environment, place the NielsenIQ files at the path set in the configuration file and run `code/03_panel/`.
4. Run `code/04_analysis/` and `code/05_exposure/` in order.

Software versions and package requirements will be listed here once the pipeline is finalized.

## Key references

- Allaire, M., T. Mackay, S. Zheng, and U. Lall (2019). Detecting community response to water quality violations using bottled water sales. *PNAS* 116(42).
- Graff Zivin, J., M. Neidell, and W. Schlenker (2011). Water quality violations and avoidance behavior: Evidence from bottled water consumption. *American Economic Review: Papers & Proceedings* 101(3).
- Singh, S., A. Gray, M. Nemati, K. Schwabe, and L. Wang (2025). Microplastic exposure disparities in California communities through bottled water consumption. *Microplastics and Nanoplastics* 5, 43.

## Contact

[Your name] · [email] · [institution]
