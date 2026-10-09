# Customer Churn Analysis

Exploratory analysis of 7,043 telecom customers to find who churns and what drives it. The analysis covers contract type, tenure, services, billing and payment method, and checks whether the headline "Electronic Check users churn most" finding holds once contract type is controlled for.

**Tools:** Python, Pandas, NumPy, Matplotlib, Seaborn (Jupyter Notebook)

## Key findings

**Overall churn is 26.5%** (1,869 of 7,043 customers). Churned customers pay more per month (74.4 vs 61.3 on average) and account for 30.5% of total monthly charges.

| Driver | Churn rate |
|---|---|
| Month-to-month contract | **42.7%** (one year 11.3%, two year 2.8%) |
| Tenure 0–6 months | **52.9%** (49–72 months: 9.5%) |
| Fiber optic internet | 41.9% (DSL 19.0%) |
| Internet users with neither Online Security nor Tech Support | **49.0%** (with both: 9.0%) |
| Senior citizens | 41.7% (non-senior 23.6%) |
| Paperless billing | 33.6% (no paperless 16.3%) |
| Electronic check payment | 45.3% (credit card auto-pay 15.2%) |

- **89% of all churners are on month-to-month contracts**, and **55% of churners leave within their first 12 months.**
- Gender has no meaningful effect (26.9% vs 26.2%). Streaming TV/Movies and phone service also show little difference.

## Is the Electronic Check effect real?

The raw gap is large (45.3% vs ~16% for auto-pay), but **78% of electronic check users are on month-to-month contracts**, versus 36–38% for auto-pay users. Part of the gap is contract mix.

Churn rate by payment method within each contract type:

| Contract | Bank transfer (auto) | Credit card (auto) | Electronic check | Mailed check |
|---|---|---|---|---|
| Month-to-month | 34.1% | 32.8% | **53.7%** | 31.6% |
| One year | 9.7% | 10.3% | 18.4% | 6.8% |
| Two year | 3.4% | 2.2% | 7.7% | 0.8% |

Electronic check still has the highest churn in every contract type, so payment method adds real risk, but the gap on month-to-month contracts is about 20 points, not the raw ~29. Mailed check customers are not a high-risk group once contract is controlled for.

If month-to-month e-check customers (1,850 of them) churned at the auto-pay rate (~33.5%), roughly 375 customers would be retained, about 20% of all churn. This assumes the payment effect is causal, which this analysis cannot confirm.

## Recommendations

1. Prioritise month-to-month customers: offer incentives to move to 1–2 year contracts (the largest churn driver).
2. Focus onboarding and retention effort on the first 6–12 months of tenure.
3. Target electronic check customers on month-to-month contracts with auto-pay migration offers.
4. Bundle or promote Online Security and Tech Support for internet customers.
5. Run an A/B test of an auto-pay incentive before assuming the payment effect is causal.
6. Track churn by contract type, tenure and payment method on a regular dashboard.

## Data and cleaning

- **Dataset:** Telco Customer Churn, 7,043 rows × 21 columns (customer demographics, services, contract, billing, churn flag).
- No null values and no duplicate rows or customer IDs.
- `TotalCharges` had 11 blank values, all for customers with tenure 0 (no charges billed yet). These were set to 0 and the column converted to float.
- `SeniorCitizen` (0/1) was converted to yes/no for readable charts.
- Added `Churn_flag` (1/0), `AutoPay` and `TenureGroup` (0–6, 7–12, 13–24, 25–48, 49–72 months) for rate calculations.

## Limitations

- Findings are associations, not causes. Contract, tenure, internet service and payment method overlap heavily, so the ranking shows where churn concentrates.
- Fiber optic customers pay more and are more often on flexible contracts, so the Fiber vs DSL gap may reflect price or contract, not the technology.
- The dataset is a snapshot with no churn dates, so time-based analysis is not possible.
- No predictive model was built. This project is exploratory analysis only.

## Repository contents

- `CCA.ipynb`: full analysis notebook
- `Dataset.csv`: source data
- `SUMMARY_AND_RECOMMENDATIONS.pdf`: one-page summary of insights and recommendations

## How to run

```bash
pip install pandas numpy matplotlib seaborn jupyter
jupyter notebook CCA.ipynb
```
Keep `Dataset.csv` in the same folder as the notebook.
