# Predicting Customer Repeat Purchase Behavior in E-Commerce

## Business Analytics Individual Case Study

**Student:** KHANDAVILLI V V S D GNANESH  
**Register Number:** CB.SC.U4CSE23662  
**Class / Section:** CSE G  
**Domain:** E-Commerce

---

## 1. Case Study Overview

### Title

**Predicting Customer Repeat Purchase Behavior in E-Commerce: A Data-Driven Approach to Retention Strategy**

### Business Problem

Online retailers need to understand which customer characteristics are associated with repeat purchasing instead of relying only on blanket discounting.

This case study analyzes survey-based customer information to examine behavioral, satisfaction-related, spending, and demographic factors associated with repeat purchase behavior. Classification models are developed to estimate repeat-purchase likelihood and assess whether the collected survey variables provide useful predictive signal.

The analysis is observational. Therefore, the results identify associations and predictive usefulness rather than causal effects.

---

## 2. Business Objectives

1. Identify behavioral, satisfaction-related, spending, and demographic factors associated with repeat purchase behavior.
2. Build and evaluate classification models to estimate the likelihood of repeat purchase.
3. Compare satisfaction-related factors against discount/spending-related factors using the same evaluation framework.
4. Translate the statistical and modeling results into actionable business insights and recommendations.

---

## 3. Data Collection

The dataset was collected through a **Google Forms questionnaire** designed for e-commerce shoppers.

The questionnaire captured:

- Demographic characteristics
- Shopping behavior
- E-commerce platform usage
- Delivery and product satisfaction
- Ease of use
- Return/refund issues
- Discount importance
- Spending-related information
- Repeat-purchase behavior

The dataset is primary survey data collected for this case study rather than a ready-made Kaggle, UCI, or GitHub dataset.

### Dataset Summary

| Item | Value |
|---|---:|
| Raw records | 11,401 |
| Columns | 13 |
| Duplicate rows removed | 5,242 |
| Rows after duplicate removal | 6,159 |
| Final unique shopper modeling population | 6,158 |
| Repeat purchase = Yes | 3,122 |
| Repeat purchase = No | 3,036 |
| Repeat purchase = Yes | 50.70% |
| Repeat purchase = No | 49.30% |

### Survey Skip Logic

The questionnaire uses skip logic.

In the raw workbook, respondents who had not shopped online during the previous six months did not receive the downstream shopper-specific questions. After exact duplicate removal, the unique dataset contains 6,158 shopper responses and one non-shopper record. The non-shopper record is excluded from the repeat-purchase modeling population by design.

The final cleaned modeling dataset therefore contains **6,158 unique shopper responses**.

---

## 4. Key Variables

The analysis considers variables covering:

- Monthly shopping frequency
- Most-used e-commerce platform
- Delivery satisfaction
- Product-match satisfaction
- Ease-of-use satisfaction
- Return/refund issue history
- Discount importance
- Age group
- Occupation
- Monthly spending capacity
- Average order value
- Repeat purchase behavior (target)

---

## 5. Data Preparation

The notebook performs the following preparation steps:

1. Loads the original Excel dataset from `data/raw_data.xlsx`.
2. Checks dataset dimensions, data types, missing values, and duplicate records.
3. Strips whitespace from text responses.
4. Removes exact duplicate rows.
5. Cleans and standardizes column names.
6. Applies the survey's shopper scope by retaining respondents who shopped online during the previous six months.
7. Saves the final cleaned modeling dataset to `data/cleaned_data.xlsx`.
8. Encodes the repeat-purchase target as a binary variable.
9. Separates predictor variables from the target.
10. Uses a stratified 80/20 train-test split.
11. Performs imputation and encoding inside scikit-learn pipelines.
12. Fits preprocessing steps within the appropriate training folds to avoid preprocessing leakage.

---

## 6. Exploratory and Statistical Analysis

The notebook includes:

- Target distribution analysis
- Categorical-variable distributions
- Repeat-purchase rate tables
- Satisfaction and discount comparisons
- Mann-Whitney U tests for ordinal survey variables
- Chi-square tests for categorical variables
- Cramér's V effect-size analysis
- Correlation/feature analysis where applicable
- Permutation importance for the Random Forest model

The statistical tests are used as exploratory evidence of association. They are **not interpreted as evidence of causation**.

For the collected sample, none of the eleven tested predictors reached statistical significance against the repeat-purchase target at the 5% level. The tested p-values ranged from **0.0825 to 1.0000**, and the observed categorical effect sizes were small, with Cramér's V values below **0.04**.

---

## 7. Analytics and Machine Learning

Two classification approaches are evaluated.

### Logistic Regression

