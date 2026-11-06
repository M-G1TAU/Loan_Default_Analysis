# Loan_Default_Analysis
A project on analyst builder to understand why loan default rates are higher at 24% compared to the acceptable threshold of 12%

# Loan Default Risk Analysis

A data analysis project exploring the key drivers of loan defaults using Python (pandas + matplotlib/seaborn).

**Status:** First personal data analytics project  
**Tools:** Python, pandas, matplotlib, seaborn  
**Dataset:** 601 loan applications + 500 borrower profiles

---

## Project Overview

This project analyzes a dataset of personal loan applications to identify factors most strongly associated with loan defaults. The goal is to provide clear, actionable insights that a lending institution could use to improve risk assessment and reduce default rates.

### Key Questions Explored
- Which borrower and loan characteristics are most correlated with default?
- How does default risk vary by credit score, debt-to-income (DTI) ratio, interest rate, employment status, and loan purpose?
- Are there practical thresholds the lending team could use when approving loans?

---

## Dataset

Two CSV files were merged on `borrower_id`:

| File | Records | Key Fields |
|------|---------|------------|
| `loan_applications.csv` | 601 | loan amount, interest rate, DTI, term, purpose, status, days delinquent, defaulted |
| `borrower_profiles.csv` | 500 | age, employment status, credit score, annual income, home ownership, dependents |

After merging, the final dataset contains **601 loans** and **22 columns**.

---

## Analysis Approach

1. **Data Cleaning & Exploration**
   - Checked for null values
   - Merged the two datasets
   - Created categorical segments for easier analysis:
     - Credit Score ranges
     - DTI ranges
     - Interest Rate ranges

2. **Default Analysis**
   - Focused on loans where `defaulted = 1`
   - Examined default counts and patterns across key segments

3. **Correlation Analysis**
   - Calculated Pearson correlation between `defaulted` and numeric features

---

## Key Findings

### Strongest Correlations with Default

| Feature | Correlation | Insight |
|---------|-------------|---------|
| Days Delinquent | **+0.88** | Very strong positive relationship. Loans past 30 days delinquent are at high risk. |
| Credit Score | **-0.29** | Lower credit scores are linked to higher default rates. |
| Interest Rate | **+0.20** | Higher interest rates are associated with higher default risk. |
| DTI Ratio | **+0.19** | Higher debt-to-income ratios increase default likelihood. |

### Default Patterns by Segment

- **Credit Score**: Highest number of defaults in the 500–599 range. Defaults drop sharply once credit scores reach 700+.
- **DTI Ratio**: Most defaults occur in the 51–75% range.
- **Interest Rate**: Defaults are concentrated in the 9–12% and Above 12% brackets.
- **Loan Purpose**: Home Improvement and Wedding loans show the highest default counts.
- **Employment Status**: Full-Time employees account for the largest share of defaults (simply because they make up the majority of the portfolio).

---

## Recommendations

1. **Tighten credit policy** for applicants with credit scores below 600.
2. **Flag or decline** applications with DTI above 50%.
3. **Monitor closely** any loan that reaches 30+ days delinquent.
4. **Review pricing and approval criteria** for Home Improvement and Wedding loans.
5. Consider fixed-rate products where possible to reduce interest-rate-driven default risk.

---

## Limitations

- The dataset covers only ~2 years (2024–2025). This is too short to reliably detect long-term trends.
- No information on collateral values (especially relevant for home improvement loans).
- Analysis is descriptive and correlational — it does **not** prove causation.

---

## How to Run the Analysis

1. Clone the repository
2. Install dependencies:
   ```bash
   pip install pandas matplotlib seaborn
