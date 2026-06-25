# Project Checklist

Use this checklist to keep the project scoped and finishable. The goal is not to make the most advanced model. The goal is to demonstrate an end-to-end AI solutions workflow.

## Phase 1: Setup

- [ ] Download the UCI Bank Marketing dataset manually.
- [ ] Save the raw files locally under `data/raw/`.
- [ ] Confirm the target column. For this dataset, the target is typically whether the client subscribed to a term deposit.
- [ ] Create a working notebook from the markdown guide files in `notebooks/`.
- [ ] Install dependencies from `requirements.txt`.

Example note to add when done:

> Dataset downloaded on YYYY-MM-DD from the UCI Machine Learning Repository. Raw data stored locally and excluded from GitHub. Target variable identified as `y`, representing whether the customer subscribed to the offer.

## Phase 2: Business framing

- [ ] Write the business question in plain English.
- [ ] Define who would use the model.
- [ ] Define what action the model might support.
- [ ] Define what a false positive means.
- [ ] Define what a false negative means.

Example:

> A false positive means the model predicts a customer will respond, but they do not. In a campaign setting, this may waste outreach effort or budget. A false negative means the model misses a customer who would have responded, causing a missed revenue opportunity.

## Phase 3: Data review

- [ ] Load the dataset into pandas.
- [ ] Check rows, columns, data types, missing values, and duplicates.
- [ ] Review categorical vs numerical features.
- [ ] Check class balance for the target variable.
- [ ] Decide which columns should be excluded before modeling, if any.

## Phase 4: Exploratory data analysis

- [ ] Plot target class balance.
- [ ] Summarize numerical variables.
- [ ] Summarize categorical variables.
- [ ] Look for obvious patterns related to campaign response.
- [ ] Write 3 to 5 plain-English observations.

## Phase 5: Baseline model

- [ ] Split the data into training and test sets.
- [ ] Build a preprocessing pipeline.
- [ ] Train a logistic regression baseline.
- [ ] Evaluate accuracy, precision, recall, F1, and ROC-AUC.
- [ ] Explain why accuracy alone may be misleading.

## Phase 6: Comparison model

- [ ] Train a second model, such as random forest or gradient boosting.
- [ ] Compare it to the logistic regression baseline.
- [ ] Decide which model is better for the business use case.
- [ ] Explain the tradeoff between precision and recall.

## Phase 7: Explainability

- [ ] Add feature importance or another explanation method.
- [ ] Identify the top model drivers.
- [ ] Translate technical drivers into business language.
- [ ] Note any features that could raise ethical or operational concerns.

## Phase 8: Stakeholder summary

- [ ] Complete `reports/stakeholder_summary_template.md`.
- [ ] Include the business question, model result, recommendation, and next steps.
- [ ] Avoid overstating what the model can do.
- [ ] Use a tone suitable for a non-technical manager.

## Phase 9: Responsible AI review

- [ ] Complete `reports/responsible_ai_review_template.md`.
- [ ] Discuss data limitations.
- [ ] Discuss potential bias or misuse.
- [ ] Discuss monitoring and retraining.
- [ ] Make a deployment recommendation: deploy, pilot, or do not deploy.

## Done definition

The project is complete when a reader can understand:

- What problem you solved.
- What data you used.
- What model you trained.
- How well it performed.
- What the model can and cannot be trusted to do.
- How you would explain the result to a business stakeholder.
