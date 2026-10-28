# Startup Survival: Exploratory Data Analysis

An exploratory data analysis (EDA) of **48,000 startups** founded between 2008 and 2021. The project checks data quality, then answers 35 structured questions about funding, industries, founding years, and five-year survival, and closes with recommendations and data limitations.

## Project Objective

To identify patterns and factors associated with startup survival and failure by examining the relationships between funding, market conditions, founder experience, team dynamics, and financial performance.

## Repository Structure

```
startup-survival-eda/
├── README.md
├── LICENSE
├── requirements.txt
├── .gitignore
├── Startup_Survival_Master_EDA.ipynb      # full analysis notebook
└── data/
    ├── startup_survival_master.csv            # raw dataset (48,000 rows x 30 columns)
    └── startup_survival_master_cleaned.csv    # output of the notebook's cleaning section
```

## Dataset

Each row is one startup (`startup_id`). Both CSVs have 48,000 rows and 30 columns. The dataset has no missing values and no duplicate rows, so the cleaning step did not change any records.

| Group | Columns |
|---|---|
| **Identity and context** | `startup_id`, `industry`, `founding_year`, `macro_climate`, `market_size_score`, `competition_intensity` |
| **Founders and team** | `founder_prior_exits`, `prior_failures`, `domain_experience_years`, `technical_cofounder`, `n_cofounders`, `cofounder_conflict`, `team_completeness`, `age_of_founder`, `weekly_hours` |
| **Funding and finances** | `funding_path`, `total_raised_usd`, `monthly_burn_rate`, `runway_months`, `unit_economics_score` |
| **Product and strategy** | `product_market_fit_score`, `did_customer_validation`, `premature_scaling`, `pivots`, `marketing_effectiveness` |
| **Outcome** | `years_to_outcome`, `outcome`, `failure_reason`, `survived_5y`, `failed` |

**Categories:**
- `industry` has 11 values: tech_saas, ecommerce, services, consumer_app, fintech, marketplace, food_bev, healthtech, hardware, biotech, agriculture.
- `funding_path` has 4 values: bootstrapped, angel, vc_seed, vc_series_a_plus.
- `outcome` has 4 values: failed, still_operating, acquired, ipo.

> **Data source:** *Add the source of the dataset here (e.g. Kaggle link or publisher) and confirm its license allows redistribution.*

## Methodology

1. **Data cleaning**: standardised column names, checked for duplicates, missing values, invalid years (outside 1900–2026), negative values, and invalid binary labels, and ran an IQR outlier check.
2. **Data understanding**: dimensions, data types, and summary statistics.
3. **Analysis**: 35 questions grouped into:
   - Dataset overview and data quality
   - Descriptive statistics
   - Pivot tables and comparative analysis
   - Visualisation: line, bar, histogram, box, scatter, pie, heatmap, and violin plots
   - Survival analysis and filtering or conditional queries
4. **Recommendations and limitations** based on the findings.

## Key Findings

- **Survival:** 50.7% of startups survived five years. Outcomes are 65.8% failed, 30.1% still operating, 4.1% acquired, and 10 IPOs.
- **Funding is highly skewed.** The mean raised is about $1.61M, but the median is only $111K, and the maximum is $52.2M.
- **Industry funding:** tech_saas has the highest total funding ($12.5B), while marketplace has the highest average ($1.69M). Average funding differs little across industries (about $1.48M to $1.69M).
- **Industry survival:** agriculture has the highest five-year survival rate (56.3%), and ecommerce the lowest (47.5%).
- **Funding path:** bootstrapped startups survive five years at 56.0%, against 37.6% for vc_series_a_plus startups. This is an association, not proof that VC funding causes failure. Later-stage funds may back riskier ventures.
- **Failure reasons:** the most common are no_market_need (12,376 startups) and ran_out_of_cash (8,981).
- **Cash:** average monthly burn is about $99K and average runway about 18.9 months.
- **Founding years:** total funding by founding year ranges from $5.16B (2013) to $5.89B (2015).
- **Survival drivers are weak individually.** The strongest correlations with `survived_5y` are product_market_fit_score (+0.15), runway_months (+0.11), and monthly_burn_rate (−0.10).

## Data Quality Notes

- **`failed` and `survived_5y` are not opposites.** 7,921 startups are marked both `failed = 1` and `survived_5y = 1`, meaning they survived five years and failed later. Define the target carefully before modelling.
- **Data leakage risk:** `years_to_outcome` (correlation +0.69 with `survived_5y`), `outcome`, `failed`, and `failure_reason` are outcome-related and should be excluded from any predictive model.
- **Funding skew:** a few highly funded startups heavily influence averages. Use medians and percentiles.
- **Founding year is not funding year.** The dataset has no dated funding records, so year-over-year funding change cannot be calculated.
- **Correlation does not prove causation.**

## How to Run

1. **Clone the repository**
   ```bash
   git clone https://github.com/<your-username>/startup-survival-eda.git
   cd startup-survival-eda
   ```
2. **Install dependencies** (a virtual environment is recommended)
   ```bash
   pip install -r requirements.txt
   ```
3. **Open the notebook** from the repository root, so the relative `data/` paths work
   ```bash
   jupyter notebook Startup_Survival_Master_EDA.ipynb
   ```

The cleaning section writes `data/startup_survival_master_cleaned.csv`, so you can regenerate the cleaned file by running it.

## Tools Used

- Python 3
- pandas, NumPy
- Matplotlib, Seaborn
- Jupyter Notebook

## Possible Next Steps

- Build a classification model to predict five-year survival, after resolving the target definition and removing leakage columns.
- Compare industries using medians and survival rates together, with sample sizes.
- Analyse failure reasons by funding path and industry.

## License

This project is released under the [MIT License](LICENSE).
