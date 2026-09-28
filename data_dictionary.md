# Data Dictionary

## cc_detail Table (Credit Card Transactions)

| Column Name | Data Type | Description | Example | Business Use |
|-------------|-----------|-------------|---------|--------------|
| **Client_Num** | INT | Unique customer identifier | 708082083 | Link to customer profile; primary key |
| **Card_Category** | VARCHAR(20) | Type of credit card issued | Blue, Silver, Platinum, Gold | Segment revenue; track product performance |
| **Annual_Fees** | INT | Annual fee charged to customer ($) | 200, 445, 250 | Revenue component; profitability analysis |
| **Activation_30_Days** | INT | Flag: Card activated within 30 days (1=Yes, 0=No) | 0, 1 | Measure new customer engagement; activation rate |
| **Customer_Acq_Cost** | INT | Cost to acquire this customer ($) | 87, 108, 106 | Calculate ROI; analyze marketing efficiency |
| **Week_Start_Date** | DATE | Start date of the reporting week | 01-01-2023, 31-12-2023 | Temporal analysis; weekly trends |
| **Week_Num** | VARCHAR(20) | Week identifier in the year | Week-1, Week-53 | Time period grouping; weekly reporting |
| **Qtr** | VARCHAR(10) | Quarter identifier | Q1, Q2, Q3, Q4 | Quarterly performance analysis |
| **current_year** | INT | Year of the transaction | 2023 | Multi-year comparison; data filtering |
| **Credit_Limit** | DECIMAL(10,2) | Maximum credit available to customer ($) | 3544, 8258, 1438.30 | Credit risk assessment; utilization analysis |
| **Total_Revolving_Bal** | INT | Outstanding balance carried forward ($) | 1661, 2517, 0 | Credit utilization indicator; risk monitoring |
| **Total_Trans_Amt** | INT | Total transaction amount in the week ($) | 15149, 992, 1447 | Spending patterns; customer engagement level |
| **Total_Trans_Ct** | INT | Number of transactions in the week | 111, 21, 23 | Transaction frequency; card usage intensity |
| **Avg_Utilization_Ratio** | DECIMAL(10,3) | Average revolving balance / Credit limit | 0.469, 0.736, 0.214 | Credit health metric; risk classification |
| **Use_Chip** | VARCHAR(10) | Payment method used | Chip, Swipe, Online | Payment technology adoption; fraud analysis |
| **Exp_Type** | VARCHAR(50) | Spending category | Travel, Bills, Grocery, Fuel, Entertainment, Food | Spending pattern analysis; targeted marketing |
| **Interest_Earned** | DECIMAL(10,3) | Interest revenue from this customer ($) | 4393.21, 69.44, 202.58 | Revenue component; profitability metric |
| **Delinquent_Acc** | VARCHAR(5) | Flag: Account in default (1=Yes, 0=No) | 0, 1 | Risk monitoring; compliance tracking |

---

## cust_detail Table (Customer Demographics)

| Column Name | Data Type | Description | Example | Business Use |
|-------------|-----------|-------------|---------|--------------|
| **Client_Num** | INT | Unique customer identifier | 708082083, 708083283 | Primary key; link to transactions |
| **Customer_Age** | INT | Age of the customer (years) | 24, 62, 32, 38 | Age-based segmentation; demographic analysis |
| **Gender** | VARCHAR(5) | Gender of customer | M, F | Gender-based targeting; diversity analysis |
| **Dependent_Count** | INT | Number of dependents | 0, 1, 2, 3, 4, 5 | Household size indicator; financial capacity proxy |
| **Education_Level** | VARCHAR(50) | Highest education attained | Uneducated, High School, Graduate, Post-Graduate, Doctorate | Income predictor; behavioral segmentation |
| **Marital_Status** | VARCHAR(20) | Marital status | Single, Married, Unknown | Household structure; spending propensity |
| **state_cd** | VARCHAR(50) | US state code | FL, NJ, NY, TX, CA, etc. | Geographic segmentation; regional analysis |
| **Zipcode** | VARCHAR(20) | Postal code | 91750 | Location-based targeting; regional patterns |
| **Car_Owner** | VARCHAR(5) | Flag: Customer owns car (yes/no) | yes, no | Wealth indicator; spending capacity proxy |
| **House_Owner** | VARCHAR(5) | Flag: Customer owns house (yes/no) | yes, no | Asset indicator; financial stability; credit risk |
| **Personal_Loan** | VARCHAR(5) | Flag: Customer has personal loan (yes/no) | yes, no | Debt level indicator; creditworthiness assessment |
| **contact** | VARCHAR(50) | Preferred contact method | cellular, telephone, unknown | Communication channel preference |
| **Customer_Job** | VARCHAR(50) | Occupation/Job category | Businessman, Selfemployeed, Blue-collar, White-collar, Govt, Retirees | Income predictor; occupation-based segmentation |
| **Income** | INT | Annual household income ($) | 202326, 5225, 14235, 45683 | Primary spending capacity indicator; credit risk |
| **Cust_Satisfaction_Score** | INT | Customer satisfaction rating | 1, 2, 3, 4, 5 | Churn risk indicator; service quality metric |

