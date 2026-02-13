# Network Intrusion Detection: Classification Modeling of NSL-KDD Dataset

**"From Detection to Defence"**

## Project Overview

Multi-class classification system to identify and categorise five types of network traffic — Normal, DoS, Probe, R2L, and U2R attacks — using the NSL-KDD cybersecurity dataset. The project addresses extreme class imbalance where the most dangerous attack types (R2L at 0.79% and U2R at 0.04%) are also the rarest, making detection particularly challenging.

## Key Results

| Metric | Baseline | Final Model | Improvement |
|--------|----------|-------------|-------------|
| Macro F1 | 0.556 | 0.641 | +0.085 |
| R2L Recall | 0.069 | 0.296 | +0.227 |
| U2R Recall | 0.035 | 0.180 | +0.145 |
| Accuracy | 0.758 | 0.807 | +0.049 |

**Final model:** XGBoost with balanced class weights, tuned via RandomizedSearchCV (100 iterations, 3-fold CV).

## Methodology

### Data Preparation
- 125,973 training records, 22,544 test records
- 47 engineered features from 41 original attributes
- Smoothed target encoding for high-cardinality service feature (70 categories)
- RobustScaler for numerical features to handle extreme outliers
- Evidence-based retention of near-constant features critical for rare attack detection

### Models Compared
17 model-strategy combinations across:
- **3 algorithms:** Logistic Regression, Random Forest, XGBoost
- **5 imbalance strategies:** Baseline, SMOTE, cost-sensitive (balanced weights), cost-sensitive (custom weights), SMOTE + cost-sensitive

### Key Findings
- Cost-sensitive learning outperformed SMOTE for extreme minority classes (U2R with only 52 training samples)
- Top 5 features account for 45.7% of model importance, with `flag_S0` (SYN flood signature) as the strongest discriminator at 19.0%
- Near-constant features like `root_shell` (zero for 99.96% of records) proved second most important overall, validating the decision to retain them during feature engineering
- High ROC-AUC (0.952) alongside moderate accuracy (0.807) reveals the gap between discrimination capability and prediction performance in imbalanced datasets

## Repository Contents

| File | Description |
|------|-------------|
| `NSL_KDD_Intrusion_Detection_Classification.ipynb` | Full Jupyter notebook with code, analysis, and visualisations |
| `NSL_KDD_Classification_Report.docx` | Written report with detailed methodology and findings |
| `data/` | NSL-KDD training and test datasets |

## Tools & Libraries

Python, pandas, NumPy, scikit-learn, XGBoost, imbalanced-learn (SMOTE), matplotlib, seaborn, SciPy

## Dataset

NSL-KDD dataset from the Canadian Institute for Cybersecurity, University of New Brunswick.  
Source: https://www.unb.ca/cic/datasets/nsl.html

## Author

Rebecca Stalley-Moores  
IBM Machine Learning Professional Certificate (In Progress)

---
*Completed February 2026 as part of IBM ML Professional Certificate — Supervised Machine Learning: Classification*
