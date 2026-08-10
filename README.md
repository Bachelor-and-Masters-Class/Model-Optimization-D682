**Overview**

This repository contains my completed submission for **Task 1** of the WGU course **D684: AI Optimization for Computer Scientists**.

The task requires demonstrating measurable improvement to an underperforming machine learning model and justifying each optimization decision with evidence. The implementation is a scripted experiment suite that trains a fixed baseline, applies six distinct optimization strategies, and produces a ranked comparison of all variants under identical evaluation conditions.

**Scenario**

An organization has an existing predictive model that is not meeting performance requirements. The assignment is to diagnose the shortfall, apply appropriate optimization techniques, and deliver both the improved model and a written report explaining which techniques worked, which did not, and why.

The experiment is designed so that the effect of each technique is isolated. The random seed, the train/test split, and the evaluation metric set are held constant across every variant, so that any change in score is attributable to the optimization applied rather than to sampling variance.

**Project Objectives**

-Train and document a reproducible baseline model

-Apply hyperparameter tuning through automated search

-Optimize the classification decision threshold using a dedicated validation split

-Evaluate constrained tree-based models as an alternative to linear regularization

-Test bagging and stacking ensemble strategies

-Rank all variants on a common metric and export supporting evidence

-Support both classification and regression problem framings

**Experimental Design**

**Baseline**
A standardized L2-regularized logistic regression, fit on a stratified 80/20 split.

**Tuned Model**
RandomizedSearchCV over penalty type, regularization strength, elastic net mixing ratio, and class weighting, scored on F1 with stratified cross-validation.

**Threshold-Optimized Model**
The tuned model is refit on a training subset, evaluated across a range of candidate decision thresholds on a held-out validation split, and the F1-maximizing threshold is carried forward to test evaluation.

**Constrained Random Forest**
A depth-limited forest with a minimum leaf size constraint, evaluating whether structural regularization outperforms coefficient regularization on this data.

**Bagging Ensemble**
Bootstrap aggregation over the tuned logistic regression with row and feature subsampling, targeting variance reduction.

**Stacked Ensemble**
Random forest and gradient boosting base learners combined through a logistic regression meta-learner, testing whether model diversity outperforms any single tuned model.

**Evaluation and Outputs**

All variants are scored on accuracy, precision, recall, F1, and ROC AUC against the same held-out test set. The experiment writes:

-A comparison table of all models ranked by F1 score

-A confusion matrix export for each model variant

-A summary file recording the best hyperparameters found, the selected decision threshold, and the final model ranking

**Skills Demonstrated**

-Controlled experimental design for model optimization

-Automated hyperparameter search with cross-validation

-Decision threshold tuning and its effect on precision-recall tradeoffs

-Regularization strategy comparison across model families

-Ensemble learning: bagging, boosting, and stacking

-Multi-metric evaluation and model ranking

-Reproducibility through seed control and fixed splits

-Automated reporting for technical documentation

**How to Run**

Classification track:

```
python experiments/run_experiments.py
```

Regression track:

```
python experiments/run_experiments_regression.py
```

Dataset and target column can be overridden through the DATA_CSV and TARGET_COL environment variables. All outputs are written to a reports directory.

**Repository Contents**

-`experiments/run_experiments.py`: Classification optimization experiment suite

-`experiments/run_experiments_regression.py`: Regression optimization experiment suite

-`data/demo_classification.csv`: Classification dataset

-`data/demo_regression.csv`: Regression dataset

-`docs/Report_Template.docx`: Written report deliverable for Task 1