Logistic Regression is used as an interpretable classification baseline for estimating repeat-purchase likelihood.

### Random Forest

Random Forest is used to capture possible nonlinear relationships and interactions among the survey variables.

### Evaluation Metrics

The models are evaluated using:

- Accuracy
- Precision
- Recall
- F1 Score
- ROC-AUC

A **majority-class baseline** is also calculated so that model performance is interpreted relative to a simple reference rather than accuracy alone.

---

## 8. Model Validation

The analysis uses:

- Stratified 80/20 train-test split
- 5-fold Stratified Cross-Validation
- Fixed random state: **42**

Preprocessing is implemented inside scikit-learn pipelines so that imputation, encoding, and scaling are learned without leaking information from validation/test data.

### 5-Fold Cross-Validation Results

| Model | CV Accuracy | CV F1 | CV ROC-AUC |
|---|---:|---:|---:|
| Majority-class baseline | 0.5070 ± 0.0003 | — | 0.5000 |
| Logistic Regression | 0.5036 ± 0.0073 | 0.5325 ± 0.0103 | 0.5040 ± 0.0116 |
| Random Forest | 0.5158 ± 0.0177 | 0.5307 ± 0.0211 | 0.5196 ± 0.0158 |

The results indicate that the current survey variables provide **limited predictive signal** for distinguishing repeat purchasers from non-repeat purchasers.

The Random Forest provides only a modest improvement over the majority-class baseline, while Logistic Regression remains close to the baseline.

---

## 9. Satisfaction vs. Discount/Spending Analysis

The original business problem proposed examining whether satisfaction-related information or discount/spending-related information provides useful predictive signal.

The notebook therefore evaluates separate feature groups using the same classification framework.

On the held-out split:

- **Satisfaction-only Logistic Regression:** ROC-AUC ≈ **0.517**
- **Discount/Spending-only Logistic Regression:** ROC-AUC ≈ **0.508**
- **Absolute ROC-AUC difference:** ≈ **0.009**

The corresponding held-out F1 scores are:

- Satisfaction-only: **0.5891**
- Discount/Spending-only: **0.5000**

This difference is reported descriptively and is **not interpreted as evidence that one feature group is a stronger causal driver** of repeat purchasing.

The broader cross-validation results indicate that overall predictive signal remains limited.

---

## 10. Business Insights

The analysis supports the following conclusions:

1. The collected survey variables provide limited predictive signal for reliable customer-level repeat-purchase targeting.
2. Statistical association tests do not provide sufficient evidence of significant relationships between the tested variables and repeat purchase at the 5% significance level.
3. The classification models perform close to the majority-class baseline when evaluated using cross-validation.
4. Satisfaction-only and discount/spending-only feature groups show a small difference on one held-out split, but this difference is not sufficient to establish a stable feature-group advantage.
5. The current analysis is more useful as a baseline assessment of the information contained in this survey than as a production-ready retention prediction system.

---

## 11. Business Recommendations

### 1. Collect transaction-level behavioral data

Future retention models should incorporate:

- Purchase recency
- Purchase frequency
- Monetary value
- Number of previous orders
- Customer tenure

### 2. Capture richer retention signals

Future data collection can include:

- Coupon usage
- Product returns
- Delivery delays
- Customer-support interactions
- Loyalty-program participation
- Reasons for repeat purchasing or switching

### 3. Avoid automated targeting with the current model

Because predictive performance is close to the majority-class baseline, the current model should not be treated as a production-ready customer-targeting system.

### 4. Use this study as a baseline

The current results can serve as a benchmark for future models that use richer behavioral and transaction-level data.

### 5. Improve future sampling

A larger and more diverse respondent population can help determine whether the weak relationships observed in this sample persist in broader e-commerce customer populations.

---

## 12. Comparison with Recent Published Studies

Three recent studies related to repeat-purchase/repurchase prediction in e-commerce were reviewed:

1. **Mauludiah, Arif, Faisal & Putra (2024)** — Logistic Regression and Random Forest on approximately 250,000 e-commerce transaction records.
2. **Duan & Hariyanto (2024)** — Logistic Regression, XGBoost and LightGBM using online-shopping transaction data.
3. **Yang (2026)** — Deep-learning and genetic-algorithm based repurchase prediction using larger behavioral/transactional datasets.

These studies use substantially different datasets and experimental settings from this survey-based case study. Therefore, their reported performance values are not treated as direct evidence that one approach is universally superior.

The comparison is instead used to understand differences in:

- Dataset size
- Transactional vs. survey-based information
- Feature richness
- Model complexity
- Evaluation methodology
- Predictive performance

---

## 13. Limitations

