# Sex-Stratified Classification of Metabolic Syndrome in the Amol Cohort

This repository contains the code used for sex-stratified classification of prevalent metabolic syndrome in the Amol cohort.

The workflow includes data cleaning, sex-stratified preprocessing, multicollinearity assessment using VIF, nested cross-validation, hyperparameter tuning, and comprehensive model evaluation.

## Repository Contents

- `Shahinfar.github.codes-Copy1.ipynb`  
  Main Jupyter Notebook containing the full analysis pipeline.

## Study Outcome

The target variable is `MetS_ATPIII`, and sex is encoded as:

- `Female = 0`
- `Male = 1`

## Data and Predictors

The analysis uses demographic, clinical, biochemical, lifestyle, and dietary predictors from the Amol cohort.

The predictor set includes variables such as:

- Age
- CVD history
- Blood lipid and liver enzyme markers
- CRP
- Renal function markers
- Vitamin D
- Family history
- Blood-pressure-related variables
- Heart disease and diabetes indicators
- Smoking and alcohol use
- Physical activity (`MET`)
- Residential area
- Macronutrient percentages
- Fiber intake
- Dietary pattern variables

Categorical predictors include variables related to:

- CVD history
- Family history
- Blood pressure
- Heart disease
- Diabetes
- Smoking
- Alcohol use
- Residential area

## Preprocessing

The notebook performs data cleaning by converting blank or nonnumeric values to missing values (`NaN`).

A sex-stratified KNN imputation procedure is implemented in the notebook:

- The data are grouped by sex
- Missing values are temporarily handled to allow scaling
- Predictors are standardized using `StandardScaler`
- `KNNImputer` with `n_neighbors = 5` is applied
- Imputed values are transformed back to the original scale
- Categorical variables are rounded and converted back to integer form

## Multicollinearity Assessment

Variance Inflation Factor (VIF) is used to assess multicollinearity among predictors.

The notebook includes:

- Fast VIF calculation based on the inverse correlation matrix
- Exact VIF calculation using `statsmodels`
- Standardization before VIF calculation
- A configurable threshold for reporting multicollinearity

## Validation Strategy

The modeling framework is based on nested stratified cross-validation:

- `INNER_FOLDS = 5`
- `OUTER_FOLDS = 5`
- `RANDOM_STATE = 42`

The inner loop is used for hyperparameter selection, and the outer loop is used for model performance estimation.

## Hyperparameter Tuning

The notebook defines a hyperparameter grid for model selection.  
For Logistic Regression, the regularization parameter `C` is searched over:
```python
[0.001, 0.01, 0.1, 1.0, 10.0, 100.0]
Evaluation Metrics
The notebook computes a comprehensive set of performance metrics, including:

Accuracy
Precision
Recall
F1-score
Matthews correlation coefficient
Cohen’s kappa
Hamming loss
Jaccard index
Sensitivity
Specificity
Positive predictive value (PPV)
Negative predictive value (NPV)
Youden index
Balanced accuracy
Error rate
ROC-AUC
Log loss
Brier score
Confusion matrix counts
Train and test ROC-AUC values are also compared to provide a simple indication of potential overfitting.

Data Availability
The original participant-level data are not included in this repository due to privacy and access restrictions.

Reproducibility Notes
The notebook contains local file paths that should be replaced with relative paths before public release.
Raw data files and generated imputed datasets should not be shared publicly.
A .gitignore file is recommended to exclude raw data, temporary outputs, and local artifacts.
Requirements
Install the required Python packages with:

bash
pip install -r requirements.txt
Citation
If you use this code, please cite the associated manuscript and dataset according to the publication details.