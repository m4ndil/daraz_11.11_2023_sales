# 11.11 Sale 2023 — Top Selling Product Data

> **Dataset file:** `/mnt/data/Top_Selling_Product_Data.csv`

---

## Overview

This repository contains the **Top Selling Product Data** collected for the **11.11 Sale 2023**. The dataset captures product-level and seller-level information for items that performed strongly during the sale event. The file included in this project is located at the path above — use it directly for analysis or transform it into a public URL if you want to share the CSV from this repo.

**Quick facts**

* **Rows (instances):** 12,907
* **Columns (features):** 15
* **CSV path (local):** `/mnt/data/Top_Selling_Product_Data.csv`

---

## Table of Contents

1. [Dataset description](#dataset-description)
2. [Columns / Data dictionary](#columns--data-dictionary)
3. [Quick start (load & inspect)](#quick-start-load--inspect)
4. [Suggested cleaning & feature engineering](#suggested-cleaning--feature-engineering)
5. [Exploratory analyses & visualizations](#exploratory-analyses--visualizations)
6. [Modelling ideas](#modelling-ideas)
7. [Reproducible examples (Pandas)](#reproducible-examples-pandas)
8. [License & attribution](#license--attribution)
9. [Contact / Maintainer](#contact--maintainer)

---

## Dataset description

Each row represents a top-selling product record observed in the 11.11 Sale 2023 dataset. The dataset includes product metadata (category, title), price information (original and discount prices), seller performance metrics (ratings, ship-on-time, chat response), delivery & store flags, and estimated sales volume information.

This dataset is suitable for descriptive analytics (category and price trends), seller performance studies, and predictive tasks (demand forecasting, sales classification), provided that a target variable is defined or derived.

---

## Columns / Data dictionary

Below are the column names and short descriptions (as discovered from the CSV):

1. `Category` — Product top-level category (string)
2. `SubCategory` — Product subcategory (string)
3. `Title` — Product title / name (string)
4. `Original Price` — Original listed price before discount (integer)
5. `Discount Price` — Price after discount (integer)
6. `Discount` — Discount value or amount (float)
7. `Seller Name` — Seller display name (string)
8. `Number of Ratings` — Total number of product ratings (integer)
9. `Positive Seller Ratings` — Count of positive seller ratings (integer)
10. `Ship On Time` — Ship-on-time percentage or metric (integer)
11. `Chat Response Rate` — Rate of chat response/engagement (integer)
12. `Delivery Type` — Delivery method / options (string)
13. `Flagship Store` — Flagship store indicator (string / categorical)
14. `No. of products to be sold` — Estimated number of units to be sold (numeric)
15. `Sell percentage to increase` — Percentage increase target to reach a sales goal (integer)

> **Note:** All columns appear to be fully populated for the dataset snapshot included; however, always verify for missing values after loading into your environment.

---

## Quick start (load & inspect)

### Prerequisites

* Python 3.8+
* pandas

### Example (local path)

```python
import pandas as pd

# adjust path if you move the CSV into the repository root or a public URL
csv_path = "/mnt/data/Top_Selling_Product_Data.csv"

df = pd.read_csv(csv_path)
print(df.shape)
print(df.columns.tolist())
print(df.head())
```

### Basic checks

* `df.info()` — verify dtypes and non-null counts
* `df.describe()` — get numeric summaries
* `df['Category'].value_counts().head()` — inspect top categories

---

## Suggested cleaning & feature engineering

1. **Normalize categorical labels** — strip whitespace, unify case, and fix typos in `Category` and `SubCategory`.
2. **Type conversions** — convert `No. of products to be sold` to integer if all values are whole numbers.
3. **Compute derived features**:

   * `price_drop = Original Price - Discount Price`
   * `discount_percent = (price_drop / Original Price) * 100`
   * `positive_rating_ratio = Positive Seller Ratings / Number of Ratings` (handle division by zero)
4. **Date/time** — if you merge with time-series data later, ensure sale timestamps are present or merged.
5. **Outlier checks** — look for unrealistic prices, ratings, or estimated sales values.

---

## Exploratory analyses & visualizations

Suggested plots and analyses to perform:

* Histogram of `Discount Price` and `price_drop` to inspect price distributions and discount depth.
* Boxplots of `discount_percent` grouped by `Category` to find categories offering deepest discounts.
* Bar charts of top `Seller Name` by number of listed products and average `Sell percentage to increase`.
* Scatter plots of `No. of products to be sold` vs. `Discount Price` or `discount_percent` to inspect price-demand relationships.
* Heatmap of correlations between numeric features (prices, ratings, ship on time, chat response).

---

## Modelling ideas

* **Regression:** predict `No. of products to be sold` using price, discount, and seller metrics.
* **Classification:** binary target for whether a product sells above a threshold (e.g., top 10% of sold units).
* **Clustering / segmentation:** group products by pricing and seller quality to identify market segments.
* **Time-series / panel models:** if you align items across multiple sale events, model demand dynamics.

---

## Reproducible examples (Pandas + scikit-learn snippet)

```python
# Basic feature engineering
df['price_drop'] = df['Original Price'] - df['Discount Price']

df['discount_percent'] = df['price_drop'] / df['Original Price'] * 100

df['positive_rating_ratio'] = df['Positive Seller Ratings'] / df['Number of Ratings'].replace(0, pd.NA)

# Example: simple regression target
# from sklearn.model_selection import train_test_split
# from sklearn.ensemble import RandomForestRegressor

# features = ['Discount Price', 'discount_percent', 'positive_rating_ratio', 'Ship On Time', 'Chat Response Rate']
# X = df[features].fillna(0)
# y = df['No. of products to be sold']
# X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
# model = RandomForestRegressor(n_estimators=100, random_state=42).fit(X_train, y_train)
```

---

## License & attribution

Specify an appropriate license for this dataset and repository. If this data is proprietary or sensitive, include access controls. Example licenses:

* CC BY 4.0 — allow reuse with attribution
* MIT — permissive for code, not dataset content

*Add a `LICENSE` file to the repo with the chosen license.*

---

## Contact / Maintainer

If you have questions about the dataset or need additional processing, contact the maintainer listed in this repository (or open an issue).

---

*Generated README — use this as the baseline documentation for working with the 11.11 Sale 2023 top-selling product data.*
