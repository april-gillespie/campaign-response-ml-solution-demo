# Responsible AI Review Template

Replace this template with your final responsible AI / deployment considerations section.

## Purpose

This review explains what would need to be considered before using the model in a real business workflow.

## Intended use

Describe what the model is meant to support.

Example:

> The model is intended to support campaign planning by estimating likelihood of a positive response based on historical campaign data.

## Not intended for

Describe what the model should not be used for.

Example:

> The model should not be used as the only basis for excluding people from outreach, making financial eligibility decisions, or making decisions outside the campaign context represented by the dataset.

## Data limitations

Answer:

- How old is the dataset?
- Is the dataset from one organization or context?
- Would the patterns generalize to a different business, country, or time period?
- Are there missing or `unknown` values?
- Are all features available before the decision point?

Your notes:

> [Replace with your findings.]

## Model limitations

Answer:

- Which metric was strongest?
- Which metric was weakest?
- How does class imbalance affect the result?
- What kinds of mistakes does the model make?
- What additional testing would be required?

Your notes:

> [Replace with your findings.]

## Feature concerns

Review the top model features.

| Feature | Plain-English meaning | Available before decision? | Concern |
|---|---|---|---|
| TBD | TBD | TBD | TBD |

Questions to ask:

- Does this feature represent information known only after contact?
- Could this feature encode sensitive or proxy information?
- Could this feature change over time?
- Could using this feature create unfair or undesirable outcomes?

## Human oversight

Describe how a person should review or use model output.

Example:

> Model predictions should be used as one input into planning, not as an automatic decision. A human reviewer should understand the threshold, expected error rates, and operational tradeoffs.

## Monitoring plan

If this were piloted, what would need to be monitored?

- Precision over time:
- Recall over time:
- Data drift:
- Feature availability:
- User feedback:
- Business outcome:

## Deployment recommendation

Choose and explain one:

- Do not deploy.
- Pilot with constraints.
- Deploy after additional validation.

Final recommendation:

> [Replace with your recommendation.]

## Summary

End with 3 to 5 sentences showing mature judgment.

Example:

> The model may be useful as a decision-support tool, but the current project is a demonstration rather than a production-ready system. Before deployment, the business would need newer validation data, a clear threshold policy, human review, and monitoring for performance drift. This review shows that model performance alone is not enough; responsible implementation also requires context, process design, and governance.
