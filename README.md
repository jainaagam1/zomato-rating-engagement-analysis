# Zomato Restaurant Analysis: What Drives Ratings and Customer Engagement?

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![SQLite](https://img.shields.io/badge/SQL-SQLite-lightgrey)
![Status](https://img.shields.io/badge/Status-In%20Progress-orange)

> Python + SQLite analysis of what drives Zomato restaurant ratings and votes: table booking, online delivery, price tier, vote outliers and hidden gems.

---

## Table of Contents
1. [Business Question](#business-question)
2. [Key Findings](#key-findings)
3. [Recommendations](#recommendations)
4. [About the Dataset](#about-the-dataset)
5. [KPIs and Metrics](#kpis-and-metrics)
6. [Approach](#approach)
7. [Tools and Requirements](#tools-and-requirements)
8. [Repository Structure](#repository-structure)
9. [How to Run](#how-to-run)
10. [Limitations](#limitations)
11. [Author](#author)

---

## Business Question

Which restaurant attributes (table booking, online delivery, price tier) are associated with higher ratings and more customer votes, and which highly rated restaurants are still under-discovered?

This matters to two audiences:
- **Restaurant owners:** which service features and pricing choices go with better customer perception.
- **Platform teams (e.g. Zomato):** which high-quality restaurants deserve more visibility.

---

## Key Findings

> ⚠️ Replace every `X` and `[...]` below with the real numbers from your notebook and SQL queries. Delete this note when done.

1. **Table booking and ratings.** Restaurants offering table booking have **X% higher** average ratings than those without ([X.X vs X.X]), but [add caveat, e.g. the gap shrinks within the same price tier].

   ![Rating by table booking](images/rating_by_booking.png)

2. **Price tier and votes.** Votes are driven mostly by **[price tier / cost]**, while ratings show a **[weak / moderate / strong]** relationship with cost (Spearman ρ = X.XX).

   ![Rating vs price](images/price_vs_rating.png)

3. **Online delivery.** Restaurants with online delivery have **[higher / lower / similar]** average ratings (X.X vs X.X) and **X% [more / fewer]** votes on average.

4. **Hidden gems.** **N restaurants** have a rating of **≥ X.X** but fewer than **Y votes**, concentrated in **[cuisine / city / price tier]**.

5. **Vote outliers.** A small share of restaurants (**X%**) accounts for **Y%** of all votes, which makes averages misleading, so medians are reported alongside means.

---

## Recommendations

- **For restaurants:** [e.g. enabling table booking is associated with better ratings, particularly in the X price tier.]
- **For the platform:** [e.g. promote the N hidden-gem restaurants to increase their discoverability.]
- **For further analysis:** [e.g. test the effect within city and cuisine segments to control for confounders.]

---

## About the Dataset

| Item | Detail |
|---|---|
| **Name** | Restaurant Market Analysis: Ratings, Prices |
| **Source** | [Kaggle: srisyra02/zomato-market-analysis](https://www.kaggle.com/datasets/srisyra02/zomato-market-analysis) |
| **Description** | Restaurant ratings, cuisines and pricing data from Zomato |
| **File used** | `Zomato_Restaurant_Dataset.xlsx` (in `data/`) |
| **Rows** | [N] |
| **Columns** | [N] |

### Key columns used
> Update this table to match your actual column names.

| Column | Description |
|---|---|
| `[restaurant name]` | Name of the restaurant |
| `[cuisines]` | Cuisine types served |
| `[rating]` | Aggregate customer rating |
| `[votes]` | Number of customer votes |
| `[average cost]` | Approximate cost for two / price indicator |
| `[table booking]` | Whether table booking is available (Yes/No) |
| `[online delivery]` | Whether online delivery is available (Yes/No) |

### Data cleaning steps
- [e.g. Removed duplicates: N rows]
- [e.g. Handled missing values in rating/cost: method used]
- [e.g. Standardised Yes/No columns]
- [e.g. Created price tier bins: Low / Medium / High]

---

## KPIs and Metrics

| KPI | Definition | Where computed |
|---|---|---|
| **Average rating** | Mean rating overall and by segment | SQL + Python |
| **Average votes** | Mean (and median) votes per restaurant | SQL + Python |
| **Rating uplift (booking / delivery)** | % difference in average rating between restaurants with and without the feature | SQL (`CASE WHEN`, `GROUP BY`) |
| **Rating by price tier** | Average rating per price bucket | SQL + Python |
| **Rating-cost correlation** | Spearman and Pearson coefficients between rating, votes and cost | Python |
| **Vote outliers** | Restaurants with votes beyond the IQR upper fence | Python |
| **Hidden gems** | High rating (≥ threshold) with low votes (≤ threshold) | SQL (`HAVING COUNT`) |

---

## Approach

1. **Data loading and cleaning** in pandas
2. **Exploratory analysis:** distributions, missing values, outliers
3. **SQL analysis in SQLite:** aggregation and segmentation queries (`AVG`, `GROUP BY`, `CASE WHEN`, `HAVING COUNT`)
4. **Visualisation:** seaborn boxplots, violin plots, correlation heatmaps (Spearman and Pearson)
5. **Insight synthesis:** findings and recommendations

---

## Tools and Requirements

- **Language:** Python 3.10+
- **Libraries:** pandas, numpy, matplotlib, seaborn, scipy, openpyxl, jupyter
- **Database:** SQLite (built from the Excel file by the notebook)

```bash
pip install -r requirements.txt
```

---

## Repository Structure

```
zomato-rating-engagement-analysis/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   └── Zomato_Restaurant_Dataset.xlsx
├── notebooks/
│   └── zomato_analysis.ipynb
├── sql/
│   ├── 01_booking_delivery_vs_rating.sql
│   ├── 02_rating_by_price_tier.sql
│   ├── 03_vote_outliers.sql
│   └── 04_hidden_gems.sql
└── images/
    ├── rating_by_booking.png
    └── price_vs_rating.png
```

---

## How to Run

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/zomato-rating-engagement-analysis.git
cd zomato-rating-engagement-analysis

# 2. (Optional) create a virtual environment
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Launch the notebook
jupyter notebook notebooks/zomato_analysis.ipynb
```

The notebook builds a local SQLite database (`zomato.db`) from the Excel file. The `.sql` files in `sql/` can be run against it using any SQLite client or from the notebook.

---

## Limitations

- The data is **observational**, so findings show association, not causation.
- Confounders such as **city, cuisine and price tier** may influence the relationships.
- Ratings and votes reflect **self-selected** reviewers.
- [Add any dataset-specific limitation, e.g. snapshot date, missing values.]

---

## Author

**Aagam**
B.Tech (AI & ML), Ajay Kumar Garg Engineering College, Ghaziabad

[LinkedIn](#) · [GitHub](#) · [Email](#)
