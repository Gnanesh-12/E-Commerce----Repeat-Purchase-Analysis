# Predicting Customer Repeat Purchase Behavior in E-Commerce

## Business Analytics Individual Case Study

**Student:** KHANDAVILLI V V S D GNANESH\
**Register Number:** CB.SC.U4CSE23662\
**Class/Section:** CSE G\
**Domain:** E-Commerce

------------------------------------------------------------------------

## 1. Case Study Title

**Predicting Customer Repeat Purchase Behavior in E-Commerce: A
Data-Driven Approach to Retention Strategy**

------------------------------------------------------------------------

## 2. Business Problem

Online retailers need to understand which customer characteristics are
associated with repeat purchasing instead of relying only on blanket
discounting.

This case study analyzes survey-based customer information to examine
behavioral, satisfaction-related, spending, and demographic factors
associated with repeat purchase behavior. Classification models are also
developed to estimate repeat-purchase likelihood and to assess whether
the collected survey variables provide useful predictive signal.

The analysis is observational. Therefore, the results identify
associations and predictive usefulness rather than causal effects.

------------------------------------------------------------------------

## 3. Business Objectives

1.  Identify behavioral, satisfaction-related, spending, and demographic
    factors associated with repeat purchase behavior.
2.  Build classification models to estimate the likelihood of repeat
    purchase.
3.  Compare satisfaction-related factors with discount/spending-related
    factors using the same evaluation framework.
4.  Translate the statistical and modeling results into actionable
    business insights.

------------------------------------------------------------------------

## 4. Data Collection and Dataset

### Data Collection Method

The dataset was collected through a **Google Forms questionnaire**
designed for e-commerce shoppers. The questionnaire captured demographic
characteristics, shopping behavior, satisfaction factors,
spending-related information, and repeat-purchase behavior.

The dataset is primary survey data collected for this case study rather
than a ready-made Kaggle, UCI, or GitHub dataset.

### Dataset Summary

-   **Raw records:** 11,401
-   **Columns:** 14, including the timestamp
-   **Duplicate records:** 1 exact duplicate
-   **Final modeling population:** 6,161 shoppers
-   **Target:** Repeat purchase (`Yes` / `No`)
-   **Target distribution:** approximately 50.72% Yes and 49.28% No

The questionnaire uses skip logic. Respondents who did not shop online
during the previous six months did not receive the downstream shopper
questions. Therefore, these respondents are excluded from the
repeat-purchase modeling population rather than being treated as
ordinary missing-value observations.

------------------------------------------------------------------------

## 5. Key Variables

The analysis considers variables covering:

-   Monthly shopping frequency
-   E-commerce platform
-   Delivery satisfaction
-   Product-match satisfaction
-   Ease-of-use satisfaction
-   Return-related issues
-   Discount importance
-   Age group
-   Occupation
-   Monthly spending capacity
-   Average order value
-   Repeat purchase behavior

------------------------------------------------------------------------

## 6. Data Preparation

The notebook performs the following preparation steps:

1.  Loads the Excel dataset from the repository's `data/` directory.
2.  Checks dataset dimensions, data types, missing values, and duplicate
    records.
3.  Removes exact duplicate rows.
4.  Cleans and standardizes column names.
5.  Applies the survey's shopper scope by retaining respondents who
    shopped online during the previous six months.
6.  Encodes the repeat-purchase target as a binary variable.
7.  Separates predictor variables from the target.
8.  Uses train/test splitting with stratification.
9.  Performs imputation and encoding within scikit-learn pipelines to
    avoid preprocessing leakage.

------------------------------------------------------------------------

## 7. Exploratory and Statistical Analysis

The notebook includes:

-   Target distribution analysis
-   Categorical-variable distributions
-   Repeat-purchase rate tables
-   Satisfaction and discount comparisons
-   Mann--Whitney U tests for ordinal survey variables
-   Chi-square tests for categorical variables
-   Cramér's V effect-size analysis

The statistical tests are used as exploratory evidence of association.
They are not interpreted as evidence of causation.

For the collected sample, the tested variables do not provide sufficient
evidence of statistically significant association with repeat purchase
at the 5% significance level, and the observed categorical effect sizes
are small.

------------------------------------------------------------------------

## 8. Analytics and Machine Learning

Two classification approaches are evaluated:

### Logistic Regression

Logistic Regression is used as an interpretable classification baseline
for estimating repeat-purchase likelihood.

### Random Forest

Random Forest is used to capture possible nonlinear relationships and
interactions among the survey variables.

### Evaluation Metrics

The models are evaluated using:

-   Accuracy
-   Precision
-   Recall
-   F1 Score
-   ROC-AUC

A **majority-class baseline** is also calculated so that model
performance is interpreted relative to a simple reference rather than
accuracy alone.

------------------------------------------------------------------------

## 9. Cross-Validation

A **5-fold Stratified Cross-Validation** procedure is applied to the
full feature set.

The final notebook reports approximately:

  Model                   CV Accuracy   CV ROC-AUC
  --------------------- ------------- ------------
  Logistic Regression           0.501        0.506
  Random Forest                 0.509        0.516

The majority-class baseline accuracy is approximately **0.507**.

These results indicate that the current survey variables provide limited
predictive signal for distinguishing repeat purchasers from non-repeat
purchasers.

------------------------------------------------------------------------

## 10. Satisfaction vs. Discount/Spending Analysis

