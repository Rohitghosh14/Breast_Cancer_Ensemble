# Breast Cancer: bagging practice project

A learning project. It predicts whether a tumor is malignant (cancer) or benign, from 30 measurements of a cell sample (scikit-learn's built-in Breast Cancer Wisconsin data, 569 patients). The goal was to understand cross-validation and bagging with an honest comparison.

**This is a practice project. It must not be used for real medical decisions.**

## Method
- Cancer is labelled `1` (212 patients, 37%), benign `0`, so recall measures how many cancers we catch
- Stratified 80/20 split: 455 train, 114 test (the test set was locked until the end)
- All models compared with the same 5 stratified folds on train only
- Noise rule: noise = std / sqrt(5). A gap smaller than the noise is a tie, and among tied models the simpler one wins

## Comparison (5-fold CV on train)
| Model | Accuracy | Recall (cancer) | Recall noise | F1 | Fit time (s) |
|---|---|---|---|---|---|
| Logistic Regression | 0.9736 | 0.9529 | 0.0178 | 0.9640 | 0.02 |
| Random Forest (200 trees) | 0.9626 | 0.9353 | 0.0174 | 0.9489 | 0.58 |
| Decision tree (no limit) | 0.9231 | 0.8941 | 0.0271 | 0.8962 | 0.01 |

The forest (bagging) clearly beats one tree, but it is tied with Logistic Regression on recall, so the simpler Logistic Regression was chosen.

## Final result (test set, 114 patients, tested once)
39 of 42 cancers caught, 3 missed, 1 false alarm. Recall 0.93, precision 0.97, accuracy 0.96.

## Limitations
- The test set is small: one cancer is about 2.4 points of recall, so the result is only a rough estimate
- 3 cancers were missed, which would matter a lot in real life
- Only one dataset and three models were compared, so the conclusion is about this dataset

## Run it
`uv sync`, then open `notebooks/01_breast_cancer.ipynb` and run all cells.

## Credits
Learning project, built step by step with an AI tutor (Claude). I ran and checked the code myself.