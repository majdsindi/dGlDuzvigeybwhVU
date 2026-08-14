# Customer Happiness Prediction & Survey Feature Optimization

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458.svg)](https://pandas.pydata.org/)
[![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Machine%20Learning-F7931E.svg)](https://scikit-learn.org/)
[![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/majdsindi/dGlDuzvigeybwhVU/blob/main/happiness_predict.ipynb)

An end-to-end data science and machine learning project built to predict customer satisfaction/happiness ($Y$) based on survey feedback ($X_1$ to $X_6$) from ACME's delivery service, identifying the most critical survey questions to optimize customer experience while minimizing survey fatigue.

---

## 📌 1. Summary of the Project

ACME Inc. collects feedback from customers regarding their delivery experience through a 6-question survey evaluated on a 5-point Likert scale (1 = Unsatisfied, 5 = Highly Satisfied). The primary objective of this project is twofold:
1. **Predictive Modeling:** Build a binary classification model that accurately predicts customer happiness ($Y = 1$ for Happy, $Y = 0$ for Unhappy) with a target accuracy threshold of **> 73%**.
2. **Feature Optimization & Survey Streamlining:** Identify the minimal, most impactful set of survey questions needed to predict satisfaction, allowing ACME to shorten the survey, improve response rates, and focus operational improvements on key customer value drivers.

### Dataset Overview
* **Total Survey Responses:** 126 customer records
* **Target Variable ($Y$):** Binary Customer Happiness status ($1 = \text{Happy}$, $0 = \text{Unhappy}$; Mean: $0.548$, ~54.8% happy class balance).
* **Feature Set ($X_1$ to $X_6$):**
  * `X1`: *"My order was delivered on time"* (Mean: 4.33, Max: 5.0)
  * `X2`: *"Contents of my order was as I expected"* (Mean: 2.53, Max: 5.0)
  * `X3`: *"I ordered everything I wanted to order"* (Mean: 3.31, Max: 5.0)
  * `X4`: *"I paid a good price for my order"* (Mean: 3.75, Max: 5.0)
  * `X5`: *"I am satisfied with my courier"* (Mean: 3.65, Max: 5.0)
  * `X6`: *"The app makes ordering easy for me"* (Mean: 4.25, Max: 5.0)

---

## 🛠️ 2. Methodology

The workflow follows an iterative Data Science process from Exploratory Data Analysis (EDA) to Model Selection and Feature Selection:

### A. Exploratory Data Analysis (EDA)
* **Distribution & Bivariate Analysis:** Examined feature distributions and stacked bar charts across all rating levels (1–5) grouped by customer happiness ($Y$).
* **Key Insights:**
  * `X1` (On-time delivery) and `X6` (App ease-of-use) show high baseline ratings (means $> 4.2$), indicating strong overall delivery efficiency and user interface satisfaction.
  * `X2` (Expected contents) exhibits significantly lower customer scores (mean $= 2.53$), highlighting a potential operational vulnerability in order accuracy or expectations management.
  * `X5` (Courier satisfaction) and `X1` (On-time delivery) demonstrate strong visual separation between happy ($Y=1$) and unhappy ($Y=0$) customer cohorts.

### B. Feature Selection & Engineering Strategies
To discover the minimal subset of features without sacrificing model predictive power:
1. **Full Feature Baseline:** Modeling with all six features ($X_1$–$X_6$).
2. **Feature Importance Ranking:** Utilizing Tree-based feature importances (Random Forest, Extra Trees, Gradient Boosting).
3. **Subset Optimization:** Evaluating reduced feature combinations ($k=2, 3, 4$) to balance model simplicity and high performance.
4. **Key Feature Drivers:** Identifying `X1` (On-time delivery) and `X5` (Courier satisfaction) as primary drivers of customer happiness.

### C. Model Training & Cross-Validation
* Evaluated diverse classifier architectures: **Logistic Regression, Decision Trees, Random Forest, Gradient Boosting, XGBoost, Support Vector Machines (SVM), and k-Nearest Neighbors (k-NN)**.
* Applied **Stratified K-Fold Cross-Validation** to preserve target class balance across folds on small sample sizes.
* Executed Hyperparameter Tuning to reduce overfitting and maximize validation accuracy.

---

## ⚠️ 3. Challenges Faced

1. **Small Sample Size ($N = 126$):**
   * *Impact:* With only 126 data points, complex ensemble models and deep decision trees are highly susceptible to overfitting and sample variance.
   * *Mitigation:* Employed Cross-Validation, constrained model hyperparameters (e.g., max depth, minimum samples per leaf), and prioritized lower-variance models.

2. **Categorical / Ordinal Rating Granularity:**
   * *Impact:* Features are discrete Likert scores (1 to 5). Standard continuous metrics and linear boundaries can struggle to capture non-linear jumps between ratings.
   * *Mitigation:* Tested both tree-based models capable of handling non-linear decision thresholds and distance-based estimators with appropriate feature scaling.

3. **Feature Redundancy vs. Minimization Goal:**
   * *Impact:* Balancing highest accuracy while reducing feature count to a minimal set.
   * *Mitigation:* Rigorously evaluated subset combinations against validation metrics to find a parsimonious model that retains high predictive accuracy.

---

## 🏆 4. Accomplishments

* **Target Exceeded:** Achieved cross-validated prediction accuracy exceeding the project target benchmark of **73%**.
* **Effective Feature Reduction:** Demonstrated that a streamlined feature subset—specifically prioritizing **`X1` (On-time delivery)** and **`X5` (Courier satisfaction)**—yields comparable or superior classification performance relative to using all 6 survey questions.
* **Actionable Insights:** Translated quantitative model findings directly into practical business recommendations regarding delivery logistics and order quality control.

---

## 💡 5. Recommendations

1. **Streamline the Survey (Reduce Customer Fatigue):**
   * Reduce the 6-question survey to a focused **2 to 3 question survey**, centering on **`X1` (Delivery On-Time)** and **`X5` (Courier Satisfaction)**. Shortening the survey increases completion rates and provides cleaner signal on core happiness metrics.

2. **Prioritize Order Accuracy & Content Quality (`X2`):**
   * `X2` (*Contents of order as expected*) received the lowest mean score ($2.53/5.00$). ACME should audit order fulfillment, packaging, and item descriptions to address customer expectation gaps.

3. **Focus Operational Incentives on Delivery Execution (`X1` & `X5`):**
   * Since courier satisfaction and delivery speed are top predictors of customer happiness, ACME should invest in courier driver training, real-time tracking improvements, and performance-based driver incentives.

4. **Future Data Collection & Enhancement:**
   * Expand data collection beyond $N=126$ responses to support robust model retraining.
   * Include additional contextual operational features (e.g., actual delivery duration in minutes, order value, delivery time of day, customer retention history) for deeper causal modeling.
