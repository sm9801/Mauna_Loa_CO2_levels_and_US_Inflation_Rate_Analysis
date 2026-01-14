# Mauna Loa CO₂ Level Prediction & U.S. Inflation Rate Analysis

## Overview
This project presents a comprehensive time series analysis covering:

- Atmospheric CO₂ concentration modeling using Mauna Loa data  
- U.S. inflation rate modeling and forecasting derived from CPI data with external regressors  

The work was completed as part of **MITx MicroMasters in Statistics and Data Science** and focuses on trend decomposition, stochastic modeling, and forecast evaluation.

---

## Project Structure
- CO₂ trend and seasonal decomposition  
- Autocovariance analysis of time series models  
- Inflation rate transformation and detrending  
- Autoregressive (AR) and SARIMAX modeling  
- Model evaluation and improvement strategies  

---

## 1. Mauna Loa CO₂ Concentration Analysis

### Objective
To model long-term atmospheric CO₂ concentration by decomposing the signal into:
- Deterministic trend  
- Seasonal (periodic) variation  
- Residual stochastic components  

### Methodology
- **Trend Model:** Quadratic regression \( F_n(t) \)  
- **Seasonality:** Monthly periodic signal computed from average residuals  
- **Final Model:**  
  \[
  X(t) = F_n(t) + P_i + R_t
  \]

### Model Evaluation
| Model | RMSE | MAPE |
|------|------|------|
| Trend only | ≈ 2.50 | ≈ 0.53% |
| Trend + Seasonality | **≈ 1.14** | **≈ 0.21%** |

### Key Insight
Including seasonal components significantly improves prediction accuracy. While the deterministic trend explains most of the variation, periodic and residual components meaningfully enhance model performance.

---

## 2. Autocovariance Functions

Analytical derivations were provided for:
- **MA(1)** autocovariance function  
- **AR(1)** autocovariance function under stationarity conditions  

These derivations establish the theoretical foundation for subsequent time series modeling.

---

## 3. U.S. Inflation Rate Modeling

### Inflation Rate Computation
Monthly inflation rates were computed from CPI data using:
\[
IR_t = \frac{CPI_t - CPI_{t-1}}{CPI_{t-1}} \times 100
\]

A logarithmic transformation was applied to CPI to stabilize variance.

### Trend Handling
- No clear seasonal trend observed  
- Outliers addressed using **Radial Basis Function (RBF) Kernel Regression**  
- Residuals modeled using autoregressive processes  

---

## 4. Autoregressive Modeling

### Lag Selection
- Autocorrelation analysis indicated **AR(3)** as the most suitable model  
- AR(p) models for \( p = 1 \) to \( 5 \) were evaluated  

| Model | RMSE | Observation |
|------|------|------------|
| AR(1) | Lowest | Poor fit quality |
| **AR(3)** | **Best** | Best balance of fit and stability |
| AR(4), AR(5) | Similar | No improvement |

### Final Inflation Model
\[
IR_t = \text{RBF Trend} + \text{AR(3) Residual}
\]

---

## 5. External Regressors & SARIMAX

### External Data
- **BER (Business Expectation Rate)** used as an exogenous regressor  
- Cross-correlation analysis used to determine optimal lag  

### Final Model
- **SARIMAX**  
  - Endogenous: log-transformed CPI inflation rate  
  - Exogenous: original (non-transformed) BER values  

### Performance
- **Best RMSE:**: 0.0527

### Key Findings
- Log transformation significantly improves CPI-based models  
- BER performs best without transformation  
- Improper scaling of external regressors degrades forecasting accuracy  

---

## Tools & Libraries
- Python  
- NumPy  
- Pandas  
- Matplotlib  
- scikit-learn  
- statsmodels  

---

## Key Takeaways
- Seasonal decomposition is critical for environmental time series modeling  
- Hybrid models outperform pure autoregressive approaches  
- External economic indicators improve inflation forecasting accuracy  
- Data scaling decisions strongly impact model performance  

---

## Author
**Seokyu Kim**
