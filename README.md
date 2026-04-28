
# Customer Churn Analysis - Power BI Dashboard

End-to-end telecom churn analysis built in Power BI to identify high-risk customer segments, explain churn drivers, and prioritize retention actions that protect recurring revenue.

## Project Overview

This project covers the full analytics workflow:
- Data cleaning and quality fixes
- Data modeling and DAX measures
- KPI-first dashboard design
- Insight generation and business recommendations

## Repository Structure

- `Data/telco_churn_unclean.csv`: raw dataset used for transformation
- `Dashboard/Customer Churn Analysis.pbix`: Power BI report file
- `Report/Customer Churn Analysis Report.md`: detailed project report
- `README.md`: project summary and usage guide

## Business Problem

The telecom business was experiencing elevated churn and needed to answer:
- Which customers are most likely to churn?
- Which factors are driving churn?
- Which retention actions should be prioritized first?

## Data Source

Dataset: [Kaggle - Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)

Key fields include:
- Customer profile: `customerID`, `gender`, `SeniorCitizen`, `Partner`, `Dependents`
- Service usage: `PhoneService`, `MultipleLines`, `InternetService`, `OnlineSecurity`, `OnlineBackup`, `TechSupport`, `StreamingTV`, `StreamingMovies`
- Commercial terms: `Contract`, `PaymentMethod`, `PaperlessBilling`, `MonthlyCharges`, `TotalCharges`
- Outcome label: `Churn`

## Data Cleaning and Quality Fixes

Main preparation steps:
- Removed duplicate `customerID` records to avoid overstating customer counts and churn.
- Standardized inconsistent text values (for example, contract naming variations).
- Applied trim/clean transformations to reduce fragmented categories.
- Corrected data types for `tenure`, `MonthlyCharges`, and `TotalCharges`.
- Converted `TotalCharges` to decimal and handled nulls for very new customers.
- Resolved logical contradictions:
  - If `PhoneService = "No"`, then `MultipleLines = "No"`.
  - If `InternetService = "No"`, then internet-dependent services are marked `"No"`.

These fixes ensure trustworthy KPIs and segmentation.

## Data Modeling and DAX

The model uses a cleaned telco churn table as the core fact table.

Core measures:
- `Total Customers`
- `Churn Customers`
- `Retained Customers`
- `Churn Rate %`
- `Average Monthly Charges`
- `Avg Monthly Charges (Churned)`
- `Avg Monthly Charges (Retained)`

Calculated columns:
- `Tenure Band` (0-6, 6-12, 12+ months)
- `Customer Type` (New vs Existing)
- `Risk Type` (High Risk vs Normal), based on contract type and early tenure

## Dashboard Design

Single-page, KPI-first layout:
- Top: overall churn KPIs
- Middle: churn drivers by contract, tenure, and add-on services
- Bottom: churn-retention split and distribution views

Visuals were chosen by analytical intent (comparison, composition, and trend) and styled with a consistent dark theme for readability.

## Dashboard Preview

![Customer Churn Analysis Dashboard](assets/images/customerDash.png)

Power BI dashboard highlighting churn rate, segment risk, and retention drivers.

## Key Insights

- Overall churn rate is `26.54%` (`1,869` of `7,043` customers).
- New customers in the `0-6 month` tenure band on `Month-To-Month` contracts drive a disproportionate share of churn.
- Churned customers show higher average monthly charges than retained customers.
- Customers without `Online Security` and `Online Backup` churn at higher rates and contribute more to revenue loss.

## Recommended Actions

1. Launch targeted onboarding and save-offers for new month-to-month customers in their first 6 months.
2. Review plan fit and pricing for high-charge, short-tenure customers.
3. Bundle Online Security and Online Backup in acquisition campaigns and track churn lift by bundle adoption.

## How to Use This Project

1. Open `Dashboard/Customer Churn Analysis.pbix` in Power BI Desktop.
2. Refresh data if needed using `Data/telco_churn_unclean.csv`.
3. Explore churn patterns by tenure, contract type, and service adoption.

## Tools Used

- Power BI Desktop
- Power Query
- DAX
- Markdown (project reporting)

## Author

Denis Mwanzia
