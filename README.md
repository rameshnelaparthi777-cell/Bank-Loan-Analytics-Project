# Bank-Loan-Analytics-Project

##  Project Overview
This project analyzes customer bank loan data using **SQL, Python, and Power BI**. The goal is to provide insights on:

- Year-wise Loan Amount trends
- Grade/Sub-grade Revolving Balance analysis
- Total Payment vs Verification Status
- State-wise and Month-wise Loan Status
- Home Ownership vs Last Payment Date
- Charged-Off Loans and Default Rates

The dashboard is fully **interactive, visually appealing, and professional**, designed to impress recruiters.

---

##  Dataset
- **Finance_1.csv**: Customer loan details
- **Finance_2.xlsx**: Additional financial metrics
- **Merged_Finance.csv**: Cleaned and merged dataset for analysis

---

##  Tools & Technology
- **SQL**: Queries for data aggregation, YoY calculations, and KPI extraction
- **Python (pandas)**: Data cleaning, merging, and preprocessing
- **Power BI**: Dashboard creation with KPIs, cards, matrix, and visualizations

---
##  Key KPIs
- Loan Amount YoY
- Revolving Balance by Grade/Sub-grade
- Total Payment by Verification Status
- State-wise and Month-wise Loan Analysis
- Charged-Off Loans and Default Rate
- Home Ownership vs Last Payment Date Analysis

---
##  SQL Queries
## 1 Year-wise Loan Amount 
SELECT issue_year, SUM(loan_amnt) AS total_loan_amount
FROM merged_finance
GROUP BY issue_year
ORDER BY issue_year;
## 2 Revolving Balance by Grade 
SELECT grade, SUM(revol_bal) AS total_revol_bal
FROM merged_finance
GROUP BY grade
ORDER BY grade;
## 3 Total Payment by Verification Status 
SELECT verification_status, SUM(total_pymnt) AS total_payment
FROM merged_finance
GROUP BY verification_status;
##  4 State-wise Loan Status Summary
SELECT addr_state, loan_status, COUNT(*) AS total_loans
FROM merged_finance
GROUP BY addr_state, loan_status
ORDER BY addr_state;
## 5 Loan Amount YoY Change 
SELECT 
    issue_year,
    SUM(loan_amnt) AS total_loan,
    LAG(SUM(loan_amnt)) OVER (ORDER BY issue_year) AS prev_year_loan,
    ROUND(((SUM(loan_amnt) - 
            LAG(SUM(loan_amnt)) OVER (ORDER BY issue_year))
            / LAG(SUM(loan_amnt)) OVER (ORDER BY issue_year)) * 100,2) 
            AS yoy_percentage
FROM merged_finance
GROUP BY issue_year
ORDER BY issue_year;
## 6 Charged-Off Loans Count & Default Rate 
SELECT 
    issue_year,
    SUM(CASE WHEN LOWER(loan_status) LIKE '%charged%' THEN 1 ELSE 0 END) AS charged_off_count,
    COUNT(*) AS total_loans,
    ROUND((SUM(CASE WHEN LOWER(loan_status) LIKE '%charged%' THEN 1 ELSE 0 END)
          / COUNT(*)) * 100,2) AS default_rate_pct
FROM merged_finance
GROUP BY issue_year
ORDER BY issue_year;
## 7 Home Ownership Analysis 
SELECT home_ownership, COUNT(*) AS total_loans
FROM merged_finance
GROUP BY home_ownership
ORDER BY total_loans DESC;
## 8 Grade & Subgrade Distribution 
SELECT grade, sub_grade, COUNT(*) AS loan_count
FROM merged_finance
GROUP BY grade, sub_grade
ORDER BY grade, sub_grade;
## 9 Monthly Loan Amount Trend 
SELECT issue_year, issue_month, SUM(loan_amnt) AS total_loan
FROM merged_finance
GROUP BY issue_year, issue_month
ORDER BY issue_year, issue_month;

---

##  Python Data Cleaning

- Merge Finance_1.csv and Finance_2.xlsx
- Clean nulls and duplicates
- Generate derived columns (Year, Month)
- Prepare the dataset for Power BI

---

##  Power BI Dashboard

- Interactive cards for each KPI
- Year-wise and Month-wise charts
- Tree maps, matrix tables, and line charts
- Filters for states, grades, and verification status

---

##  Screenshots
![DASHBOARD](https://github.com/rameshnelaparthi777-cell/Bank-Loan-Analytics-Project/blob/main/POWER%20BI%20DASHBOARD%20SCREENSHOT.png)

---

## Business Insights 

Verified customers have higher repayment stability

Grade A–C customers show lower revolving balance, meaning better risk profile

Certain states show high default concentration

YoY loan disbursements show steady growth

Home ownership strongly correlates with higher repayment tendencies


