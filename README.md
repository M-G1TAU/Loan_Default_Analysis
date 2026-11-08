# Loan Default Risk Analysis

A data analysis project exploring the key drivers of loan defaults and portfolio behaviour using Python (pandas + matplotlib).

**Status:** First personal data analytics project  
**Tools:** Python, pandas, matplotlib, seaborn  
**Dataset:** 601 loan applications + 500 borrower profiles (merged on `borrower_id`)

---

## Project Overview

This project analyses personal loan applications to identify factors most strongly associated with default and to surface behavioural and geographic patterns that a lending institution could use for risk management and portfolio strategy.

### Key Questions Explored
- Which borrower and loan characteristics are most correlated with default?
- How does default risk vary by credit score, DTI, interest rate, employment status, loan purpose and state?
- Are there practical thresholds or geographic differences the lending team should examine further?

<img width="640" height="480" alt="credit_score-range" src="https://github.com/user-attachments/assets/b32dd0a1-86be-48ad-8664-4f91a539b40f" />

<img width="640" height="480" alt="credit_score-range1" src="https://github.com/user-attachments/assets/982fb3c6-8310-4e59-a53a-9388408493b1" />

<img width="640" height="480" alt="dti_range" src="https://github.com/user-attachments/assets/10ed309c-0934-47ca-93e5-eefc46b9f599" />

<img width="640" height="480" alt="employment_status" src="https://github.com/user-attachments/assets/5fc4b558-4bd8-4d5f-962e-5b6f6f8d8f27" />

<img width="640" height="480" alt="interest_range" src="https://github.com/user-attachments/assets/7aaa1e61-9a83-45ca-92b4-d61d0111ee33" />


<img width="2200" height="800" alt="loan_purpose" src="https://github.com/user-attachments/assets/a01efc11-8d61-46cf-9e55-93ac250966d3" />

## Dataset

| File | Records | Key Fields |
|------|---------|------------|
| `loan_applications.csv` | 601 | loan amount, interest rate, DTI, term, purpose, status, days delinquent, defaulted |
| `borrower_profiles.csv` | 500 | age, employment status, credit score, annual income, home ownership, dependents, state |

Final merged dataset: **601 loans**, 22 columns. Overall default rate: **24.3%**.

---

## Analysis Approach

1. Data loading, null checks and merge on `borrower_id`
2. Creation of categorical segments (credit score, DTI, interest rate ranges)
3. Default-focused exploration and correlation analysis
4. Extended behavioural analysis by loan purpose and state (sample size + default rate + income)

---

## Key Findings

### 1. Strongest Correlations with Default

| Feature | Correlation | Insight |
|---------|-------------|---------|
| Days Delinquent | **+0.88** | Very strong positive relationship. Loans past 30 days delinquent carry high risk. |
| Credit Score | **-0.29** | Lower credit scores linked to higher default rates. |
| Interest Rate | **+0.20** | Higher rates associated with higher default risk. |
| DTI Ratio | **+0.19** | Higher debt-to-income increases default likelihood. |

### 2. Credit Score, DTI & Interest Rate Patterns
- Highest default counts in credit score band **500–599**. Defaults fall sharply above 700.
- Most defaults sit in the **51–75% DTI** range.
- Defaults concentrated in the **9–12%** and **Above 12%** interest rate brackets.
- Non-defaulters generally receive lower interest rates than defaulters.

### 3. Loan Purpose – Behavioural Differences

Average loan amounts differ meaningfully between non-defaulters and defaulters:

| Loan Purpose | Non-defaulters (avg) | Defaulters (avg) | Observation |
|--------------|----------------------|------------------|-------------|
| Auto Loan | $18,405 | $22,644 | Non-defaulters borrow ~$4.2k less |
| Business Loan | $22,480 | $16,407 | Non-defaulters borrow ~$6.1k **more** |
| Education | $17,115 | $29,183 | Non-defaulters borrow ~$12.1k less |
| Debt Consolidation | $21,030 | $29,036 | Non-defaulters borrow ~$8.0k less |
| Medical Expenses | $21,298 | $30,421 | Non-defaulters borrow ~$9.1k less |

Possible interpretations:
- Smaller Auto / Education / Debt Consolidation loans may be more sustainable.
- Larger Business loans among non-defaulters may reflect businesses that generate cash flow supporting repayment — worth monitoring.

### 4. Geographic Insights (State-level)

Sample sizes are small for many states, so rates should be treated cautiously. Key contrasts:

| State | Loans | Default Rate | Avg Income | Note |
|-------|-------|--------------|------------|------|
| VA | 12 | **58.3%** | $57.5k | Highest rate (small sample) |
| CA | 12 | **50.0%** | $63.6k | High rate despite above-average income |
| MO | 31 | **41.9%** | $58.1k | High rate, larger sample |
| TX | 12 | **41.7%** | $56.5k | High rate |
| CO | 22 | **31.8%** | $65.7k | Elevated rate with higher income |
| NC | 33 | **18.2%** | $67.8k | Lower rate, higher income |
| PA | 12 | **16.7%** | $56.8k | Same sample size as CA/TX but much lower default |
| LA | 18 | **0.0%** | $74.9k | No defaults in this sample |

Notable comparisons:
- **PA vs CA** (both 12 loans): 16.7% vs 50% default rate.
- **NC vs MO** (33 vs 31 loans): 18.2% vs 41.9% default rate. NC also has ~$10k higher average income.
- Several lower-income states show elevated default rates, consistent with an income-related risk pattern, but CA and CO are exceptions that need further investigation.

---

## Recommendations

1. **Credit policy**: Consider tighter criteria or enhanced review for credit scores below 600 and DTI above 50%.
2. **Delinquency management**: Act early once a loan reaches 30 days past due.
3. **Product review**: Examine underwriting and pricing for Home Improvement, Wedding, Education and larger Debt Consolidation loans.
4. **Geographic deep-dive**: Investigate CA, CO, VA, MO and TX (high default) versus PA, NC and LA (lower default) for differences in borrower mix, product mix or local conditions.
5. **Business loans**: Larger business loans among non-defaulters suggest potential value in tracking business performance post-disbursement.

---

## Limitations

- Dataset covers only ~2 years (2024–2025) — too short for reliable trend analysis.
- Many states have small sample sizes (especially CA, PA, TX, VA with only 12 loans each). Default rates on small samples are volatile.
- No collateral / home-value data for home-related loans.
- Analysis is descriptive and correlational; it does not prove causation.

---

## How to Run

```bash
pip install pandas matplotlib seaborn