---

## Key Metrics Calculations

### Revenue Metrics
- **Total Revenue** = SUM(Annual_Fees) + SUM(Interest_Earned)
- **Revenue per Customer** = Total Revenue / Distinct Count(Client_Num)
- **Revenue by Card Category** = Revenue filtered by Card_Category

### Customer Engagement Metrics
- **Activation Rate** = COUNT(Activation_30_Days=1) / Total Customers × 100
- **Average Transaction Amount** = SUM(Total_Trans_Amt) / COUNT(Total_Trans_Ct)
- **Customer Acquisition Cost (CAC)** = SUM(Customer_Acq_Cost) / New Customers

### Risk & Credit Metrics
- **Delinquency Rate** = COUNT(Delinquent_Acc=1) / Total Customers × 100
- **Average Utilization Ratio** = AVG(Avg_Utilization_Ratio)
- **Credit Health Score** = Low utilization ratio + No delinquency flag + Positive interest earned

### Spending Pattern Metrics
- **Total Spending by Category** = SUM(Total_Trans_Amt) grouped by Exp_Type
- **Transaction Frequency** = AVG(Total_Trans_Ct) by customer segment
- **Chip vs Swipe Adoption** = COUNT(Use_Chip) / Total Transactions

### Customer Segmentation Metrics
- **By Income Level** = Revenue/Customer count grouped by Income brackets
- **By Education** = Spending patterns across Education_Level
- **By Occupation** = Revenue segmentation by Customer_Job
- **By Demographics** = Age, Gender, Marital Status, Family Size analysis

---

## Data Quality Notes

### Date Handling
- Week_Start_Date format: DD-MM-YYYY
- Data spans 52 weeks (Jan 1 - Dec 31, 2023) plus Week 53 supplementary data
- All dates are ISO week dates (Monday start)

### Missing/Null Values
- **state_cd, contact, Education_Level**: Some "Unknown" values indicate missing data
- **Marital_Status**: "Unknown" indicates data not provided during KYC
- All financial columns (Income, Fees, etc.) are complete with no nulls

### Categorical Values
- **Activation_30_Days**: Binary (0 or 1)
- **Delinquent_Acc**: Binary (0 or 1)
- **Car_Owner, House_Owner, Personal_Loan, contact**: Categorical
- **Cust_Satisfaction_Score**: Scale 1-5 (1=Low, 5=High)
- **Use_Chip**: Values are "Chip ", "Swipe ", "Online " (note trailing spaces)

### Data Constraints
- Credit_Limit > 0 for all records
- Total_Revolving_Bal ≤ Credit_Limit (enforced by credit policies)
- Avg_Utilization_Ratio ranges 0.0 - 1.0
- All monetary values in USD ($)
- All transaction volumes in count units

---

## SQL Join Reference

To combine transaction and customer data:

```sql
SELECT 
    cc.Client_Num,
    cc.Card_Category,
    cc.Total_Trans_Amt,
    cc.Interest_Earned,
    cc.Delinquent_Acc,
    cust.Customer_Age,
    cust.Income,
    cust.Customer_Job,
    cust.Cust_Satisfaction_Score
FROM cc_detail cc
INNER JOIN cust_detail cust ON cc.Client_Num = cust.Client_Num
WHERE cc.current_year = 2023;
```

---

## Analytical Frameworks Using This Data

### 1. Customer Segmentation (RFM Analysis)
- **Recency**: Last transaction date (Week_Num)
- **Frequency**: Total_Trans_Ct over time
- **Monetary**: Total_Trans_Amt or Interest_Earned

### 2. Risk Classification
- **Low Risk**: Utilization < 0.3, No delinquency, Active usage
- **Medium Risk**: Utilization 0.3-0.7, Occasional usage
- **High Risk**: Utilization > 0.7, Delinquent flag, Low activity

### 3. Customer Profitability
- **High Profitability**: High Interest_Earned + Annual_Fees, Low CAC
- **Medium Profitability**: Moderate metrics across all dimensions
- **Low Profitability**: High CAC, Low Interest_Earned, Early churn risk

### 4. Demographic Insights
- **Income Correlation**: Income vs. Total_Trans_Amt, Credit_Limit
- **Education Impact**: Education_Level vs. Average spending, utilization
- **Occupation Analysis**: Customer_Job vs. Card_Category preference

---

## Compliance & Regulatory Mapping

| Column | Regulatory Purpose | Compliance Framework |
|--------|------------------|----------------------|
| Client_Num, Customer_Age, Gender | KYC (Know Your Customer) | AML/CFT Compliance |
| Income, Dependent_Count, House_Owner | Risk Assessment | Credit Risk Framework |
| Delinquent_Acc | Default Monitoring | NPL (Non-Performing Loan) Tracking |
| Total_Trans_Amt, Total_Revolving_Bal | Transaction Monitoring | AML Transaction Reporting |
| Cust_Satisfaction_Score | Service Quality | Customer Protection Regulations |

---

**Last Updated**: 2024
**Data Source**: Credit card portfolio and customer relationship management system
**Contact**: anukritichaturvedi98@gmail.com
