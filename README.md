# ThyroidDx

ThyroidDx is a supervised machine learning project focused on the classification of thyroid disorders
using clinical history and laboratory measurements. The project is based on a well-known thyroid
disease dataset commonly used in data mining research.

---

## Dataset Description

The dataset used in this project originates from the **UCI Thyroid Disease dataset**, a benchmark
dataset designed for evaluating classification algorithms in medical decision-making.

### General Characteristics

| Property | Description |
|--------|------------|
| Domain | Endocrinology (thyroid disorders) |
| Data type | Tabular, structured clinical data |
| Records | ~3,700 patient cases |
| Features | Clinical history, laboratory values, treatment indicators |
| Target variable | Thyroid diagnosis (categorical) |
| Missing values | Present in several laboratory features |

### Feature Categories

The dataset contains a mixture of feature types:

| Feature group | Examples |
|-------------|----------|
| Demographic | Age |
| Laboratory values | TSH, T3, TT4, T4U, FTI |
| Medication status | On thyroxine, on antithyroid medication |
| Medical history | Thyroid surgery, I-131 treatment |
| Clinical queries | Query hypothyroid, query hyperthyroid |

---

### Hyperthyroid Conditions

| Code | Diagnosis |
|----|----------|
| A | Hyperthyroid |
| B | T3 toxic |
| C | Toxic goitre |
| D | Secondary toxic |

### Hypothyroid Conditions

| Code | Diagnosis |
|----|----------|
| E | Hypothyroid |
| F | Primary hypothyroid |
| G | Compensated hypothyroid |
| H | Secondary hypothyroid |

### Binding Protein Disorders

| Code | Diagnosis |
|----|----------|
| I | Increased binding protein |
| J | Decreased binding protein |

### General Health Status

| Code | Diagnosis |
|----|----------|
| K | Concurrent non-thyroidal illness |

### Replacement Therapy Status

| Code | Diagnosis |
|----|----------|
| L | Consistent with replacement therapy |
| M | Underreplaced |
| N | Overreplaced |

### Antithyroid Treatment

| Code | Diagnosis |
|----|----------|
| O | Antithyroid drugs |
| P | I-131 treatment |
| Q | Surgery |

### Miscellaneous Conditions

| Code | Diagnosis |
|----|----------|
| R | Discordant assay results |
| S | Elevated TBG |
| T | Elevated thyroid hormones |

---

### Diagnostic Grouping Used in Prior Experiments

According to the original dataset documentation, earlier experiments focused on
deriving decision trees for the most frequent and clinically relevant diagnostic groups:

- **Hyperthyroid conditions** (A, B, C, D)
- **Hypothyroid conditions** (E, F, G, H)
- **Binding protein disorders** (I, J)
- **General health status** (K)
- **Replacement therapy status** (L, M, N)
- **Discordant results** (R)

These groupings reflect clinically meaningful categories and informed the design of
classification experiments in this project.

---

## Methodology

### Data Preprocessing
- Removal of records with excessive missing values
- Handling of remaining missing values using standard preprocessing techniques
- Separation of features and target diagnosis labels
- Train–test split for supervised learning

  ---

### Supervised Learning Models

**Models Implemented**

Several supervised learning models were trained and evaluated to assess their suitability for
thyroid disease classification. The models were selected to represent increasing levels of
complexity and clinical interpretability.

| Model                | Purpose      | Key Characteristics                                    |
| -------------------- | ------------ | ------------------------------------------------------ |
| Dummy Classifier     | Baseline     | Predicts the most frequent class only                  |
| Logistic Regression  | Linear model | Probabilistic, interpretable, linear decision boundary |
| Decision Tree (CART) | Tree-based   | Rule-based, interpretable, non-linear                  |
| Random Forest        | Ensemble     | Multiple trees, improved generalization                |


**Model Comparison (Qualitative)**

| Model               | Performance  | Strengths                             | Limitations                 |
| ------------------- | ------------ | ------------------------------------- | --------------------------- |
| Dummy Classifier    | Very low     | Baseline reference only               | No clinical relevance       |
| Logistic Regression | Moderate     | Simple, stable, interpretable         | Limited non-linear modeling |
| Decision Tree       | Good         | High interpretability, clinical logic | Prone to overfitting        |
| Random Forest       | Best overall | Higher accuracy, robust predictions   | Reduced interpretability    |

The Dummy Classifier served as a minimal baseline, confirming that meaningful learning was
achieved by all subsequent models.
Logistic Regression improved performance over baseline but showed limitations in handling
complex, non-linear relationships common in endocrine data.
The Decision Tree classifier achieved strong performance while maintaining interpretability,
making it particularly suitable for clinical reasoning and educational purposes.
The Random Forest model demonstrated the best overall predictive performance, benefiting from
ensemble learning and reduced variance, at the cost of reduced transparency.

Across all models:

Performance improved consistently from baseline to ensemble methods

Tree-based models outperformed linear models

Misclassifications were most common among clinically overlapping diagnoses

Observed errors reflected real-world diagnostic ambiguity rather than model failure

Confusion matrices and classification reports in the notebooks illustrate class-wise behavior and
highlight areas of diagnostic overlap.

---

## Conclusion

This project demonstrates that supervised machine learning models can effectively classify thyroid
disease states using structured clinical and laboratory data.

Simple baselines are insufficient for medical classification

Interpretable models (Decision Trees) offer a strong balance between performance and clinical insight

Ensemble methods (Random Forests) provide the highest accuracy but reduced explainability

The results emphasize the importance of balancing predictive performance with interpretability in
medical AI applications.

## Limitations

Class imbalance across diagnostic categories

Missing laboratory values in a subset of records

No external validation dataset

Retrospective data only

Models not intended for clinical deployment

---

## Files in This Repository
- File	Description
- ThyroidDx.ipynb	Main analysis notebook containing preprocessing, modeling, and evaluation
= thyroid0387.csv	Thyroid disease dataset
= README.md	Project documentation
