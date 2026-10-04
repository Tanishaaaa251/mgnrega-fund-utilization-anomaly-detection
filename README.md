# MGNREGA Fund Utilization & Anomaly Detection Dashboard

## Project Overview

This project analyzes MGNREGA fund utilization across the 14 districts of Kerala for FY 2023–24 and FY 2024–25. Python is used for data extraction and preprocessing, SQL for analytical calculations and risk-flag generation, and Power BI for interactive visualization.

The dashboard helps users explore district-wise financial patterns and identify district-year observations that may need further examination. A flag is a screening indicator, not proof of irregularity or wrongdoing.

## Project Scope

- **Geography:** 14 districts of Kerala
- **Financial Years:** 2023–24 and 2024–25
- **Raw Inputs:** 28 government MIS report files (one per district-year)
- **Analytical Grain:** One row per district per financial year
- **Final Dataset:** 28 district-year observations

## Tools & Technologies

- **Python:** Data extraction, cleaning, standardization, and consolidation
- **SQL:** Financial metric calculations, analytical views, and risk flags
- **Power BI:** Interactive dashboard, KPI cards, and district-level exploration
- **Excel:** Additional spot-checking of selected calculations

## Data Pipeline

1. Extracted information from government MIS reports using Python.
2. Cleaned and standardized the data, including district names, text fields, and numeric financial values.
3. Consolidated district-year records into a structured dataset.
4. Used SQL to calculate financial indicators and generate five flagging outputs.
5. Connected the analytical data to Power BI for visualization and interactive exploration.
6. Cross-checked selected calculations against the underlying values as a validation step.

## Flagging Methodology

| Flag | What It Checks | Rule |
|---|---|---|
| **1. Wage–Material Ratio** | Material expenditure share | Flags records where the material share of the wage-plus-material base is above 40%. |
| **2. Administrative Expenditure** | Administrative expenditure share | Flags records where the administrative share is above 6%. |
| **3. Utilization Outlier** | District utilization compared with other districts in the same financial year | Calculates a year-wise Z-score and flags observations where the absolute Z-score is greater than 1. |
| **4. Payment Due Burden** | Relative payment-due burden among districts in the same year | Uses `NTILE(4)` within each financial year and flags the fourth quartile. |
| **5. Year-over-Year Balance Deterioration** | Change in district balance between the two financial years | Calculates balance as availability minus expenditure, compares the two years, and flags the three most negative changes. |

These rules identify observations for further review. They should not be interpreted as confirmed financial irregularities.

## Dashboard

The Power BI dashboard provides an interactive view of the analyzed data, including key indicators and district-level exploration. Users can filter and investigate district-year records, and use drill-through to move from the overview to district details.

## Key Definitions

- **Balance:** Total Availability − Total Expenditure
- **Utilization Percentage:** Total Expenditure ÷ Total Availability × 100
- **Total Flags:** The number of flag events raised across the observations

A district-year with multiple flags is counted once in the flagged district-years metric, but contributes multiple times to the total flags metric.

## Validation

Selected calculations were independently checked using the underlying values. Excel was used as an additional sanity check; it was not a separate analytical processing layer.

## Limitations

- The analysis covers only Kerala and two financial years.
- The dataset contains 28 district-year observations, so the results are best treated as an initial screening exercise.
- Peer-relative thresholds highlight unusual patterns within the available data and do not establish the cause of those patterns.
- Flagged observations require contextual review before any administrative conclusion is drawn.

## Future Improvements

- Extend the analysis to more financial years to study longer-term trends.
- Expand coverage to other states for regional comparisons.
- Further automate data extraction, preprocessing, and dashboard refresh.
- Add more validation checks and investigate flagged observations using additional context.

## Dashboard Screenshots

Dashboard screenshots are included in this repository to provide a visual overview of the project and its interactive analysis.
