# CHANGELOG — ML_DIABETES_PREDICTION_ORGANIZED.ipynb

## Created from: `ML_DIABETES_PREDICTION.ipynb` (commit `0a834dd` — "fixed pca")

---

## Conflicts Resolved

### 1. Double CSV Load (cells 2 & 3)
**Problem**: Both cell 2 and cell 3 loaded `pd.read_csv('diabetes_prediction_dataset.csv')`, one was a leftover Google Colab path.  
**Fix**: Kept a single `pd.read_csv()` call.

### 2. MLP vs RF Used Different Preprocessing Pipelines
**Problem**: MLP trained on `X_train_pca` (PCA-transformed data), while Random Forest built its own internal `ColumnTransformer` pipeline with `SimpleImputer + StandardScaler + OneHotEncoder` — running completely different preprocessing than MLP.  
**Fix**: Created a shared data split section. Each model section now clearly states whether it uses PCA data or raw features. Tree models (RF, GB) use raw features directly. MLP uses PCA-transformed data.

### 3. RF's Redundant Internal Pipeline
**Problem**: RF cell created its own `numeric_transformer` (SimpleImputer + StandardScaler) and `categorical_transformer` (SimpleImputer + OneHotEncoder), but after feature engineering there are NO categorical features left (gender was already one-hot encoded, smoking was ordinally mapped) and NO nulls. The entire ColumnTransformer was a no-op except StandardScaler, which trees don't need.  
**Fix**: Removed RF's internal pipeline. RF now trains directly on raw `X_train` since tree-based models are scale-invariant.

### 4. SMOTE Created But Never Used
**Problem**: Cell 37 created `X_train_smote, y_train_smote` via `SMOTE(random_state=42)`, but neither MLP nor RF actually used the SMOTE data. Both trained on non-SMOTE data.  
**Fix**: Removed SMOTE entirely. Models handle class imbalance via `class_weight='balanced'` (RF) or threshold tuning.

### 5. Missing `stratify=y` in Train/Test Split
**Problem**: Original `train_test_split()` calls did NOT use `stratify=y`. With ~91.5%/8.5% class imbalance, this risks uneven class distribution across splits.  
**Fix**: Added `stratify=y` to `train_test_split()`.

### 6. Empty Cell 57
**Problem**: Cell 57 was completely empty.  
**Fix**: Removed.

---

## Pipeline Changes

| Aspect | Original Notebook | Organized Notebook |
|--------|------------------|-------------------|
| Data split | 70/15/15 (train/val/test), no stratify | **80/20 (train/test), stratified** |
| Validation | Fixed 15% validation set | **StratifiedKFold(5) CV during search** |
| SMOTE | Created but unused | **Removed** |
| PCA | Applied to all data | **Available for models that need it** |
| Preprocessing | Each model had its own pipeline | **Shared split; each model uses appropriate data** |
| Class imbalance | Not addressed | **class_weight='balanced' + threshold tuning** |

---

## Models

| Model | Status | Data Used | Notes |
|-------|--------|-----------|-------|
| MLP | ✅ Implemented | PCA | `RandomizedSearchCV(n_iter=20, cv=5, scoring='f1')` |
| Random Forest | ✅ Rewritten | Raw features | Simplified — removed redundant internal pipeline |
| Gradient Boosting | ✅ NEW | Raw features | Hyperparams from `not.ipynb` grid |
| Logistic Regression | 📝 Placeholder | — | To be implemented by team member |
| Naive Bayes | 📝 Placeholder | — | To be implemented by team member |
| SVM (Linear + Kernel) | 📝 Placeholder | — | PSO + GridSearch required per task |

---

## New Sections Added

- **Helper Functions**: `find_best_threshold()` — shared threshold tuning utility
- **Model Comparison**: Summary table + bar chart comparing all trained models
- **PCA vs Non-PCA Comparison**: Side-by-side graphs comparing performance with/without PCA
- **Learning Curves**: For each implemented model (MLP, RF, GB)

---

## Task Description Compliance

| Requirement | Status |
|------------|--------|
| EDA + visualization | ✅ Preserved from original |
| Preprocessing | ✅ Scaling, encoding, feature engineering |
| PCA vs without PCA | ✅ Both paths available + comparison section |
| Train/validation/test split | ✅ 80/20 + StratifiedKFold(5) CV |
| Logistic Regression | 📝 Placeholder ready |
| MLP | ✅ Implemented |
| SVM (Linear + Kernels) | 📝 Placeholder ready (with PSO note) |
| Naive Bayes | 📝 Placeholder ready |
| Two Ensemble algorithms | ✅ Random Forest + Gradient Boosting |
| Confusion matrix + metrics | ✅ For all implemented models |
| Best model selection | ✅ Comparison section |
| Learning curves | ✅ For all implemented models |
