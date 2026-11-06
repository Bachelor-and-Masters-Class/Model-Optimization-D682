# Baseline vs. Optimized Models

**WGU D684 · AI Optimization for Computer Scientists · Task 1**

Takes a model that isn't good enough, applies six improvement techniques one at a time, and ranks the results. Seed, data split and metrics stay the same for every version, so any change in score comes from the technique itself.

## The six versions

1. **Baseline:** logistic regression on an 80/20 split.
2. **Tuned:** automatic search for better settings, scored on F1.
3. **Better cutoff:** picks the yes/no cutoff that gives the best F1 on a separate validation set.
4. **Limited random forest:** caps tree depth and leaf size to avoid overfitting.
5. **Bagging:** averages many copies of the tuned model trained on random slices of the data.
6. **Stacking:** combines a random forest and gradient boosting through a third model.

## Output

- A results table, all models ranked by F1 (also shows accuracy, precision, recall and ROC AUC)
- A confusion matrix for each model
- A summary with the best settings found and the chosen cutoff

## Run it

```
python experiments/run_experiments.py              # classification
python experiments/run_experiments_regression.py   # regression
```

Use your own data with `DATA_CSV` and `TARGET_COL`. Results go to `reports/`.

## Files

- `experiments/`: the two experiment scripts
- `data/`: sample datasets
- `docs/Report_Template.docx`: written report for Task 1

**Built with:** Python, scikit-learn, pandas
