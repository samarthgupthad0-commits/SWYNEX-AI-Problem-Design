# SWYNEX AI Problem Design: Employee Request Triage

## Problem

HR teams receive short employee requests about workplace processes. Sorting each request into the right queue takes time and can delay a response. This project proposes a small AI classifier that assigns a request to one of four queues: **Leave**, **Payroll**, **Benefits**, or **IT Support**. It helps HR triage incoming messages; it does not make decisions about employees.

## User

The primary user is an HR or operations coordinator who reviews incoming employee requests. Employees benefit from faster routing. A coordinator remains responsible for checking the suggested category and handling the request.

## Data source and scope

Use a small, manually reviewed dataset of short, fictional employee request messages labeled with one of the four categories. Start with 80–200 examples, with roughly balanced categories. The examples can be written for this exercise or drawn from approved, anonymized examples if the organization provides them. Do not use real names, contact details, medical information, salary details, or other identifying information.

Split the examples into training and test sets before modeling (for example, 80% / 20%). Keep near-duplicate phrasings in the same split so the test set measures generalization rather than memorization. Record the label definitions and dataset limitations alongside the examples.

## Proposed approach

Build a baseline text classifier using TF-IDF features and logistic regression. For a new message, return the predicted queue and confidence. If confidence is below a chosen threshold, mark it **Needs human review** instead of presenting a confident category. A simple keyword baseline can be included for comparison.

## Constraints and safeguards

- The model only recommends a queue; it must not approve leave, determine payroll, assess performance, or make other employment decisions.
- Use fictional or explicitly approved anonymized data. Store no employee identifiers in the experiment dataset.
- Do not infer sensitive attributes or use them as model inputs.
- Show the human reviewer the original message and the suggested category; allow correction.
- Treat low-confidence and out-of-scope messages as human review cases.
- The small dataset is a prototype and may not represent real message variety or language use.

## Success criteria and evaluation

Evaluate on the held-out test set. Report accuracy, macro F1, and a confusion matrix so performance on each queue is visible. Compare against the keyword baseline.

The prototype is successful if:

1. Macro F1 is at least **0.80** on the held-out set.
2. No category has recall below **0.70**.
3. At least **90%** of predictions marked high-confidence are correct; uncertain cases should be routed to human review.
4. The report includes errors, class counts, the split method, and limitations.

These are initial targets for a small demonstration dataset, not a claim of production readiness. If the dataset is too small to support these thresholds, report the measured results and the evidence needed before deployment rather than tuning on the test set.

## Deliverables

- This problem definition and success criteria.
- A small fictional, labeled dataset or a documented approved data source.
- A reproducible baseline classifier and evaluation summary.
- A short demo showing the suggested queue and human-review behavior.

