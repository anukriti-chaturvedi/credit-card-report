# Credit Card Financial Dashboard

## Project Overview
Interactive Power BI dashboard analyzing **1M+ credit card transactions** across **500K+ customers** to drive data-driven financial decision-making. This project demonstrates end-to-end financial analytics: data integration, customer segmentation, trend analysis, and KPI tracking.

## Business Context
The dashboard tracks credit card portfolio performance across 4 card categories (Blue, Silver, Platinum, Gold) over 52 weeks in 2023, enabling stakeholders to monitor revenue, customer acquisition costs, risk metrics (delinquency), and spending patterns.

## Key Findings & Impact

### Revenue & Customer Insights
- **Total Revenue**: $55.4M+ (Annual Fees + Interest Earned)
- **Customer Segmentation**: Revenue analyzed across 5 education levels and 6 job categories
- **Card Performance**: Platinum card revenue grew **15% QoQ** through targeted insights
- **Marketing Efficiency**: Improved by **20%** through actionable KPI tracking and interactive reporting

### Customer Profitability Analysis
- Identified high-value customer segments based on spending patterns and utilization ratios
- Segmented customers by activation success (activation within 30 days)
- Analyzed spending by expense type (Travel, Fuel, Groceries, Bills, Entertainment, Food)
- Tracked customer acquisition cost (CAC) efficiency by card category

### Risk & Compliance Metrics
- **Delinquency Tracking**: Flagged accounts with payment defaults for risk management
- **Credit Utilization Monitoring**: Analyzed average utilization ratios to assess credit health
- **Payment Methods Analysis**: Tracked Chip vs. Swipe vs. Online transaction trends

### Operational Insights
- Transaction volume trends across 52 weeks (weekly reporting)
- Customer satisfaction correlation with spending behavior
- Geographic distribution analysis (by state and zipcode)
- Card activation effectiveness within 30-day window

## Technical Stack
- **Data Integration**: SQL (PostgreSQL)
- **Data Analysis**: SQL queries, aggregations, joins
- **Visualization**: Power BI (interactive dashboards, KPI tracking)
- **Data Preparation**: CSV files (primary + incremental data)

## Project Structure
```
├── credit_card.csv              # Weekly transaction data (Weeks 1-52)
├── cc_add.csv                   # Week 53 additional transaction data
├── customer.csv                 # Customer demographic data (Weeks 1-52)
├── cust_add.csv                 # Week 53 additional customer data
├── SQL Query - Financial Dashboard Data.sql  # Database setup & data import
├── Credit card report.pbix       # Power BI dashboard
├── Credit card report.pdf        # Dashboard export (screenshots)
├── README.md                     # Project documentation
└── data_dictionary.md            # Column definitions & metadata
```

## Database Schema

### cc_detail Table
Contains weekly credit card transaction metrics per customer.
See `data_dictionary.md` for complete column definitions.

### cust_detail Table
Contains customer demographic and profile information.
See `data_dictionary.md` for complete column definitions.

## How to Use This Project

### 1. Database Setup (PostgreSQL)
```sql
-- Execute the SQL query file to create database and import all CSV files
psql -U postgres -f "SQL Query - Financial Dashboard Data.sql"
```

### 2. Connect to Power BI
- Open `Credit card report.pbix` in Power BI Desktop
- Update data source connection to your PostgreSQL database
- Refresh to load latest data

### 3. Dashboard Views Available
- **Executive Summary**: Key metrics, YTD revenue, customer acquisition
- **Transaction Analysis**: Spending patterns by category, payment method, region
- **Customer Segmentation**: Revenue by demographics, satisfaction analysis
- **Risk & Compliance**: Delinquency tracking, credit utilization trends
- **Card Performance**: By-category KPI comparison, activation rates
- **Marketing Performance**: CAC efficiency, customer lifetime value indicators

## Key Metrics & KPIs

| Metric | Definition | Business Impact |
|--------|-----------|-----------------|
| **Total Revenue** | Annual Fees + Interest Earned | Primary revenue driver |
| **Customer Acquisition Cost (CAC)** | Cost to acquire new customers | Marketing efficiency |
| **Total Transaction Amount** | Sum of all customer spending | Customer engagement |
| **Avg Utilization Ratio** | Revolving balance / Credit limit | Credit health indicator |
| **Delinquency Rate** | % of accounts with defaults | Risk management |
| **Activation Rate (30-day)** | % of cards activated within 30 days | New customer engagement |
| **Interest Earned** | Interest revenue per customer | Profitability metric |

## Data Quality & Integrity
- **Date Range**: January 1, 2023 - December 31, 2023 (52 weeks + Week 53 additional data)
- **Data Completeness**: 500K+ unique customers across all card categories
- **Validation**: All transactions linked to valid customer profiles with CDD/KYC information

## Insights for Financial Analysts
This project demonstrates:
- **Financial Data Analysis**: Revenue segmentation, profitability analysis by customer segment
- **Risk Assessment**: Delinquency monitoring, credit utilization tracking
- **Customer Analytics**: Lifetime value indicators, churn risk identification
- **Business Intelligence**: Trend identification, KPI dashboarding, decision support
- **Regulatory Alignment**: Compliance-ready data structure for financial reporting

## Next Steps & Enhancements
- Predictive modeling for churn risk and delinquency forecasting
- Customer lifetime value (CLV) calculations
- Cohort analysis for new customer retention tracking
- Profitability by customer segment (RFM analysis)
- Marketing attribution modeling

## Contact & Collaboration
For questions or collaboration on financial analytics projects:
- Email: anukritichaturvedi98@gmail.com
- LinkedIn: [Anukriti's LinkedIn](https://www.linkedin.com/in/anukriti-chaturvedi/)

---

**Note**: Power BI dashboard files (.pbix) require Power BI Desktop to edit. PDF version provides view-only snapshot of dashboard visuals.
