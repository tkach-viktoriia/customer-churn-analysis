# Customer Churn & Retention Analysis

This repository contains an analysis of customer churn for a subscription-based business. The goal is to identify which customer segments are most at risk of leaving, what behavioral signals predict churn, and where the business should focus retention efforts.

The full analysis is available in the [Jupyter notebook](https://github.com/tkach-viktoriia/customer-churn-analysis/blob/main/customer_churn_analysis.ipynb).

## Main Summary & Recommendation

- **Recommendation:** Prioritize retention campaigns for monthly contract holders and female customers — these two segments drive the majority of churn.
- **Key Finding:** 56.7% of customers churned — the business is losing more customers than it retains. Monthly contract customers show a 100% churn rate, making contract type the single strongest predictor of churn.
- **Top Behavioral Signal:** Churned customers contact support 3x more often than retained customers (5.1 vs 1.6 calls on average), making support call frequency a reliable early warning indicator.

## Data Audit & Cleaning

The dataset was inspected for missing values, duplicates, and data type inconsistencies before any analysis was performed.

| Check | Result |
|---|---|
| Total rows loaded | 440,833 |
| Rows removed (missing values) | 1 |
| Duplicate rows | 0 |
| Rows analyzed | 440,832 |
| Columns with incorrect dtype (float → int) | 9 |

All numeric columns were stored as `float64` despite representing whole numbers (age, tenure, support calls, etc.). These were converted to `int64` to reflect the true nature of the data. The single row containing missing values was removed as it had nulls across all columns.

## Exploratory Data Analysis

| Check | Result |
|---|---|
| Total customers analyzed | 440,832 |
| Churned customers | 249,999 (56.7%) |
| Retained customers | 190,833 (43.3%) |
| Age range | 18 — 65 |
| Tenure range | 1 — 60 months |
| Total Spend range | $100 — $1,000 |

The dataset is well-balanced across subscription types (~33% each) and contract lengths (Annual: 40.2%, Quarterly: 40.0%, Monthly: 19.8%). Gender split is 56.8% Male / 43.2% Female.

## Key Findings

### 1. Contract Length — Strongest Churn Driver

| Contract Length | Churn Rate |
|---|:---:|
| Monthly | 100.0% |
| Annual | 46.1% |
| Quarterly | 46.0% |

Every single monthly customer churned. This is the most critical finding in the dataset — the monthly contract structure has zero retention. Annual and quarterly contracts perform similarly at ~46%, suggesting the issue is specific to the monthly model rather than a general dissatisfaction with the product.

### 2. Gender Gap in Churn

| Gender | Churn Rate |
|---|:---:|
| Female | 66.7% |
| Male | 49.1% |

Female customers churn at a 17.6 percentage point higher rate than male customers. This gap is significant enough to suggest a product-market fit issue for a specific user segment rather than random variance.

### 3. Subscription Type — No Significant Impact

| Subscription Type | Churn Rate |
|---|:---:|
| Basic | 58.2% |
| Standard | 56.1% |
| Premium | 55.9% |

Churn rates are nearly identical across all subscription tiers (2.3pp spread). This confirms that churn is driven by customer behavior and contract structure — not by price point or plan features.

### 4. Behavioral Signals (Churned vs Stayed)

| Metric | Stayed | Churned | Delta |
|---|:---:|:---:|:---:|
| Avg. Support Calls | 1.6 | 5.1 | +3.5 |
| Avg. Payment Delay (days) | 10.0 | 15.2 | +5.2 |
| Avg. Total Spend ($) | $749 | $541 | −$208 (−28%) |
| Avg. Age | 36.3 | 41.8 | +5.5 |
| Avg. Tenure (months) | 32.3 | 30.5 | −1.8 |

Customers who churn spend 28% less, contact support 3x more often, and delay payments more frequently. These three signals — support calls, payment delay, and total spend — form the basis for a potential early warning system.

## Contextual Hypotheses & Dataset Limitations

1. **Support Calls as a Churn Predictor:** The 3x gap in support call frequency between churned and retained customers suggests that dissatisfaction manifests in service interactions before the customer actually leaves. A threshold-based alert (e.g., flagging customers with 4+ support calls) could enable proactive retention outreach.
2. **Monthly Contract Structural Issue:** The 100% churn rate on monthly contracts may reflect a selection effect — customers who choose monthly contracts may already have lower commitment intent. Alternatively, the monthly billing cycle may increase churn opportunity by presenting a regular cancellation decision point. Distinguishing between these hypotheses would require event-level data on cancellation timing relative to billing dates.
3. **Gender Gap Hypothesis:** The higher female churn rate may reflect differences in product usage patterns, communication preferences, or unmet needs within the product experience. This cannot be confirmed without qualitative data (surveys, session recordings, or segmented feature usage logs).
4. **Dataset Limitation:** This dataset contains aggregated customer-level metrics without event timestamps or behavioral sequences. Proving causal relationships between the identified signals and churn decisions would require raw clickstream or CRM event data.

## Repository Structure

- `README.md`
- `customer_churn_analysis.ipynb` — Main analysis notebook
- `customer_churn_dataset.csv` — Raw dataset
- `customer_churn_cleaned.csv` — Cleaned dataset used for Tableau
- `customer_churn_dashboard.png` — Tableau dashboard screenshot

## Dashboard

[View Interactive Dashboard on Tableau Public](https://public.tableau.com/shared/YKWCMM2BJ?:display_count=n&:origin=viz_share_link)

## Data Source

Dataset sourced from [Kaggle — Customer Churn Dataset](https://www.kaggle.com/datasets/ahmedemadmorad/customer-churn-dataset).
