# Data-Centric Bank Customer Churn Prediction

**M.Tech Thesis Project | Indian Institute of Technology (IIT) Jodhpur**

| | |
|---|---|
| **Author** | Samrat Chowdhury (M25AI1077) |
| **Supervisor** | Dr. Nishant Kumar, SMIEEE, FIETE |
| **Department** | School of Artificial Intelligence and Data Science |
| **Status** | ✅ Complete — Phase 1 & Phase 2 |

---

## Project Overview

Customer churn in retail banking represents a compounding financial challenge: replacing a lost customer costs five to seven times more than retaining one. This project develops a **data-centric machine learning framework** for churn prediction, demonstrating that systematic dataset refinement — not algorithmic complexity — is the primary driver of model performance.

The framework addresses three structural problems in real banking data:

1. **Class imbalance** — churned customers constitute only ~20% of the portfolio, biasing standard classifiers toward the majority class.
2. **Limited feature expressiveness** — raw attributes (balance, age) fail to capture customer engagement intensity.
3. **Economically uncalibrated decisions** — the default 0.50 probability threshold treats false negatives and false positives as equally costly, which is false in banking.

---

## Research Contributions

| # | Contribution |
|---|---|
| 1 | Domain-driven feature engineering: Balance-per-Product (F₁), Tenure-to-Age Ratio (F₂), Is_Senior, Active-Credit Interaction (F₃) |
| 2 | SMOTE class rebalancing — ablation-validated 16.7pp Recall improvement |
| 3 | Comparative benchmarking of 5 classifiers (LR, DT, RF, XGBoost, LightGBM) |
| 4 | Hybrid ensemble: soft voting (LightGBM + XGBoost) and stacking (RF + XGBoost + LightGBM → Logistic Regression) |
| 5 | SHAP explainability — global feature importance and local per-customer explanations |
| 6 | Cost-sensitive threshold optimisation — τ = 0.06 minimises total financial loss to $730,500 |

---

## Key Results

| Model / Configuration | Recall | ROC-AUC | Notes |
|---|---|---|---|
| LightGBM (standalone) | 0.641 | 0.849 | Best single classifier |
| Soft Voting (LGBM + XGB) | 0.617 | 0.847 | Default threshold τ = 0.50 |
| Stacking Ensemble | 0.870 | — | Default threshold τ = 0.50 |
| Soft Voting (cost-optimised) | **0.948** | — | τ = 0.06, min cost $730,500 |
| Stacking (threshold-optimised) | **0.961** | — | τ = 0.10 |

**SHAP finding:** Age (45–60 bracket) and Tenure-to-Age Ratio are the two strongest global churn drivers.

---

## Publications

1. **Samrat Chowdhury and Nishant Kumar**, "A Data-Centric Framework for Bank Customer Churn Prediction Using Domain-Driven Feature Engineering and Class Rebalancing," *IEEE NELE 2025 Conference (NELE26000062)*, VIT Vellore, India. **[Accepted and Presented | Paper ID: 2522]**

2. **Samrat Chowdhury and Nishant Kumar**, "Data-Centric Churn Prediction in Retail Banking Using Hybrid Ensemble Learning and Threshold Optimization," submitted to *2nd IEEE International Conference on Renewable Energy and Sustainable E-Mobility (RESEM-2026)*, MANIT Bhopal, India. **[Under Review | Paper ID: 1025]**

---

## Repository Structure

