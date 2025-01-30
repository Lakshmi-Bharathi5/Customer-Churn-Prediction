# Customer Churn Analysis
## Overview
This project is a comprehensive **Customer Churn Analysis** using **Power BI**. The analysis focuses on understanding customer churn rates, identifying key factors contributing to churn, and providing actionable insights to improve customer retention. The dataset includes customer demographics, account information, and service subscriptions from a telecom company.

## Key Concepts
### What is Churn?
Churn refers to the rate at which customers stop doing business with a company or service, typically expressed as a percentage of the customer base.

### What is Churn Rate?
Churn Rate, also known as attrition rate, is the rate at which customers stop doing business with a company over a given period. It is calculated as:
Churn Rate = (Churned Customers / Total Number of Customers) x 100%

### What is Customer Churn?
Customer Churn refers to the natural business cycle of losing and acquiring customers. It can occur due to factors such as dissatisfaction with the product or service, competitive offerings, or changes in customer preferences.

## About the Dataset
The dataset is a Microsoft Excel file containing **7,043 rows** and **23 columns** of customer information, including:
- **Customer Demographics**: Gender, age (Senior Citizen or Young Citizen), partner status, dependents.
- **Account Information**: Tenure, contract type, payment method, monthly charges.
- **Service Subscriptions**: Phone service, internet service, additional services like online security, streaming, etc.

## Data Preparation
The data transformation and cleaning were performed using **Power Query** in Power BI. Key steps included:
- Changing data types for columns like `customerID`, `gender`, and `SeniorCitizen`.
- Renaming columns for better readability (e.g., `customerID` to `CustomerID`, `gender` to `Gender`, `tenure` to `Tenure`).
- Replacing values in the `PaymentMethod` column for consistency (e.g., "Mailed check" to "Mailed Check").
- Adding conditional columns:
  - `CitizenshipStatus`: Classifies customers as "Young Citizen" or "Senior Citizen".
  - `ChurnStatus`: Classifies customers as "Churned" or "Retained".

## Measures Used in Visualizations
The following measures were created in Power BI for analysis:
- **Total Customers**: `COUNT(ChurnDataset[CustomerID])`
- **Churned Customers**: `CALCULATE(COUNTA('ChurnDataset'[CustomerID]), 'ChurnDataset'[Churn] IN { "Yes" })`
- **Retained Customers**: `CALCULATE(COUNTA('ChurnDataset'[CustomerID]), 'ChurnDataset'[Churn] IN { "No" })`
- **Churn Rate %**: `ChurnDataset[Churned Customers] / COUNT(ChurnDataset[CustomerID])`
- **Monthly Revenue Loss**: `CALCULATE(SUM(ChurnDataset[MonthlyCharges]), ChurnDataset[Churn] = "Yes")`
- **Revenue Loss %**: `DIVIDE([Monthly Revenue Loss], SUM('ChurnDataset'[MonthlyCharges]), 0)`

## Key Insights
- **Total Customers**: 7,043
- **Churned Customers**: 1,869 (26.54% churn rate)
- **Monthly Revenue Loss**: $139.13K (30.50% of total revenue)
- **Retained Customers**: 5,174 (73.46% retention rate)

## Visualizations
The Power BI report includes interactive dashboards and visualizations for:
- **Customer Demographics**: Gender, age, partner status, dependents.
- **Account Details**: Tenure, contract types, payment methods, monthly charges.
- **Service Subscriptions**: Phone service, internet service, additional services.
- **Churn Analysis**: Churn rate, revenue loss, and retention metrics.
