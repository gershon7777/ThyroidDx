# ThyroidDx

ThyroidDx is a supervised machine learning project focused on the classification of thyroid disorders
using clinical history and laboratory measurements. The project is based on a well-known thyroid
disease dataset commonly used in data mining research.

---
 ## Quickstart

**Google Colab**
1. Open `ThyroidDx.ipynb` in Colab
2. Run the dataset upload cell and upload `thyroid0387.csv`
3. Run all cells top to bottom
4. Loading the Dataset in Google Colab When running this notebook in Google Colab, the dataset must be uploaded manually using the
Colab file upload widget.

The following code cell is responsible for loading the dataset:

    "from google.colab import files uploaded = files.upload() 
    file_name = list(uploaded.keys())[0] 
    df = pd.read_csv(file_name)"
    
5. Run the cell. --> Click “Choose Files” when prompted. --> Upload the dataset file:thyroid0387.csv
Done, all the code should run. 

Once uploaded, the file is saved in the Colab session and automatically loaded into a pandas
DataFrame.

After successful upload, the notebook will display a confirmation message indicating that the file
has been loaded correctly.

---

## Dataset Description

The dataset used in this project originates from the **UCI Thyroid Disease dataset**, a benchmark
dataset designed for evaluating classification algorithms in medical decision-making.

The data consists of demographic information, hormone measurements (TSH, T3, TT4, T4U, FTI),
medication status, medical history, and clinician-assigned diagnostic labels. Missing values are
present in several laboratory features and are handled during preprocessing.



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

Data preprocessing included handling missing values, feature selection, and train–test splitting.
Several supervised learning models were trained and evaluated to compare predictive performance and
interpretability.

The following models were implemented:

- Dummy Classifier (baseline)
- Logistic Regression
- Decision Tree (CART)
- Random Forest

---
  
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


**Model Comparison**

| Model               | Performance  | Strengths                             | Limitations                 |
| ------------------- | ------------ | ------------------------------------- | --------------------------- |
| Dummy Classifier    | Very low     | Baseline reference only               | No clinical relevance       |
| Logistic Regression | Moderate     | Simple, stable, interpretable         | Limited non-linear modeling |
| Decision Tree       | Good         | High interpretability, clinical logic | Prone to overfitting        |
| Random Forest       | Best overall | Higher accuracy, robust predictions   | Reduced interpretability    |

The Dummy Classifier served as a minimal baseline and performed poorly, confirming that meaningful learning is required.

Logistic Regression improved over baseline but remained limited by its linear decision boundary, which is often insufficient for complex endocrine relationships and interactions between clinical features.

The Decision Tree (CART) model provided strong performance while remaining interpretable. Its rule-based structure is useful for clinical-style reasoning, but single trees can be sensitive to noise and may overfit, especially when classes overlap or when missingness is not uniform across features.

The Random Forest model achieved the best overall predictive performance. This is expected because a Random Forest combines many decision trees (an ensemble) and aggregates their predictions. Compared to a single CART tree, the ensemble reduces variance and improves generalization, particularly in noisy clinical datasets. The trade-off is reduced interpretability, since the final prediction is produced by many trees rather than a single transparent rule set.

Misclassifications occurred primarily among clinically overlapping diagnostic categories, reflecting real-world diagnostic ambiguity rather than purely algorithmic error.

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

Class imbalance is present across diagnostic categories. However, this imbalance is not necessarily a flaw: in real-world medicine, most people are not hyperthyroid or hypothyroid, so a dataset where “healthy / non-disease” patterns are more common can reflect realistic population prevalence. In that sense, the dataset provides a useful approximation of real clinical distribution.

At the same time, imbalance can still affect model behavior and evaluation. Models may learn to prioritize majority classes, and minority classes may show reduced recall. For this reason, performance should be interpreted with attention to class-wise metrics and confusion matrices, not accuracy alone.

Additional limitations include missing laboratory values in a subset of records, retrospective design, and lack of external validation. The models in this repository are for educational and research portfolio purposes and are not intended for clinical deployment.


---

## Clinical Framing and Future Work

Clinical practice does not rely only on a final diagnosis label. It uses structured reasoning: symptoms, risk factors, pre-test probability, and guideline-driven follow-up testing. In the notebook, we also explored a clinically oriented framing inspired by decision-support resources (e.g., AMBOSS-style logic), with the goal of moving beyond pure pattern recognition toward guideline-compatible reasoning.

A future extension of this project is to combine supervised learning with clinical guideline logic, for example:
- integrating structured rules or decision pathways alongside ML predictions,
- improving interpretability by mapping model signals to clinically meaningful thresholds,
- and evaluating whether guideline-aware modeling reduces unsafe or clinically implausible predictions.

We also introduced a “pre-lab risk score” concept, where a simplified model would estimate risk using pre-laboratory information (history and clinical context) before confirmatory hormone testing. This mirrors real clinical workflow: early triage and probability estimation before ordering definitive tests. A future version of the notebook can implement this as a separate model trained on pre-lab features only and compare its performance to full-lab models.

---

## Files in This Repository
  File	Description
- ThyroidDx.ipynb	Main analysis notebook containing preprocessing, modeling, and evaluation
  
- thyroid0387.csv	Thyroid disease dataset
  
- README.md	Project documentation
