# Disease Prediction: Confusion Matrix, Precision, Recall and F1

A Google Colab notebook with two parts:

- **Part A:** the numerical question from the lecture slide (200 patients, 80 diseased, 70 caught, 20 false alarms).
- **Part B:** preprocessing and classification on the Breast Cancer Wisconsin (Diagnostic) dataset, with accuracy, precision, recall, F1 and plots.

## Run it

1. Open `disease_prediction_metrics.ipynb` in Google Colab.
2. Runtime > Run all. The notebook downloads the data with `kagglehub` (Kaggle: `uciml/breast-cancer-wisconsin-data`).
3. Figures are saved in `visualizations/`.

## Part A: slide answer

|                    | Predicted diseased | Predicted healthy |
|--------------------|-------------------:|------------------:|
| **Actually diseased** | TP = 70 | FN = 10 |
| **Actually healthy**  | FP = 20 | TN = 100 |

| Metric    | Formula                | Value |
|-----------|------------------------|------:|
| Accuracy  | (TP + TN) / total      | 0.850 |
| Precision | TP / (TP + FP)         | 0.778 |
| Recall    | TP / (TP + FN)         | 0.875 |
| F1-score  | 2PR / (P + R)          | 0.824 |

## Part B: preprocessing

- Dropped the `id` column and the empty `Unnamed: 32` column
- Checked missing values and duplicates (none found)
- Encoded the target: malignant = 1, benign = 0
- Stratified 80/20 train-test split
- Feature scaling inside the pipeline (fitted on training data only)

## Part B: test-set results (sample run)

| Model               | Accuracy | Precision | Recall | F1    |
|---------------------|---------:|----------:|-------:|------:|
| Logistic Regression | 0.965    | 0.975     | 0.929  | 0.951 |
| Random Forest       | 0.974    | 1.000     | 0.929  | 0.963 |

Model choice uses cross-validated F1 on the training data, not the test score.
These numbers come from a run on the scikit-learn copy of the same UCI data. A Colab run with the Kaggle file may differ slightly.

## Files

- `disease_prediction_metrics.ipynb`: the notebook
- `visualizations/`: confusion matrices, class balance, correlations, metric comparison, ROC curves, `model_results.csv`
