# Capstone Project  
## **Buy vs. Rent in 2025–2026: A ZIP-Level Cash-Flow Comparison (Final Report)**  

**Author:** Siddarth R. Mannem  
**Course:** AI/ML Professional Certificate — Capstone Project Final 24.1  

---

## 1. Define the Problem Statement  
The central question this project addresses is:  
> *Is it financially better to buy or rent a home in the United States in 2025–2026?*  

The challenge lies in projecting ownership and rental cash flows over a multi-year horizon under varying economic conditions (mortgage rates, property taxes, insurance, and maintenance costs).  
The machine learning solution builds a **predictive and scenario-based framework** to quantify which ZIP codes are more favorable for homeownership versus renting.  

**Goals:**  
- Compare the 5-year Net Present Value (NPV) of buying vs. renting for every U.S. ZIP code.  
- Identify macroeconomic thresholds (e.g., interest rate sensitivity) where buying becomes less favorable.  
- Develop explainable, data-driven visualizations for policymakers and consumers.  

**Potential Benefits:**  
- Guides consumers and financial advisors on real estate affordability trends.  
- Provides investors and housing policy analysts with granular ZIP-level insights.  
- Quantifies “tipping points” in mortgage and tax conditions for better financial planning.  

---

## 2. Model Outcomes or Predictions  
- **Learning Type:** Regression (continuous output) and Classification (binary buy/rent recommendation).  
- **Algorithms Used:** Linear Regression, Ridge, Lasso, ElasticNet, Random Forest, Gradient Boosted Trees.  
- **Learning Approach:** Supervised Learning — using historical ZIP-level data of home prices, rents, mortgage rates, and taxes.  
- **Predicted Outputs:**  
  1. **Regression Target:** `own_minus_rent` — estimated annual cost difference (ownership − rent).  
  2. **Classification Target:** `buy_recommend` — binary recommendation (1 = buy, 0 = rent).  

The model outputs were later extended for **scenario-based predictions**, enabling sensitivity analyses across rate, tax, and maintenance variations.

---

## 3. Data Acquisition  
**Sources Used:**  
- **Zillow Research (ZORI & Home Value Index)** — median rent and price by ZIP code.  
- **Federal Reserve Economic Data (FRED)** — national mortgage rate trends.  
- **U.S. Census & Local Tax Assessors** — property tax and insurance rate averages.  
- **Internal Integration:** Combined and cleaned in `master_housing_dataset_clean.csv` and `master_housing_dataset_zip.csv`.  

**Data Volume:**  
- ~20,000 ZIP-level observations spanning 2015–2024, normalized to 2025 projections.  

**Data Visualization Highlights:**  
- Distribution plots of ownership vs. rent deltas.  
- Scatterplots showing rent-to-price ratio vs. mortgage rate.  
- Heatmaps of buy favorability across states.  

These exploratory visuals validated that mortgage rate and rent-to-price ratio were the most predictive features for buy–rent outcomes.

---

## 4. Data Preprocessing / Preparation  

### a. Cleaning and Quality Control  
- Removed nulls and outliers from price, rent, and mortgage rate columns.  
- Recalculated ratios (`rent_to_price_ratio`, `own_minus_rent`) to ensure consistency.  
- Standardized financial percentages (tax, insurance, maintenance) as decimal fractions.  

### b. Handling Missing Values  
- Used **median imputation** for numerical variables and **mode imputation** for categorical fields.  
- Filled sparse ZIP-level data with regional/state averages to maintain stability.  

### c. Splitting and Encoding  
- **Train/Test Split:** 75% training, 25% test split (stratified for classification).  
- **Feature Scaling:** StandardScaler for numeric fields; OneHotEncoder for categorical variables (state, region).  
- **Data Pipeline:** Implemented via `ColumnTransformer` to ensure consistent preprocessing.  

### d. Data Artifacts  
- Clean master dataset saved as: `model_training_frame_v2.csv`  
- Pretrained transformer and model artifacts stored in `/artifacts/` for reuse in scenario analysis.

---

## 5. Modeling  

