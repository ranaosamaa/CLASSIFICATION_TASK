# Diabetes Classification Project

This project is a machine learning classification workflow for predicting diabetes outcomes using a structured medical dataset. It includes exploratory data analysis, feature engineering, dimensionality reduction, and several classification models with hyperparameter tuning.

## Repository Contents

- `diabetes_prediction_dataset.csv` — Primary dataset used for model training and evaluation.
- `FINAL_ML_DIABETES_PRED.ipynb` — Final notebook version with polished analysis and results.
- `Features_version2.ipynb` — Additional notebook for feature experiments and alternative model workflows.
- `CHANGELOG.md` — Project history and changelog.

## Project Overview

The notebooks cover:

- Data loading and initial cleaning
- Exploratory data analysis (EDA) with visualizations
- Feature engineering and encoding
- Train/test splitting with stratified sampling
- Standard scaling and PCA for models that benefit from it
- Model training with randomized hyperparameter search
- Model evaluation using F1 score, precision, recall, accuracy, ROC AUC, and confusion matrices
- Comparison of model performance and PCA impact

## Models Included

- Multi-Layer Perceptron (MLP)
- Random Forest Classifier
- Gradient Boosting Classifier
- Support Vector Machine (SVM) with linear and RBF kernels
- Logistic Regression (placeholder/experimentation)
- Gaussian Naive Bayes (placeholder/experimentation)

## Dependencies

The notebooks use the following Python libraries:

- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- imbalanced-learn
- scipy

Install dependencies with pip:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn scipy
```

## Usage

1. Open the notebook files in Jupyter or VS Code:
   - `FINAL_ML_DIABETES_PRED.ipynb`

2. Run cells sequentially to reproduce the analysis.


## Notes

- `OrganizedNotebook.ipynb` is the most complete pipeline and includes cross-validated hyperparameter searches and model comparison.
- The dataset is expected to be in the same directory as the notebooks.
- If you need to reproduce results in a fresh environment, create a new Python virtual environment before installing dependencies.

## License

This repository does not currently include a license file. Add one if you intend to share or publish the project publicly.
