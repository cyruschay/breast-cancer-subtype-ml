# Breast Cancer Subtype Classification using Gene Expression

Keywords: `Machine Learning`, `transcriptomics`, `glycobiology`

**Author**: Cyrus Chun Hong Au Yeung  
**Date**: November 2024
**Poster**: poster.pdf

---

## Project Overview

This project explores the role of **glycosyltransferase (GT) gene expression** in breast cancer subtype classification using ML techniques. Glycosylation, a critical post-translational modification, is known to be dysregulated in many cancers. Here, RNA-seq data from the **TCGA-BRCA** dataset is used to build predictive models for classifying tumors into five PAM50 subtypes:

- Luminal A
- Luminal B
- HER2-enriched
- Basal-like
- Normal-like

**Objectives**

- Develop and evaluate multiple ML models using GT gene expression to classify breast cancer subtypes.
- Identify key glycoenzymes that serve as predictive biomarkers for subtype classification.

## Project Structure

```bash
breast-cancer-subtype-ml/
├── data/                  # Raw and processed data files
│   ├── raw/               # Original TCGA-BRCA datasets
│   └── processed/         # Cleaned & merged expression + metadata
├── scripts/               # All R scripts used in analysis
│   ├── 01_data_wrangling.Rmd
│   ├── 02_classification.Rmd
│   └── 03_downstream_analysis.Rmd
├── results/               # Figures and plots
├── notebooks/             # Rendered RMarkdown reports
│   └── 01_data_wrangling.pdf
│   └── 02_classification.pdf
├── README.md              # Project overview and instructions
├── poster.pdf
└── .gitignore
```

## Data Source

- **TCGA Breast Cancer (BRCA)** RNA-seq data (downloaded via UCSC Xena)
- 209 GT genes identified; 182 successfully mapped to expression matrix
- Metadata includes PAM50 subtype labels and clinical variables

---

## Methods

### 1. Data Wrangling

- Filtered gene expression matrix to include GT genes only
- Merged with clinical metadata and survival information
- Removed patients without PAM50 annotations

### 2. Machine Learning Models

9 supervised learning models were trained and compared:

- Logistic Regression
- k-Nearest Neighbors (kNN)
- Decision Tree (CART)
- Random Forest (RF)
- Gradient Boosted Machines (GBM)
- XGBoost
- Support Vector Machine (SVM) - Linear, Polynomial, Radial

**Model evaluation:**

- 80/20 train-test split
- 10-fold cross-validation
- Primary metric: **Kappa Statistic** (accounts for class imbalance)

### 3. Best Model

The **SVM with polynomial kernel** performed best:

- **Accuracy**: 89.9%
- **Kappa**: 0.8555

## Key Findings

- Top GT genes: `UGT8`, `B3GNT5`, `ST8SIA1`
- Genes involved in **N-glycosylation** and **sialylation** pathways were key contributors
- Potential biomarkers for aggressive subtypes (e.g., Basal-like)

## Dependencies

This project uses **R (≥ 4.4.1)** and the following packages:

```r
library(tidyverse)
library(caret)
library(randomForest)
library(xgboost)
library(e1071)
library(rpart)
library(rpart.plot)
```

## How to Run

1. Clone this repo:
   ```bash
   git clone https://github.com/cyruschay/breast-cancer-subtype-ml.git
   ```
2. Decompress `tgca_brca_counts.tsv.zip` in `data/processed/`
3. Run the `.Rmd` files under `scripts/` in RStudio

## License

This project is licensed under the [MIT License](LICENSE).