### Algorithms Implemented  
| Model Type | Algorithm | Purpose |
|-------------|------------|----------|
| Linear Models | OLS, Ridge, Lasso, ElasticNet | Baseline regression, interpretability |
| Ensemble Methods | Random Forest, Gradient Boosted Trees | Non-linear interactions, robustness |
| Classification | Logistic Regression | Binary buy/rent recommendation |
| Regression | Linear & Ridge Regression | Continuous ownership–rent delta prediction |

All models were built using scikit-learn pipelines for modularity and reproducibility.  

### Model Explainability  
- Linear coefficients and permutation importances were used to interpret top predictors:  
  **Mortgage Rate**, **Rent-to-Price Ratio**, **Tax Rate**, and **Maintenance %** emerged as the strongest drivers of affordability.  

---

## 6. Model Evaluation  

**Metrics Used:**  
- **Regression:** R², MAE, RMSE  
- **Classification:** Accuracy, ROC-AUC, Confusion Matrix  

**Key Findings:**  
- Linear models achieved R² ≈ 0.72 with consistent generalization.  
- Regularized models (Ridge, ElasticNet) improved feature stability and reduced overfitting.  
- Ensemble models (Random Forest, GBDT) provided stronger nonlinear capture, with MAE improvement of ~12% over OLS.  
- Feature importance across models was consistent — mortgage rate and rent/price ratio were the leading predictors.  

**Evaluation Visuals:**  
- Model coefficient bar charts.  
- Scenario-level KPI dashboards.  
- 2×3 grid of visual comparisons across scenarios.  

---

## 7. Scenario & Sensitivity Analysis  

**Objective:**  
Extend static models into dynamic simulations reflecting different macroeconomic conditions.  

**Scenarios Modeled:**  
- **Base:** Current rate/tax/insurance baseline.  
- **LowRates:** –10% mortgage rate.  
- **HighRates:** +25% mortgage rate.  
- **HighTax:** +0.2% property tax.  
- **HighInsMaint:** +20% insurance + maintenance.  

**Visualization Outputs:**  
- Scenario bar charts for buy share and flip rate.  
- State-level histograms of cost differentials.  
- Dual-axis rate-sensitivity line chart showing buy-share drop vs. NPV delta rise.  
- Interactive ipywidgets dashboard for scenario and state filtering.  

**Key Takeaways:**  
- Mortgage rate changes dominate all other variables.  
- Buy favorability flips around **1.05× mortgage multiplier**.  
- Tax and insurance sensitivities are localized, not national.  
- Midwest and Southeast states remain resilient affordability zones.  

---

## 8. Results & Insights  

**Main Results:**  
- At 2025 baseline conditions, ~60–65% of ZIPs favor buying.  
- A +1–1.5% rate hike would flip majority of ZIPs to rent-favorable.  
- Regional disparities persist — Midwest & Southeast remain buy-positive, coastal markets remain rate-sensitive.  

**Visual Summary Highlights:**  
- Scenario KPI Dashboard (6.1)  
- Flip Rate Comparison (6.2)  
- State-Level Delta Distributions (6.3)  
- Combined Grid Dashboard (6.5)  
- Mortgage Rate Sensitivity Curve (7.1)  

---

## 9. Next Steps  
- Extend projection horizon from 5 years → 10 years for long-term trend analysis.  
- Integrate **time-series models (ARIMA / Prophet)** for mortgage and rent forecasts.  
- Explore **clustering (unsupervised)** to identify ZIP groups with similar affordability patterns.  
- Add **interactive web dashboard (Plotly Dash / Streamlit)** for public visualization and policy outreach.

---

## 10. Outline of Project  

- [Notebook 0: Data Ingestion](notebooks/00_data_ingestion.ipynb)  
- [Notebook 1: Initial Report & EDA](notebooks/01_initial_report_eda.ipynb)  
- [Notebook 2: Cost Projection Model](notebooks/02_cost_projection_model.ipynb)  
- [Notebook 3: Scenario & Sensitivity Analysis](notebooks/03_scenario_analysis.ipynb)  

---

### 📬 **Contact and Further Information**  
**Author:** Siddarth R. Mannem  
**Email:** siddharth451m@gmail.com  
**LinkedIn:** [linkedin.com/in/siddarth-mannem](https://linkedin.com/in/siddarth-mannem)  
**GitHub:** [AIMLcert/Capstone-Assignment-20.1](https://github.com/AIMLcert/Capstone-Assignment-20.1.git)  

---
