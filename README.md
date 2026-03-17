# 馃彞 Customer Insurance Purchase Prediction
### A Comparative Study of ML Classification Algorithms

---

## 馃搵 Table of Contents
- [Project Overview](#project-overview)
- [Business Goal](#business-goal)
- [Dataset](#dataset)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Algorithms Used](#algorithms-used)
- [Results](#results)
- [Questions Answered](#questions-answered)
- [Key Findings](#key-findings)
- [Output Files](#output-files)
- [Real-Life Applications](#real-life-applications)

---

## 馃搶 Project Overview

This project builds and compares five machine learning classification algorithms to predict whether a bank customer will purchase health insurance based on their **Age** and **Estimated Salary**. The goal is to identify the most accurate and generalizable model for deployment in a real banking environment.

---

## 馃幆 Business Goal

> As an Analyst at a Bank Insurance Company, leverage customer demographic data to build an AI model capable of predicting insurance purchase behaviour 鈥� enabling smarter, more targeted marketing campaigns.

---

## 馃搳 Dataset

| Property         | Details                              |
|-----------------|--------------------------------------|
| Records          | 400 customers                        |
| Features         | Age (18鈥�65), Estimated Salary        |
| Target           | Purchased (1 = Yes, 0 = No)          |
| Train/Test Split | 75% / 25%                            |
| Scaling          | StandardScaler applied to all models |

**To use your own dataset**, replace the synthetic block in the script with:

```python
df = pd.read_csv('Social_Network_Ads.csv')
df = df[['Age', 'EstimatedSalary', 'Purchased']]
```

---

## 馃搧 Project Structure

```
insurance-ml-project/
鈹�
鈹溾攢鈹€ insurance_ml_project.py       # Main script (all code)
鈹溾攢鈹€ README.md                     # This file
鈹�
鈹斺攢鈹€ outputs/                      # Generated after running
    鈹溾攢鈹€ fig1_eda.png
    鈹溾攢鈹€ fig2_decision_boundaries.png
    鈹溾攢鈹€ fig3_metrics.png
    鈹溾攢鈹€ fig4_confusion_matrices.png
    鈹溾攢鈹€ fig5_q1_predictions.png
    鈹溾攢鈹€ fig6_q2_predictions.png
    鈹斺攢鈹€ fig7_hypotheses.png
```

---

## 鈿欙笍 Installation

**Requirements:** Python 3.8+

Install dependencies:

```bash
pip install numpy pandas matplotlib scikit-learn
```

---

## 馃殌 Usage

```bash
python insurance_ml_project.py
```

The script will:
1. Generate / load the dataset
2. Train all 5 classifiers
3. Print metrics and predictions to the console
4. Save 7 figures as PNG files in the working directory

---

## 馃 Algorithms Used

| # | Algorithm              | Type              | Key Hyperparameters              |
|---|------------------------|-------------------|----------------------------------|
| 1 | Logistic Regression    | Linear            | default                          |
| 2 | K-Nearest Neighbours   | Instance-based    | n_neighbors=5                    |
| 3 | Support Vector Machine | Kernel-based      | kernel='rbf'                     |
| 4 | Decision Tree          | Tree-based        | max_depth=5                      |
| 5 | Random Forest          | Ensemble          | n_estimators=100, max_depth=5    |

---

## 馃搱 Results

| Algorithm            | Accuracy | Precision | Recall | F1-Score |
|----------------------|----------|-----------|--------|----------|
| Logistic Regression  | 77.0%    | 77.9%     | 86.9%  | 82.2%    |
| KNN                  | 78.0%    | 77.5%     | 90.2%  | 83.3%    |
| SVM                  | 78.0%    | 77.5%     | 90.2%  | 83.3%    |
| Decision Tree        | 76.0%    | 78.5%     | 83.6%  | 81.0%    |
| **Random Forest**    | **78.0%**| **79.1%** | 86.9%  | 82.8%    |

> 鉁� **Best Overall:** KNN & SVM (accuracy + recall)  
> 鉁� **Best Precision:** Random Forest (recommended for targeted campaigns)  
> 鉁� **Most Interpretable:** Logistic Regression

---

## 鉂� Questions Answered

### Q1 鈥� Predictions: Set 1

| Age | Salary      | Prediction     |
|-----|-------------|----------------|
| 30  | $87,000     | 鉁� PURCHASE     |
| 40  | No Salary   | 鉁� NO PURCHASE  |
| 40  | $100,000    | 鉁� PURCHASE     |
| 50  | No Salary   | 鉁� NO PURCHASE  |

### Q2 鈥� Predictions: Set 2 (Extreme Values)

| Age | Salary          | Prediction     |
|-----|-----------------|----------------|
| 18  | No Salary       | 鉁� NO PURCHASE  |
| 22  | $600,000        | 鉁� PURCHASE     |
| 35  | $2,500,000      | 鉁� PURCHASE     |
| 60  | $100,000,000    | 鉁� PURCHASE     |

### Q3 鈥� Hypotheses Testing

| Hypothesis                                          | Result              |
|-----------------------------------------------------|---------------------|
| H1: Young + high salary 鈫� more likely to buy        | 鉁� Partially Supported |
| H2: Older + high salary 鈫� less likely to buy        | 鉂� Not Supported     |
| H3: Salary has stronger impact than age             | 鉁� Supported         |

### Q4 鈥� Lessons Learned

- Feature scaling is **critical** for KNN and SVM
- No single best algorithm 鈥� choice depends on business priority (recall vs precision)
- Tree models do **not extrapolate** beyond training data range
- Missing/zero salary values **dominate** predictions regardless of age

---

## 馃攽 Key Findings

- **Salary is the dominant predictor.** Customers with no income are predicted not to purchase regardless of age.
- **Middle-aged customers (35鈥�50)** with moderate-to-high salaries are the core insurance-buying demographic.
- **KNN/SVM** are best when you want to maximise leads captured (high recall).
- **Random Forest** is best when lead quality matters more than quantity (high precision).
- **Decision Trees** are the weakest performer and most prone to overfitting.

---

## 馃梻锔� Output Files

| File                          | Description                                      |
|-------------------------------|--------------------------------------------------|
| `fig1_eda.png`                | Age vs Salary scatter + purchase rate by age group |
| `fig2_decision_boundaries.png`| Decision boundaries for all 5 classifiers       |
| `fig3_metrics.png`            | Bar charts: Accuracy, Precision, Recall, F1      |
| `fig4_confusion_matrices.png` | Confusion matrices for all 5 classifiers         |
| `fig5_q1_predictions.png`     | Q1 test points plotted on decision boundaries    |
| `fig6_q2_predictions.png`     | Q2 test points (extreme salary values)           |
| `fig7_hypotheses.png`         | Hypothesis testing 鈥� age and salary effect curves|

---

## 馃實 Real-Life Applications

### Case Study 1 鈥� Targeted Insurance Marketing
Use **Random Forest** (highest precision) to score the full customer base and identify the top 20% most likely purchasers 鈥� reducing campaign costs by up to 80% while maintaining revenue.

### Case Study 2 鈥� Loan Default Risk Profiling
Apply the same pipeline with features like credit score, debt-to-income ratio, and employment history. Use **KNN/SVM** (high recall) to flag potential defaulters for review, reducing manual processing time by ~60%.

---

## 馃懁 Author

**Analyst 鈥� Bank Insurance Company**  
Comparative ML Study | February 2026

---

> *"The goal is not to find the most complex model, but the most appropriate one."*
