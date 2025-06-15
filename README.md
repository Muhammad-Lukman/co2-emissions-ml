# Predicting National CO₂ Emissions Using Economic and Energy Indicators

This project uses historical global data and machine learning to predict national CO₂ emissions based on economic performance, energy use, and environmental metrics.

---
👤 **Author**: Muhammad Lukman  
🧪 Microbiology + Machine Learning Researcher  
📧 [Email](dr.mlukmanuaf@gmail.com) | 🔗 [LinkedIn](https://www.linkedin.com/in/muhammad-lukman-790468304) | 💻 [GitHub](https://github.com/Muhammad-Lukman)

🗓️ **Last Updated**: June 2025

---

## Dataset

- **Source**: [Our World in Data - CO₂ and GHG Emissions](https://github.com/owid/co2-data)
- **Period**: 1750–2022  
- **Coverage**: 200+ economies, 76+ indicators  
- **License**: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/legalcode.en)

---

## Objective

> We built multiple variants of machine learning models to predict national CO₂ emissions using economic and energy indicators. After removing proxy features such as total greenhouse gases and CO₂ including land-use change, our final model — a Random Forest — still achieved an R² of 0.9924 on the test set.

---

## ML Models Used

| Model              | CV R²   | Test R² | MAE     | RMSE   |
|-------------------|---------|---------|---------|--------|
| Linear Regression | 0.57    | 0.57    | ~612    | ~1251  |
| Ridge Regression  | 0.57    | 0.57    | ~611    | ~1251  |
| **Random Forest** | 0.9996  | 0.9995  | **5.6** | **36.5** |
| Random Forest (No GHG) | 0.9989  | 0.9924  | 11.2    | 159.5  |

---

## Highlights from EDA

- Strong log-scale correlation between GDP and CO₂.
- GHG indicators (especially `total_ghg_excluding_lucf`) dominate feature importance.
- Many features had extreme skewness — corrected using `QuantileTransformer`.
- High correlation detected and removed (`threshold > 0.90`).

---

## Pipeline Overview

### 1. Data Cleaning & Imputation
- Interpolation per country-year
- IterativeImputer for remaining values

### 2. Feature Engineering
- Ratio features (e.g., CO₂ per capita, energy per GDP)
- Dropping highly correlated fields (ρ > 0.90)
- Temporal encoding via `year`

### 3. Scaling
- `QuantileTransformer` with `normal` output distribution

### 4. Modeling & Evaluation  
   - Models: Linear Regression, Ridge, Random Forest  
   - Final model: Random Forest w/o GHG indicators  
   - Cross-validation: 5-Fold CV with MAE, RMSE, and R²

---

## Visuals Included

- CO₂ vs GDP (log-log scatter)
- Heatmaps (full and grouped)
- Actual vs Predicted plots
- Residual error distribution
- Feature importance rankings

All plots are **colorblind-friendly**, **publication-ready**, and saved to `/outputs`.

---

## Requirements

Install with:

```bash
pip install -r requirements.txt
