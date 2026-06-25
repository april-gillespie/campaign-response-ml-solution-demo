# Source Code Guide

This folder is optional for the first version of the project.

For the weekend version, it is completely acceptable to do the work in notebooks and keep this folder as a placeholder. If you later want to make the repo more polished, move reusable code into Python files here.

## Suggested future files

```text
src/
├── data_prep.py
├── train_model.py
├── evaluate_model.py
└── explain_model.py
```

## What belongs here

Use `src/` for reusable functions, not one-time notebook exploration.

Examples:

- Loading data.
- Cleaning columns.
- Splitting features and target.
- Creating preprocessing pipelines.
- Training models.
- Calculating evaluation metrics.
- Saving charts or result tables.

## Example function outline

```python
def load_bank_marketing_data(path):
    """Load the Bank Marketing dataset from a semicolon-separated CSV file."""
    import pandas as pd
    return pd.read_csv(path, sep=";")
```

## Good enough for version 1

For the first version, focus on finishing the analysis. Do not over-engineer the code structure before you have results.

A strong first version has:

- Clear notebook flow.
- Clean README.
- Metrics table.
- Stakeholder summary.
- Responsible AI notes.

A more polished second version can move repeated code here.