The original business problem proposed examining whether
satisfaction-related information or discount/spending-related
information provides useful predictive signal.

The notebook therefore evaluates separate feature groups using the same
classification framework.

On the held-out split:

-   Satisfaction-only Logistic Regression: ROC-AUC ≈ **0.528**
-   Discount/Spending-only Logistic Regression: ROC-AUC ≈ **0.504**
-   Absolute ROC-AUC difference: ≈ **0.025**

This difference is reported descriptively and is **not interpreted as
proof that satisfaction is a stronger causal driver** of repeat
purchasing. The broader cross-validation results indicate that overall
predictive signal remains limited.

------------------------------------------------------------------------

## 11. Business Insights

The analysis supports the following conclusions:

1.  The collected survey variables do not provide sufficient predictive
    signal for reliable customer-level repeat-purchase targeting.
2.  Statistical association tests do not provide sufficient evidence of
    significant relationships between the tested variables and repeat
    purchase at the 5% significance level.
3.  The classification models perform close to the majority-class
    baseline when evaluated using cross-validation.
4.  The satisfaction and discount/spending feature groups show a small
    difference on one held-out split, but this difference is not
    sufficient to establish a stable feature-group advantage.
5.  The current analysis is therefore more useful as a baseline
    assessment than as a production-ready retention prediction system.

------------------------------------------------------------------------

## 12. Business Recommendations

### 1. Collect transaction-level behavioral data

Future retention models should incorporate:

-   Purchase recency
-   Purchase frequency
-   Monetary value
-   Number of previous orders
-   Customer tenure

### 2. Capture richer retention signals

Future data collection can include:

-   Coupon usage
-   Product returns
-   Delivery delays
-   Customer-support interactions
-   Loyalty-program participation
-   Reasons for repeat purchasing or switching

### 3. Avoid automated targeting with the current model

Because predictive performance is close to the baseline, the current
model should not be treated as a production-ready customer targeting
system.

### 4. Use this study as a baseline

The current results can serve as a benchmark for future models that use
richer behavioral and transaction-level data.

### 5. Improve future sampling

A larger and more diverse respondent population can help determine
whether the weak relationships observed in this sample persist in
broader e-commerce customer populations.

------------------------------------------------------------------------

## 13. Limitations

-   The data is self-reported and may contain recall or response bias.
-   The study uses an observational survey design and therefore does not
    establish causation.
-   Survey respondents may not represent the complete population of
    e-commerce customers.
-   Respondents who did not shop online in the previous six months are
    outside the repeat-purchase modeling population because of the
    questionnaire's skip logic.
-   Model performance may change on a new customer population, platform
    mix, or future time period.
-   The survey measures customer characteristics retrospectively, so the
    model should be treated as an analytical scoring exercise rather
    than a proven real-time intervention system.
-   Several survey variables have relatively even response
    distributions; this may reflect the questionnaire design or
    respondent composition and should be considered when interpreting
    generalizability.

------------------------------------------------------------------------

## 14. Project Structure

``` text
ecommerce-repeat-purchase-analysis/
│
├── README.md
├── analysis.ipynb
├── Case_Study_Report.pdf
│
└── data/
    └── E-Commerce Survey.xlsx
```

### Files

-   **`README.md`** --- Project overview, methodology, results, and
    business insights.
-   **`analysis.ipynb`** --- Complete data preparation, exploratory
    analysis, statistical testing, machine learning, evaluation, and
    interpretation.
-   **`data/E-Commerce Survey.xlsx`** --- Primary survey dataset used
    for the analysis.
-   **`Case_Study_Report.pdf`** --- Final case study report following
    the prescribed Business Analytics report format.

------------------------------------------------------------------------

## 15. Reproducibility

The notebook is designed to run from the repository root.

Ensure the dataset is located at:

``` text
data/E-Commerce Survey.xlsx
```

Then open `analysis.ipynb` in Jupyter Notebook or JupyterLab and use:

**Kernel → Restart Kernel and Run All Cells**

The notebook uses a fixed random state of **42** and a stratified 80/20
train-test split for reproducible model evaluation.

------------------------------------------------------------------------

## 16. Tools and Libraries

The analysis uses Python and the following major libraries:

-   NumPy
-   Pandas
-   Matplotlib
-   Seaborn
-   Scikit-learn

Key scikit-learn components include:

-   `train_test_split`
-   `StratifiedKFold`
-   `cross_validate`
-   `ColumnTransformer`
-   `Pipeline`
-   `SimpleImputer`
-   `OneHotEncoder`
-   `StandardScaler`
-   `LogisticRegression`
-   `RandomForestClassifier`
-   Classification metrics
-   Permutation importance

------------------------------------------------------------------------

## 17. References

The final case study report contains the detailed references and the
required comparison with at least three recent published studies related
to repeat purchase/customer retention analytics.

Methodology and software documentation used in the notebook should be
cited in the final report where appropriate.

------------------------------------------------------------------------

## 18. Final Conclusion

The collected survey data does not provide sufficient statistical or
predictive evidence to reliably explain or predict repeat purchase
behavior using the measured survey variables.

The classification models achieve performance close to the
majority-class baseline under cross-validation. Therefore, the current
model should not be treated as a production-ready retention targeting
system.

The study instead provides a baseline understanding of the predictive
information available in the collected survey and identifies the need
for richer transaction-level and behavioral data for future
customer-retention modeling.
