# 04 — Model Evaluation and Explainability

Use this file as an instruction guide. The goal is to compare your baseline model against one stronger model, then explain the tradeoffs clearly.

## Goal

Evaluate whether a comparison model improves on the logistic regression baseline. Then explain the result in plain English.

## Step 1: Train a comparison model

A random forest is a reasonable first comparison model.

```python
from sklearn.ensemble import RandomForestClassifier

comparison_model = Pipeline(steps=[
    ("preprocessor", preprocessor),
    ("model", RandomForestClassifier(
        n_estimators=200,
        random_state=42,
        class_weight="balanced",
        n_jobs=-1
    ))
])

comparison_model.fit(X_train, y_train)
```

## Step 2: Evaluate the comparison model

```python
y_pred_rf = comparison_model.predict(X_test)
y_proba_rf = comparison_model.predict_proba(X_test)[:, 1]

rf_metrics = {
    "accuracy": accuracy_score(y_test, y_pred_rf),
    "precision": precision_score(y_test, y_pred_rf),
    "recall": recall_score(y_test, y_pred_rf),
    "f1": f1_score(y_test, y_pred_rf),
    "roc_auc": roc_auc_score(y_test, y_proba_rf)
}

rf_metrics
```

## Step 3: Compare models

Create a table comparing logistic regression and random forest.

```python
results = pd.DataFrame([
    baseline_metrics,
    rf_metrics
], index=["Logistic Regression", "Random Forest"])

results
```

Update variable names as needed.

## Step 4: Choose the best model for the use case

Do not automatically choose the model with the highest accuracy. For an imbalanced classification problem, accuracy can hide weak performance on the smaller class.

Write your decision using this structure:

- Best model overall:
- Metric I prioritized:
- Why that metric matters:
- Main tradeoff:
- What I would test next:

Example:

> I prioritized recall because this use case values finding more likely positive responses. However, the tradeoff is that more false positives may be included. A pilot should compare model-assisted selection against the existing process before relying on the model.

## Step 5: Add basic explainability

For random forest, start with feature importance.

```python
preprocessor = comparison_model.named_steps["preprocessor"]
model = comparison_model.named_steps["model"]

categorical_features = preprocessor.named_transformers_["cat"].named_steps["onehot"].get_feature_names_out(categorical_cols)
all_features = list(numeric_cols) + list(categorical_features)

feature_importance = pd.DataFrame({
    "feature": all_features,
    "importance": model.feature_importances_
}).sort_values("importance", ascending=False)

feature_importance.head(20)
```

Plot top features:

```python
feature_importance.head(15).sort_values("importance").plot(
    kind="barh",
    x="feature",
    y="importance",
    legend=False
)
plt.title("Top Model Features")
plt.xlabel("Importance")
plt.ylabel("Feature")
plt.show()
```

## Step 6: Translate the model result

For each top feature, write:

- Technical feature name:
- Plain-English meaning:
- Why it may matter:
- Whether it would be available before the decision point:
- Any limitation or concern:

## Replace this guide with your findings

When finished, replace this guide with:

- Model comparison table.
- Explanation of your chosen metric.
- Feature importance chart.
- Plain-English interpretation.
- Recommendation for next steps.
