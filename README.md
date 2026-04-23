# Prediction of Kidney Disease Stages Using Data Mining Algorithms

This repository contains a Jupyter notebook that explores chronic kidney disease prediction with several machine learning models and compares them on the same dataset.

It is based on the paper included in this repo, `Prediction of kidney disease stages using data mining algorithms.pdf`, and the main working notebook is `project_notebook.ipynb`.

## What Is In This Repo

- `project_notebook.ipynb` - end-to-end notebook for loading, cleaning, training, and evaluating the models.
- `Data/data.csv` - the kidney disease dataset used by the notebook.
- `Prediction of kidney disease stages using data mining algorithms.pdf` - the reference paper for the project.

## Project Goal

The notebook compares multiple classifiers for kidney disease classification and reports standard evaluation metrics on a held-out test set. The workflow is:

1. Load the CSV dataset.
2. Drop the `id` column.
3. Replace `?` placeholders with missing values.
4. Encode categorical columns.
5. Fill numeric missing values with the column mean.
6. Split the data into train, validation, and test sets.
7. Train and compare several algorithms.
8. Print a results table and plot the metrics.

## Dataset Snapshot

The dataset currently included in this repo has:

- 400 rows
- 26 columns
- a target column named `classification`

Important feature groups include:

- Demographics: `age`, `bp`
- Kidney function / lab values: `sg`, `al`, `su`, `bgr`, `bu`, `sc`, `sod`, `pot`, `hemo`, `pcv`, `wc`, `rc`
- Categorical clinical indicators: `rbc`, `pc`, `pcc`, `ba`, `htn`, `dm`, `cad`, `appet`, `pe`, `ane`

Note: the raw CSV contains `?` placeholders and some whitespace-variant values in the class labels, so preprocessing is required before modeling.

## Models Compared

The notebook trains and evaluates these models:

- Multilayer Perceptron (MLP)
- Support Vector Machine (SVM)
- Radial Basis Function network approximation
- Probabilistic Neural Network (implemented with Gaussian Naive Bayes in the notebook)

## Current Notebook Results

The following values are produced by the current notebook logic on the included
dataset:

| Algorithm | Accuracy | Precision | Recall | F1 Score |
| --- | ---: | ---: | ---: | ---: |
| MLP | 0.85 | 0.69 | 1.00 | 0.82 |
| SVM | 0.67 | 0.00 | 0.00 | 0.00 |
| RBF | 0.50 | 0.27 | 0.30 | 0.29 |
| PNN | 0.93 | 0.90 | 0.90 | 0.90 |

Small but important note: the notebook currently computes `precision_score`, `recall_score`, and `f1_score` with `pos_label=2`. Because the target column is label-encoded directly, that positive label corresponds to the encoded `notckd` class in the current CSV. If you normalize the labels first, those scores may change.

## How To Run

1. Install the Python dependencies:

   ```bash
   pip install numpy pandas matplotlib seaborn scikit-learn jupyter
   ```

2. Open `project_notebook.ipynb` in Jupyter Lab, Jupyter Notebook, or VS Code.
3. Run the cells from top to bottom.

## Reproducibility Notes

- The notebook uses a 70/15/15 train/validation/test split with `random_state=42`.
- The last heatmap cell references `df_metrics`, which is not defined in the notebook as committed. If you want that plot, you will need to build `df_metrics` from the `results_table` first.
- `StandardScaler` is imported but not used in the current notebook.

## Suggested Improvements

- Clean the class labels before encoding so `ckd` variants are merged.
- Add a reusable preprocessing pipeline.
- Save the metrics table and plots as notebook outputs or standalone figures.
- Add a small script or function wrapper so the experiments can be rerun more easily outside the notebook.

## Reference

- El-Houssainy A. Rady, Ayman S. Anwar *Prediction of kidney disease stages using data mining algorithms* (2019). The paper PDF is included in the repository for context.

