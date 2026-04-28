
# Customer Churn Analysis – Power BI Dashboard

This project delivers a comprehensive telecom customer churn analysis using Power BI. It encompasses data cleaning, DAX-based data modeling and interactive dashboard design to help telecom providers identify which customer segments are churning, understand the reasons behind churn and prioritize retention strategies.

## Data Source

The dataset used is the [Telco Customer Churn dataset from Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn). It contains customer-level information such as demographics, account details, service usage, and churn status.

**Key columns include:**
- `customerID`, `gender`, `SeniorCitizen`, `Partner`, `Dependents`
- `tenure`, `PhoneService`, `MultipleLines`, `InternetService`, `OnlineSecurity`, `OnlineBackup`, `DeviceProtection`, `TechSupport`, `StreamingTV`, `StreamingMovies`
- `Contract`, `PaperlessBilling`, `PaymentMethod`, `MonthlyCharges`, `TotalCharges`, `Churn`

## Data Quality Observations & Cleaning

- Some monetary columns (e.g., `MonthlyCharges`, `TotalCharges`) contain currency symbols or missing values.
- Inconsistent text values (e.g., “month to month”, “Month-to-month”, “Month-To-Month”) were standardized.
- Rows with missing or null `TotalCharges` for new customers were handled by replacing nulls with 0 only when `MonthlyCharges` had a value.
- Service columns with values like “No internet service” or “No phone service” were normalized for analysis.
- Duplicate `customerID` rows were removed to avoid overstating churn and revenue.
- Data types for tenure, MonthlyCharges, and TotalCharges were corrected for accurate aggregations.
- Logical contradictions were fixed (e.g., if `PhoneService` = "No", then `MultipleLines` = "No").

## Data Modeling & DAX

The model centers on a cleaned Telco Churn fact table, featuring:

**Measures:**
- Total Customers, Churned Customers, Retained Customers, Churn Rate (%)
- Average Monthly Charges, with separate averages for churned and retained customers

**Calculated Columns:**
- Tenure Band (0–6, 6–12, 12+ months)
- Customer Type (New vs. Existing)
- Risk Type (High Risk vs. Normal), based on month-to-month contracts and low tenure

These calculations directly address questions like “Which segment should be prioritized for retention this month?”

## Dashboard Design

The Power BI dashboard features a single-page, KPI-focused layout:

- **Top:** Overall KPIs (Total Customers, Churn Rate %, Churned Customers)
- **Middle:** Churn drivers (by Contract, Tenure Band, Online Security/Backup, Customer Type)
- **Bottom:** Retention overview and churn distribution

Visuals are selected based on analytical needs (e.g., column charts for churn by tenure, bar charts for contract/revenue, donut charts for retention split), all presented in a consistent dark theme for readability.

## Key Insights

- The overall churn rate is approximately 26.5% (1,869 out of 7,043 customers).
- New customers (0–6 months) on Month-To-Month contracts have a churn rate exceeding 50%, contributing most to overall churn.
- Churned customers have higher average monthly charges (mid-70s) compared to retained customers (low-60s).
- Customers lacking Online Security or Online Backup are more likely to churn and represent a significant portion of lost revenue.

## Recommendations

- Implement targeted onboarding and retention offers for new, month-to-month customers (0–6 months).
- Review plans and pricing for high-charge, short-tenure, month-to-month customers.
- Bundle Online Security and Online Backup in acquisition offers and monitor churn rates by bundle adoption.

