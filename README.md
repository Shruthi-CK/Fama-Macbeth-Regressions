# Fama-Macbeth-Regressions

# Asset Pricing Models Comparison: CAPM vs Fama-French 3-Factor Model

This project empirically tests and compares two foundational asset pricing models: the Capital Asset Pricing Model (CAPM) and the Fama-French 3-Factor (FF3F) Model.

The goal is to determine if the FF3F model, which adds size (SMB) and value (HML) factors to CAPM's single market (MKT) factor, provides a superior explanation for stock returns.

The analysis follows the classic Fama-French (1993) methodology:

## 1. Data Collection

Downloads the 25 Fama-French portfolios (sorted on size and book-to-market) as the test assets, along with the three risk factors (MKT-RF, SMB, HML) and the risk-free rate (RF).

## 2. Time-Series (TS) Regressions

For each of the 25 portfolios, we run time-series regressions for both models:

* **CAPM:** `R_p - R_f = α + β_mkt * (MKT-RF)`
* **FF3F:** `R_p - R_f = α + β_mkt * (MKT-RF) + β_smb * SMB + β_hml * HML`
* **Goal:** We compare the R-squared values (explanatory power) and the alphas (unexplained returns, or pricing errors) from each model.

## 3. GRS Test

We use the Gibbons, Ross, & Shanken (GRS) test to statistically determine if the alphas from all 25 portfolios are jointly equal to zero. A failed test (a significant p-value) indicates the model is "rejected" and fails to explain the returns.

## 4. Fama-MacBeth (CS) Regressions

We perform a two-pass cross-sectional regression to test if the risk factors carry a significant risk premium.

* **Pass 1:** The TS regressions from Step 2 provide the factor betas (risk loadings) for each portfolio.
* **Pass 2:** For each month, we regress the cross-section of all 25 portfolio returns against their betas from Pass 1. This generates a time-series of risk premia (lambdas, `λ`).
* **Goal:** We check if the average lambda for each factor (MKT, SMB, HML) is statistically different from zero. This tells us if investors are actually rewarded for taking on that specific factor risk. The analysis includes the Shanken (1992) correction for errors-in-variables.

Finally, all results are compiled into an Excel report for review.
