# Data Folder Guide

Use this folder for local dataset organization. Do not commit raw downloaded data unless you intentionally confirm the license and file size are appropriate for GitHub.

Recommended local structure:

```text
data/
├── README.md
├── raw/
│   └── bank-additional-full.csv
└── processed/
    └── cleaned_bank_marketing.csv
```

## What to do

1. Download the Bank Marketing dataset directly from the UCI Machine Learning Repository.
2. Save the original file in `data/raw/`.
3. Keep the raw file unchanged.
4. If you clean or transform the data, save that output in `data/processed/`.
5. In your notebook, clearly document which file you loaded.

## Why this matters

Keeping raw and processed data separate makes the project easier to review. It also shows good data hygiene, which matters in real AI and analytics workflows.

## Suggested dataset notes to fill in

Replace this section after downloading the data.

- Dataset name:
- Source:
- Download date:
- File name used:
- Number of rows:
- Number of columns:
- Target column:
- Target meaning:
- Known limitations:

Example:

> The target column is `y`, which indicates whether the customer subscribed to a term deposit after the campaign. This project treats `yes` as the positive class.

## Important caution

Some columns may describe campaign contact behavior rather than stable customer traits. Before presenting the project, think about whether the model is predicting customer interest, campaign execution quality, or both.
