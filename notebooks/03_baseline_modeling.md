# 03 — Baseline Modeling

Use this file as an instruction guide. The goal is to build a simple, explainable baseline model before trying a stronger model.

## Goal

Train a logistic regression baseline model that predicts campaign response. Use preprocessing pipelines so the project looks clean and reproducible.

## Step 1: Import modeling libraries

```python
import pandas as pd
import numpy as np

from pathlib import Path
from sklearn.model_selection import train_test_split
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import OneHotEncoder, StandardScaler
from sklearn.pipeline import Pipeline
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score, roc_auc_score, confusion_matrix, classification_report
```

## Step 2: Load data and split features/target

```python
DATA_PATH = Path("../data/raw/bank-additional-full.csv")
df = pd.read_csv(DATA_PATH, sep=";")

X = df.drop(columns=["y"])
y = df["y"].map({"no": 0, "yes": 1})
```

## Step 3: Identify column types

```python
categorical_cols = X.select_dtypes(include=["object"]).columns.tolist()
numeric_cols = X.select_dtypes(exclude=["object"]).columns.tolist()
```

## Step 4: Train/test split

Use stratification because the target class is likely imbalanced.

```python
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42,
    stratify=y
)
```

## Step 5: Build preprocessing and model pipeline

```python
numeric_transformer = Pipeline(steps=[
    ("scaler", StandardScaler())
])

categorical_transformer = Pipeline(steps=[
    ("onehot", OneHotEncoder(handle_unknown="ignore"))
])

preprocessor = ColumnTransformer(
    transformers=[
        ("num", numeric_transformer, numeric_cols),
        ("cat", categorical_transformer, categorical_cols)
    ]
)

baseline_model = Pipeline(steps=[
    ("preprocessor", preprocessor),
    ("model", LogisticRegression(max_iter=1000, class_weight="balanced"))
])
```

## Step 6: Train the model

```python
baseline_model.fit(X_train, y_train)
```

## Step 7: Evaluate the model

```python
y_pred = baseline_model.predict(X_test)
y_proba = baseline_model.predict_proba(X_test)[:, 1]

metrics = {
    "accuracy": accuracy_score(y_test, y_pred),
    "precision": precision_score(y_test, y_pred),
    "recall": recall_score(y_test, y_pred),
    "f1": f1_score(y_test, y_pred),
    "roc_auc": roc_auc_score(y_test, y_proba)
}

metrics
```

Also print:

```python
print(confusion_matrix(y_test, y_pred))
print(classification_report(y_test, y_pred))
```

## Step 8: Interpret the baseline

Write a short paragraph:

- What did the model do well?
- Where did it struggle?
- Was precision or recall more important for this use case?
- Is the model useful enough to compare against a stronger model?

Example:

> The logistic regression baseline provides a transparent starting point. Because the dataset is imbalanced, accuracy is not enough to judge performance. For a campaign targeting use case, recall may matter if the business wants to avoid missing likely responders, while precision may matter if outreach cost or customer annoyance is high.

## Step 9: Save baseline results

Create a small metrics table you can reuse in the final report.

Example:

```python
baseline_results = pd.DataFrame([metrics], index=["Logistic Regression Baseline"])
baseline_results
```

## Replace this guide with your findings

When finished, replace this guide with:

- Model setup summary.
- Metrics table.
- Confusion matrix.
- Business interpretation of false positives and false negatives.
- Decision on what to try next.
