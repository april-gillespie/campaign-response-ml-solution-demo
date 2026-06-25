# 02 — Exploratory Data Analysis

Use this file as an instruction guide. The goal is to understand the data before modeling and produce a few useful observations that a business stakeholder could understand.

## Goal

Explore the relationship between customer/campaign features and campaign response. Do not try to prove causation. Look for patterns, data quality issues, class imbalance, and features that may be useful for prediction.

## Step 1: Reload data and define target

```python
import pandas as pd
import matplotlib.pyplot as plt
from pathlib import Path

DATA_PATH = Path("../data/raw/bank-additional-full.csv")
df = pd.read_csv(DATA_PATH, sep=";")

target = "y"
```

## Step 2: Plot target distribution

```python
df[target].value_counts().plot(kind="bar")
plt.title("Campaign Response Distribution")
plt.xlabel("Response")
plt.ylabel("Count")
plt.show()

response_rate = (df[target] == "yes").mean()
response_rate
```

Write:

> The positive response rate is approximately X%. This confirms that the project is an imbalanced classification problem.

## Step 3: Review numerical features

```python
numeric_cols = df.select_dtypes(exclude=["object"]).columns.tolist()
df[numeric_cols].describe().T
```

For each numerical feature, ask:

- What does it represent?
- Is the range reasonable?
- Are there outliers?
- Could this feature create data leakage?

Optional quick histograms:

```python
for col in numeric_cols:
    df[col].hist(bins=30)
    plt.title(f"Distribution of {col}")
    plt.xlabel(col)
    plt.ylabel("Count")
    plt.show()
```

## Step 4: Review categorical features

```python
categorical_cols = df.select_dtypes(include=["object"]).columns.tolist()

for col in categorical_cols:
    print("\n", col)
    print(df[col].value_counts().head(10))
```

For each categorical feature, ask:

- Are there many categories?
- Are any categories rare?
- Are there `unknown` values?
- Does the column need one-hot encoding?

## Step 5: Compare features against the target

Example for categorical response rates:

```python
feature = "job"
response_by_feature = (
    df.groupby(feature)[target]
    .apply(lambda x: (x == "yes").mean())
    .sort_values(ascending=False)
)
response_by_feature
```

Example plot:

```python
response_by_feature.plot(kind="bar")
plt.title(f"Response Rate by {feature}")
plt.ylabel("Response Rate")
plt.show()
```

Repeat for a few features that seem meaningful.

## Step 6: Write business observations

Write 3 to 5 observations in plain English.

Example format:

1. Customers with [feature/category] had a higher observed response rate, but this does not prove that the feature caused the response.
2. The target class is imbalanced, so model evaluation should include precision, recall, F1, and ROC-AUC.
3. Several features contain `unknown`, which may represent missing or unavailable customer information.

## Step 7: Decide what to carry into modeling

Create notes like:

- Features to include:
- Features to exclude:
- Features requiring encoding:
- Features requiring scaling:
- Data concerns to revisit later:

## Replace this guide with your findings

When finished, replace this guide with:

- Target distribution chart.
- Summary of important numerical features.
- Summary of important categorical features.
- 3 to 5 business-readable insights.
- Modeling decisions based on EDA.