- The data is self-reported and may contain recall or response bias.
- The study uses an observational survey design and therefore does not establish causation.
- Survey respondents may not represent the complete population of e-commerce customers.
- Respondents who did not shop online in the previous six months are outside the repeat-purchase modeling population because of the questionnaire's skip logic.
- Model performance may change on a new customer population, platform mix, or future time period.
- The survey measures customer characteristics retrospectively, so the model should be treated as an analytical scoring exercise rather than a proven real-time intervention system.
- Several survey variables have relatively even response distributions across nearly every question. This may reflect the questionnaire design or respondent composition and should be considered when interpreting generalizability.

---

## 14. Project Structure

```text
ecommerce-repeat-purchase-analysis/
│
├── README.md
├── analysis.ipynb
├── Case_Study_Report.pdf
│
└── data/
    ├── raw_data.xlsx
    └── cleaned_data.xlsx
```

### Files

- **`README.md`** — Project overview, methodology, results, limitations, and business insights.
- **`analysis.ipynb`** — Complete data preparation, exploratory analysis, statistical testing, machine learning, evaluation, and interpretation.
- **`data/raw_data.xlsx`** — Original raw questionnaire dataset before data cleaning.
- **`data/cleaned_data.xlsx`** — Final cleaned dataset used for exploratory analysis, statistical testing, and machine-learning modeling.
- **`Case_Study_Report.pdf`** — Final Business Analytics case study report.

---

## 15. Reproducibility

The notebook is designed to run from the repository root.

### Raw dataset

The original source dataset should be located at:

```text
data/raw_data.xlsx
```

The notebook loads this file and performs the documented cleaning workflow.

### Cleaned dataset

The cleaning workflow produces:

```text
data/cleaned_data.xlsx
```

The final cleaned dataset contains **6,158 unique shopper responses** and is used for the subsequent analysis and modeling.

Then open `analysis.ipynb` in Jupyter Notebook or JupyterLab and use:

**Kernel → Restart Kernel and Run All Cells**

The notebook uses:

- Random state: **42**
- Stratified 80/20 train-test split
- 5-fold Stratified Cross-Validation

These settings are used to make the model evaluation reproducible.

---

## 16. Tools and Libraries

The analysis uses Python and the following major libraries:

- NumPy
- Pandas
- Matplotlib
- Seaborn
- Scikit-learn

Key scikit-learn components include:

- `train_test_split`
- `StratifiedKFold`
- `cross_validate`
- `ColumnTransformer`
- `Pipeline`
- `SimpleImputer`
- `OneHotEncoder`
- `StandardScaler`
- `LogisticRegression`
- `RandomForestClassifier`
- Classification metrics
- Permutation importance

---

## 17. References

### [1] Mauludiah et al. (2024)

Mauludiah, S. F., Arif, Y. M., Faisal, M., & Putra, D. D. (2024). *Struggling Models: An Analysis of Logistic Regression and Random Forest in Predicting Repeat Buyers with Imbalanced Performance Metrics*. Applied Information System and Management (AISM), 7(2), 31–38.

DOI: https://doi.org/10.15408/aism.v7i2.39326

### [2] Duan & Hariyanto (2024)

Duan, L., & Hariyanto, D. T. (2024). *Machine Learning Modeling for Forecasting Repeat Purchases in Online Shopping*. MALCOM: Indonesian Journal of Machine Learning and Computer Science, 4(3), 863–874.

DOI: https://doi.org/10.57152/malcom.v4i3.1388

### [3] Yang (2026)

Yang, S. (2026). *Predicting repurchase behavior and optimizing marketing for e-commerce users with genetic algorithms and deep learning*. Scientific Reports, 16, Article 16035.

DOI: https://doi.org/10.1038/s41598-026-45903-5

### [4] Scikit-learn

Pedregosa, F., Varoquaux, G., Gramfort, A., Michel, V., Grisel, O., Blondel, M., Prettenhofer, P., Weiss, R., Dubourg, V., Vanderplas, J., Passos, A., Cournapeau, D., Brucher, M., Perrot, M., & Duchesnay, É. (2011). *Scikit-learn: Machine Learning in Python*. Journal of Machine Learning Research, 12, 2825–2830.

---

## 18. Final Conclusion

The collected survey data provides limited statistical and predictive evidence for explaining or predicting repeat-purchase behavior using the measured survey variables.

Both classification models achieve performance close to the majority-class baseline under cross-validation, while the statistical tests do not provide sufficient evidence of significant relationships at the 5% level.

The study therefore serves as a documented baseline of the predictive information available in the collected survey and identifies the need for richer transaction-level and behavioral data for future customer-retention modeling.