```text
Customer_Churn_Thesis/
│
├── data/
│   ├── raw/
│   │       Churn_Modelling.csv              # Original Kaggle dataset (~10,000 records)
│   └── processed/
│           train_augmented.csv              # SMOTE-augmented training set
│           test_original.csv               # Held-out test set (unmodified)
│           Churn_Data_Augmented_Processed.csv
│
├── notebooks/
│   ├── phase1/
│   │       01_Data_Engineering_Phase1A.ipynb     # EDA, feature engineering, SMOTE
│   │       02_Model_Benchmarking_Phase1B.ipynb   # 5-classifier benchmarking
│   │       Phase1_Comparison.ipynb               # Raw vs refined baseline comparison
│   │
│   └── phase2/
│           03_Hybrid_Model_Phase2.ipynb           # Soft voting ensemble + feature importance
│           04_SHAP_Explainability_Phase2.ipynb    # Global + local SHAP analysis
│           05_Cost_Sensitive_Churn_Model_phase2.ipynb  # Cost matrix + threshold optimisation
│           06_ablation_hybrid_threshold_colab_phase2.ipynb  # Ablation + stacking ensemble
│
├── results/
│   ├── figures/                            # 17 output PNG figures
│   │       Phase1_Comparison_model_recall_comparison.png
│   │       01_Data_Engineering_Phase1A_AgeDistribution_ChurnVSRetain.png
│   │       01_Data_Engineering_Phase1A_BalancePerProductVsChurnStatus.png
│   │       01_Data_Engineering_Phase1A_FeatureCorrelationMatrix.png
│   │       02_Model_Benchmarking_Phase1B_benchmark.png
│   │       02_Model_Benchmarking_Phase1B_Confusion_Matrix_LightGBM.png
│   │       03_Hybrid_Model_Phase2_Hybrid_Model_Confusion_Matrix.png
│   │       03_Hybrid_Model_Phase2_Top_10_Important_Features.png
│   │       04_SHAP_Explainability_Phase2_shap_summary_plot.png
│   │       04_SHAP_Explainability_Phase2_shap_feature_importance.png
│   │       04_SHAP_Explainability_Phase2_shap_dependence_age.png
│   │       04_SHAP_Explainability_Phase2_shap_waterfall_index_0.png
│   │       04_SHAP_Explainability_Phase2_shap_waterfall_index_5.png
│   │       05_Cost_Sensitive_Churn_Model_phase2_cost_optimization_curve.png
│   │       05_Cost_Sensitive_Churn_Model_phase2_Cost_Sensitive_Confusion_Matrix.png
│   │       06_ablation_hybrid_threshold_colab_phase2_stacking_confusion_matrix.png
│   │       06_ablation_hybrid_threshold_colab_phase2_threshold_recall_curve.png
│   │
│   └── tables/                             # CSV exports of all result metrics
│           Phase1_Comparison_results.csv
│           phase1_results.csv
│           02_Model_Benchmarking_Phase1B_benchmark.csv
│           03_Hybrid_Model_Phase2_hybrid_results.csv
│           04_SHAP_Explainability_Phase2_SHAP_results.csv
│           04_SHAP_Explainability_Phase2_shap_values.csv
│           05_Cost_Sensitive_Churn_Model_phase2_cost_sensitive_results.csv
│           06_ablation_hybrid_threshold_colab_phase2_ablation_results.csv
│
├── papers/
│   ├── paper1_model_comparison/            # IEEE NELE 2025 (Accepted)
│   └── paper2_hybrid_model/               # IEEE RESEM 2026 (Under Review)
│
├── presentation/
│       Samrat_M25AI1077_Thesis_FINAL_20slides.pptx   # Final viva presentation
│       Speaker_Notes_All_20_Slides.md                 # Speaker notes
│
├── thesis/
│       Samrat_M25AI1077_Thesis_FINAL_v5_.docx         # Final thesis document
│       Samrat_M25AI1077_Thesis_FINAL_v5_.pdf          # PDF version
│       turnintin_similarity_report_*.pdf               # Turnitin plagiarism report
│       turnintin_AI_Writing_report_*.pdf               # Turnitin AI writing report
│
└── requirements.txt                        # Python dependencies
```

---

## Setup and Reproducibility

### Prerequisites
- Python 3.8 or higher
- Jupyter Notebook or Google Colab

### Installation

```bash
# Clone the repository
git clone https://github.com/schowdhury34/bank-customer-churn-prediction
cd Customer_Churn_Thesis

# Install dependencies
pip install -r requirements.txt
```

### Running the Pipeline

Execute notebooks in the following order for full reproducibility:

```bash
# Phase 1
notebooks/phase1/01_Data_Engineering_Phase1A.ipynb   # → produces train_augmented.csv, test_original.csv
notebooks/phase1/02_Model_Benchmarking_Phase1B.ipynb # → produces benchmarking results
notebooks/phase1/Phase1_Comparison.ipynb             # → raw vs refined comparison

# Phase 2
notebooks/phase2/03_Hybrid_Model_Phase2.ipynb
notebooks/phase2/04_SHAP_Explainability_Phase2.ipynb
notebooks/phase2/05_Cost_Sensitive_Churn_Model_phase2.ipynb
notebooks/phase2/06_ablation_hybrid_threshold_colab_phase2.ipynb
```

### Dataset

The project uses the publicly available [Bank Customer Churn Prediction dataset](https://www.kaggle.com/datasets/gauravtopre/bank-customer-churn-dataset) from Kaggle (~10,000 anonymised records). Place `Churn_Modelling.csv` in `data/raw/` before running the pipeline.

---

## Methodology Summary

```
Raw Data (Kaggle)
      │
      ▼
01. EDA + Feature Engineering
      │  Balance-per-Product (F₁) = AccountBalance / NumOfProducts
      │  Tenure-to-Age Ratio (F₂) = Tenure / Age
      │  Is_Senior = 1 if Age ≥ 60
      │  Active-Credit Interaction (F₃) = CreditScore × IsActiveMember
      ▼
02. SMOTE (training set only — no data leakage)
      │  1,630 churned → 6,370 churned (balanced 50/50)
      ▼
03. Benchmarking (5 classifiers)
      │  Primary metric: Recall (churn class)
      │  Winner: LightGBM (Recall = 0.641, AUC = 0.849)
      ▼
04. Hybrid Ensembles
      │  Soft Voting (LGBM + XGB): Recall = 0.617
      │  Stacking (RF + XGB + LGBM → LR): Recall = 0.870
      ▼
05. SHAP Explainability
      │  Top drivers: Age, Tenure_Age_Ratio, IsActiveMember
      │  High-risk zone: customers aged 45–60
      ▼
06. Cost-Sensitive Threshold Optimisation
         C_FN = $5,000 | C_FP = $500 | τ_opt = 0.06
         Soft Voting: Recall = 0.948, Min Cost = $730,500
         Stacking:    Recall = 0.961 at τ = 0.10
```

---

## License

This project is submitted in partial fulfilment of the requirements for the degree of Master of Technology at IIT Jodhpur. All rights reserved.
