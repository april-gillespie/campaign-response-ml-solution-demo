# 01 — Project Setup and Data Review

Use this file as an instruction guide. When you do the work, create a Jupyter notebook or Python script based on these steps, then replace this guide with your actual findings or link to the completed notebook.

## Goal

Load the UCI Bank Marketing dataset, understand its structure, identify the target variable, and write the business problem in a way that a non-technical stakeholder can understand.

## Step 1: Create the business framing

Write 2 to 4 sentences answering:

- What decision could this model support?
- Who would use the prediction?
- What action might they take based on the prediction?
- What should they not assume from the prediction?

Example:

> This project evaluates whether historical campaign data can help predict which customers are likely to respond to a marketing campaign. A sales or marketing operations team could use the model to prioritize outreach, but the model should support human decision-making rather than automatically excluding customers.

## Step 2: Import core libraries

Example starter code:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

from pathlib import Path
```

## Step 3: Load the data

Update the path to match your actual downloaded file.

```python
DATA_PATH = Path("../data/raw/bank-additional-full.csv")

df = pd.read_csv(DATA_PATH, sep=";")
df.head()
```

If the file does not load correctly, check:

- Is the separator semicolon instead of comma?
- Did you download the ZIP and extract the CSV?
- Is the file path correct relative to your notebook location?

## Step 4: Inspect the dataset

Run:

```python
df.shape
df.info()
df.describe(include="all")
df.isna().sum().sort_values(ascending=False).head(20)
df.duplicated().sum()
```

Write notes like:

- Number of rows:
- Number of columns:
- Missing values:
- Duplicate rows:
- Target column:
- Positive class:

## Step 5: Confirm the target variable

The target is likely `y`.

```python
df["y"].value_counts()
df["y"].value_counts(normalize=True)
```

Write a plain-English interpretation:

> The target is imbalanced: only X% of customers responded positively. This means accuracy alone may be misleading, because a model could appear accurate by mostly predicting the majority class.

## Step 6: Identify feature types

```python
categorical_cols = df.select_dtypes(include=["object"]).columns.tolist()
numeric_cols = df.select_dtypes(exclude=["object"]).columns.tolist()

categorical_cols, numeric_cols
```

Note whether the target column appears in categorical columns. If so, remove it from the feature list before modeling.

## Step 7: Early risk notes

Before modeling, answer:

- Are there columns that could leak information from after the campaign result?
- Are there sensitive or proxy variables?
- Are there operational variables that might change over time?
- Would this dataset generalize to another bank, country, or decade?

## Replace this guide with your findings

When finished, replace this guide with:

1. A short setup summary.
2. The dataset shape.
3. The target distribution.
4. Any data quality issues.
5. Initial risks or limitations.
